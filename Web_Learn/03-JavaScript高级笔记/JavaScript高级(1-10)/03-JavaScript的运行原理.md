- 浏览器内核是由两部分组成的 , 以webkit为例
- WebCore : 负责HTML解析 , 布局 , 渲染等等的相关的工作
- JavaScriptCore: 解析 , 执行JavaScript代码
- 另外一个强大的JavaScript引擎 : V8

# V8引擎的执行原理

- V8是用C++编写的Google开源高性能JavaScript和WebAssembly引擎
  - 它用于Chrome和Node.js
- V8可以独立运行 , 也可以嵌入到任何C++应用程序

#### 执行原理

JavaScript源代码 —解析—（转成）—AST抽象语法树—lgnition（通过 ： 转换）—ByteCode（字节码）—— 运行结果

![JavaScriptV8引擎运行流程](D:\OneDrive\桌面\JavaScriptV8引擎运行流程.png)



# V8引擎的架构

- V8引擎本身的源码大概超过100w行C++代码

- **parse模块** : 会将JavaScript代码转换成AST(抽象语法树) , 
  - 解决器并不直接认识JavaScript代码
  - 函数没有调用 , 不会转换AST
- **lgnition模块** : 解释器 , 会将AST转换成ByteCode(字节码)
  - 同时会收集TurboFan优化所需要的信息
- **TurboFan模块** : 编译器 , 可以将字节码编译为CPU可以直接执行的机器码
  - 如果一个函数被多次调用 , 会被标记为热点函数

# JavaScript的执行过程

### 1.初始化全局对象

- js引擎会再代码没有执行之前 , 会再堆内存中创建一个全局对象 :**Global Object (GO)**
  - GO :window

- 该对象所有的作用域(scope)都可以访问
- 里面会包含Date(时间) , array(数组) , string(字符串) , number(数字) , settimeout(定时器)

### 2.执行上下文(Execution contexts)

- js引擎的内部有个执行上下文栈 , 用于执行代码的调用栈
  - 执行的是全局的代码块
    - 全局的代码为了执行会构建一个global execution context(GEC)
      - GEC会被放入到ECS中执行
  - GEC被放入到ECS中里面包含两部分内容
  - 第一部分
    - 在代码执行前 ,在parser转成AST的过程中
      - 会将全局定义的变量 , 函数等都加入到GO中
        - 对于全局上下文中VO就是GO了
        - 但并不会赋值
          - 这个过程也称之为变量的作用域提升(hoisting)
  - 第二部分
    - 在代码执行中 , 对变量赋值 , 或者执行其他的函数

# 认识VO对象(Variable object 对象)

- 每一个执行上下文会关联一个VO , 变量和函数声明会被添加到这个VO对象中
  - 去当全局代码被执行的时候 , VO就是GO对象了
- 全局上下文中关联
  - 作用域链
  - VO
  - this

# 全局代码执行

1. 执行前 ,
2. 变量 函数会先放到VO中 (GO)
3. 但是变量还没有赋值 ,函数不同
4. 都是undefined
5. 开始执行后
6. 变量在GO中开始每一个都赋值
7. 在展示出来



# 函数执行体中的变量

- 当执行的过程中执行到一个函数
  - 那就会根据这个函数体中的代码
    - 创建一个函数执行上下文(function execution context 简称:FEC)
    - 并且加入到执行上下文栈(Execution contexts stack)中
- 因为每一个执行上下文都会关联一个VO 
  - 一个函数执行上下文中 ,会创建一个AO对象(Activation object)

# AO对象 : 激活对象

- AO对象会使用arguments作为初始值
  - 并且初始值是传入的参数
- AO对象会作为执行上下文的VO来存放函数中的变量的初始值



# 函数多次执行调用

- 每一次函数执行调用都是
  - 创建一个执行上下文 : 创建VO
  - VO关联AO
    - 在AO对象中创建添加执行
- 第二次执行调用
  - 会再堆内存中将上一个AO销毁 : 因为第一个函数执行上下文已经执行完毕
    - 在重新创建一个AO
  - 重复多次



# 函数的相互调用

- 第一个函数执行上下文中调用另一个函数
  - 核心点就是
  - 在创建一个AO
    - 可以多次创建AO
  - AO执行完成后销毁



# 作用域和作用域链

- 当进入到一个执行上下文时
  - 执行上下文也会关联一个作用域链(Scope Chain)
    - scope : 作用域
    - chain: 链
  - 作用域链是一个对象列表
    - 用于变量标识符的求值
  - 当进入一个执行上下文时,  这个作用域链被创建 , 并且根据代码类型 ,添加一系列的对象
  - 函数被创建时, 就已经确定了作用域链

#### 代码类型

- 全局代码
- 函数代码