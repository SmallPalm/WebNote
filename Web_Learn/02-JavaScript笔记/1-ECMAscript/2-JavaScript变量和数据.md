# JavaScript的变量

- 存放数据的容器
- 独特之处在于它存放的数据是可以变换的

- 变量的声明
  - var 就是关键字 , 就是给JS引擎沟通的桥梁
- 给变量赋值
  - var  变量名 =  “赋值”

**不使用关键字来声明变量的,  会被添加到window对象上 , 但是也可以声明变量 , 不推荐**

## JavaScript的数据类型

- JavaScript中的值都具有特定的类型
  - 将值赋值给变量 ,  那变量就变成了一个特殊的数据类型
  - 一个变量中可以在前一刻存储一个字符串类型(string)  , 下一刻就可以变化成一个数字类型(num)
  - 允许这种操作的编程语言  被称为**动态类型** 的编程语言
- 基本 的数据类型
  - Number  :  数字类型 
  - String  :   字符串类型
  - Boolean  :  布尔类型
  - Undefined：未定义
  - Null ： 空
  - Object : 对象 
  - Bigint
  - Symbol



## typeof操作符 

不是一个函数

- 因为ES（num）系统是比较松散的 ，所有需要一种手段来确定任意变量的数据类型

  - 就是一个变量定义

  - ```html
    var info =  “egjroib“
    info = 120
    info = []
    info = {}
    ```

  - 这样识别确定不了info是什么类型

- 对一个值使用typeof 操作符会返回下列字符串之一 （能够确定变量是什么类型）

  - ```html
    consolg.log( typeof info)
    ```


## Number类型

- Number类型代表整数类型和浮点数类型（小数点）
- Number类型可以做数字计算 ， 操作运算符
- Number类型可以表示**进制**
  - 十六进制用 0x （后面跟数字）
  - 八进制用 0o （后面跟数字）
  - 二进制用0b （后面跟数字）

# String类型 

- String类型代表的是字符串类型 
  - 表示的时候可以用
    - 单引号
    - 双引号
    - 反引号 （``）
      - 反引号是可以拼接字符串的，
      - 可以写${} 
      - 字符串可以拼接对象， 和一些变量
  - 字符串的转移字符
    - 需要在符号的前面的添加/
- 字符串的拼接 
- 获取字符串的长度
  - .length

### Boolean类型

- 表示真假
- true / false

### Undefined类型

- 特殊值 表示空值

## Object类型

- 特殊类型  通常称为引用类型或者复杂类型

- ```html
  var info={
  name:"limingyu"
  age:"10"
  height:"190"
  }
  ```

- 其他数据类型通常称为 **原始类型** 因为他们 的值就包含一个单独 的内容

- Object 往往可以 表示一组数据 ，  是其他数据的一个集合

- 在JavaScript中可以使用花括号{}的方式来表示一个对象

- object是对象的意思

## Null类型

- 表示一个对象为空
- 通常做为对对象做初始化  会赋值Null
- 和Undefined的关系
  - Undefined是一个变量声明但是没有初始化
  - Null是一个变量 保持一个对象 ，但不确定时 ， 可以先赋值为Null
- 其他类型的初始化 是Null  Boolean为false
- 但当对象{} 的初始化时  Boolean为true
  - 但是这个空对象是占据缓存的 ，就是空数值他也是存在的
  - 其他类型为Null是 0x0  不占据缓存的
- Null存在的意义就是对 对象进行初始化的 ，并且在装成Boolean类型 会自动转成false

## 转换数据

```html
log(Numder(undefined))  //NaN
log(Numder(true))  // 1
log(Numder(false)) // 0
log(Numder (null)) // 0
log(Numder("abc123")) //NaN
log(Numder("")) //0
```

