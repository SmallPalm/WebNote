# GO: Global Object理解

- 在JS代码执行前会在堆内存中创建一个全局对象 为 (GO) : Global Object
- 用于存放一些定义好的变量方法
  - 如Date，Array，String，Number，setTimeout等方法	
- 同时在语法分析 转成 AST 的过程中也会将一些变量 函数 存放在GO中，
  - 只是变量的初始值是undefined
  - **语法分析和 AST 生成**：
    - 当编译器进行语法分析时，会对源码进行扫描和解析，识别其中的关键字、变量名、函数名等，并**根据语言的语法规则生成对应的抽象语法树**（AST）。这一步将源代码解析为一棵树结构，树的每个节点代表源代码的一个语法成分（如变量声明、函数调用、表达式等）。





# AO: Activation Object理解

- 函数在执行前会先在堆内存中创建一个AO （Activation Object）对象 
- AO （Activation Object）对象  ： 存放arguments 对应函数的参数，以及在函数中定义的变量，初始化为Undefined



# VO：Variable Object理解

- Variable Object 在执行函数时，会在执行上下文栈（ECS）中进入一个函数执行上下文中（FEC）其中有三个核心
- 核心之一是VO
- 指向的是当前函数在内存解析时创建的AO，而在全局执行上下文中指向的是GO