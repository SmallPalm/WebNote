# 声明变量

- TypeScript中定义变量需要指定 标识符 的类型。
  - 声明的变量的类型称之为类型注解
  - 没有声明的变量
    - TS默认会进行类型检测
- TS中小写和大写是有区别的
  - string是TS中定义的字符串类型
  - String是ECMAScript中定义的一个类

# 变量的类型推导

- 开发中, 并不会在声明变量是都写上对应的数据类型
- 这时的TS本身的特性会帮助我们推断出变量相对应的数据类型



# JavaScript - number类型

- 数字类型是开发中经常使用的类型
  - TS和JS一样, 不区分整数类型和浮点数类型
    - 统一称之为number类型
- 数字的进制
  - 二进制 : 0b
  - 八进制 : 0o
  - 十六进制 : 0x



# JavaScript - boolean类型

- boolean类型只有两个取值：true和false，非常简单



# JavaScript - string类型

- string类型是字符串类型
  - 可以使用单引号或者双引号表示
- 支持ES6的模板字符串来拼接变量和字符串



# JavaScript - Array类型

- 数组类型的定义有两种方式
  1. Array<string>事实上是一种泛型的写法，我们会在后续中学习它的用法
  2. 定义相同类型的数组
     - string[] : 只允许字符串存在的数组
     - array[] : 只运行数字运行的数组

# JavaScript - Object类型

- object对象类型可以用于描述一个对象
  - 但是从对象中我们不能获取数据，也不能设置数据

# JavaScript - Symbol类型

- 在ES5中

  - 不可以在对象中添加相同的属性名称的

- 在ES6中

  - 可以通过symbol来定义相同的名称

  - 因为Symbol函数返回的是不同的值

  - ```tsx
    const s1 : symbol = Symbol("title")
    const s2 : symbol = Symbol("title")
    
    const person = {
        [s1]: "程序员",
        [s2]: "老师"
    }
    ```



# JavaScript – null类型

# JavaScript - undefined类型

- 在 JavaScript 中

  - undefined 和 null 是两个基本数据类型

- 在TypeScript中

  - 它们各自的类型也是undefined和null
  - 也就意味着它们既是实际的值
    - 也是自己的类型

- ```tsx
  let n: null = null
  let u: undefined = undefined
  ```



# 函数的参数类型

- 函数是JavaScript非常重要的组成部分
- TypeScript允许我们指定**函数的参数**和**返回值的类型**。
- 参数的类型注解
  - 声明函数时
    - 可以在每个参数后添加类型注解
    - 以声明函数接受的参数类型

# 函数的返回值类型

- 添加返回值的类型注解, 这个注解出现在函数列表的后面

- 跟变量的类型注解相同
  - 通常情况不需要返回类型注解
  - 因为TS会根据Return返回值推断函数的返回值类型



# 匿名函数的参数

- 匿名函数的参数与函数参数的声明会有一些不同

- 当一个函数出现在TypeScript可以确定该函数会被如何调用的地方时, 该函数的参数会自动指定类型

- ```tsx
  let name = ['a', 'b', 'c', 'd']
  names.forEach((item) => itme.toUpperCase())
  ```

- 不需要指定item的类型

- 为TypeScript

  - 会根据forEach函数的类型
  - 以及数组的类型推断出item的类型

- 这是过程称之为上下文类型

- 因为函数执行的上下文可以帮助确定参数和返回值类型



## 限制函数参数为对象类型

- ```tsx
  function foo(point:{x: number, y: number}){}
  ```

- 使用一个对象来作为类型

  - 在对象我们可以添加属性
    - 并且告知TypeScript该属性需要是什么类型
  - 属性之间可以使用 , 或者 ; 来分割
    - 最后一个分隔符是可选的
  - 每个属性的类型部分也是可选的
    - 如果不指定，那么就是any类型

### 可选类型

- ```tsx
  function foo(point:{x: number, y: number, z?:number}){}
  ```

- 对象的属性可以有z, 也可以没有z

- x和y就是必须传入的, 如果不传会自动报错

# TypeScript - any类型

- 在某些情况下, 我们无法确定一个变量的类型
  - 可能变量会发生一些变化
    - 这种情况可以使用Any类型
- Any类型的变量可以进行任何的操作
  - 获取不存在的属性, 方法
  - 赋值任何类型的值
    - 如 number, string, symbol

用处

- 对于某些情况的处理过于繁琐不希望添加规定的类型注解
- 或者在引入一些第三方库时, 缺失了类型注解
  - 这时可以使用any类型

# TypeScript - unknown类型

- unknown用于描述类型不确定的变量
  - unknown是TypeScript比较特殊的类型

- 和any类型类似
  - unknown类型的值上做任何事情都是不合法的

## any 和 unknown类型的区别

类型检测

1. 赋值到any不会有类型检测 : 
   - any类型的值执行任何操作而不会得到编译时错误
2. 赋值到unknown类型会触发类型检测
   - unknown类型，赋值操作会触发类型检测
     - 需要进行**类型断言**或者**类型缩小**操作后才能使用。

安全问题

1. any类型可能导致类型安全问题
   - 对于 any类型，任何操作都是允许的
2. unknown类型可以提供更好的类型安全
   - 对于 unknown 类型，需要先进行类型检查或者类型断言

- any类型是TS中最宽松的类型

- unknown类型表示一个未知类型的值
  - **强制**在使用它时先进行**显式的类型检查或转换**
    - 从而提高代码的类型安全性



# TypeScript - Void类型

- void : 用来指定一个函数是没有返回值的
  - 那么函数的返回值就是void类型
- 默认一个函数没有写任何返回类型
  - 默认返回值的类型就是void类型

手动给函数赋值void,那这个函数就是不可以返回值的

但基于上下文的类型推导（Contextual Typing）

- 推导出返回类型为 void 的时候
  - 并**不会强制函数一定不能返回内容**

# TypeScript - never类型

- never 表示永远不会发生值的类型



# TypeScript - tuple类型

- 元组类型

元组类型和数组类型的区别

- 数组中通常建议存放相同类型的元素
  - 不同类型的元素是不推荐放在同一个数组中
- 元组中每个元素都有自己特性的类型
  - 根据索引值获取到的值可以确定对应的类型；

应用场景

- tuple通常可以作为函数的返回的值
  - 在使用的时候会非常的方便；