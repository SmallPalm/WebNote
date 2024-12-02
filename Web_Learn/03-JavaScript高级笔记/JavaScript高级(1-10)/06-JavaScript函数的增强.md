# 函数对象的属性

- **name**
  - 一个函数的名词 ,我们可以通过name来访问
- **length**
  -  用于返回函数参数的个数
    - rest参数是不参与参数的个数的
    - rest参数 :  ...args

## arguments

- arguments : 是一个对应于传递给函数的参数的类数组(array - like)对象
- array-like 意味着它不是一个数组类型 ,而是一个对象类型
  - 但是它却拥有数组的一些特性 
    - 比如说length , 数组长度
    - 比如说可以通过index索引来访问
  - 但是它却没有数组的一些方法 
    - 比如filter , map等,  不能使用

## Arguments转Array

- 在开发中, 我们经常需要将arguments转成Array  , 以便使用数组的一些特性
- 转化方式
  1. 遍历arguments，添加到一个新数组中
  2. 调用数组slice函数的call方法
     - slice可以使用空数组调用
     - 也可以使用Array.prototype调用
     - slice函数使用的是this指向
     - slice显示绑定call arguments
     - this指向arguments
  3. 使用Array.from
     1. 直接转换
  4. 使用[...arguments]
     1. 将arguments中的itme 全部添加到一个数组中

- 箭头函数不绑定arguments
  - 在箭头函数中使用arguments会去上层作用域中查找



# 函数的剩余(rest)参数

- ES6中引用了rest parameter , 可以将不定数量的参数(**实参**)放入到一个数组中
- 如果最后一个参数(**形参**)是...为前缀的
- 那么它会将剩余的参数(**实参**)放到该参数(**形参**)中
- 并且作为一个数组

**剩余参数需要写到其他参数的最后**



#### 剩余参数和arguments的区别

- **剩余参数**只包括哪些没有对应形参的实参
  - 而**arguments**对象包含了传给函数的所用实参
- arguments对象不是一个真正的数组
  - 而rest参数(**剩余参数**)是一个真正的数组 , 可以进行数组的所用操作
- arguments是早期的ECMAScript中为了方便去获取所用的参数提供的一个数据结构
  - 而rest参数是ES6中提供并且希望来代替arguments



# 理解JavaScript纯函数

- 函数式编程中有一个非常重要的概念叫做纯函数
  - JavaScript符合函数式编程的范式 , 所以也有纯函数的概念
- 在**react**开发中纯函数是被多次提及的
  - 比如**react**中组件就被要求像是一个纯函数 (为什么是像 ,因为还有**class**组件) ,
    - **redux** 中有一个**reducer**的概念 ,也是要求必须是一个纯函数
- **纯函数不能使用闭包 , 不能使用外层作用域**

#### 维基百科定义

- 在程序设计中 , 若一个函数符合以下条件
  - 那么这个函数被称为纯函数
- 此函数在相同的输入值时,  需产生相同的输出
- 函数的输出和输入值 以外的其他隐藏信息或状态无关 
  - 也和由I/O 设备产生的外部输出无关
- 该函数不能有语义上可观察的函数副作用
  - 比如 : “触发事件” , 使输出设备输出 , 或更改输出值以外物件的内容等
- **总结**
- 确定的输入 ,  一定会产生确定的输出
- 函数在执行过程中, 不能产生**副作用**

### 副作用概念的理解

- 在计算机科学中 , 也引用副作用的概念
- 表示在执行一个函数时 , 除了返回函数值之外, 还对调用函数产生了附加的影响
- 比如修改了全局变量 , 修改参数或者改变外部的存储
- 纯函数在执行的过程中就是不能产生这样的副作用
  - 副作用往往是产生bug的  “温床”

**纯函数可以在确定的输入的时候, 产生确定的输出 , 并且不会修改外层作用域的内容**



## 纯函数的案例

- 数组实参方法
- slice()
  - 纯函数 : 不会修改原数组本身
  - 不会对原数组进行任何修改操作 , 而是生成一个新的数组
- splice
  - 不是纯函数
  - 截取数组 , 会返回一个新的数组 , 也会对原数组进行修改

# 纯函数的作用和优势

- 保证了函数的纯度 , 只是单纯实现自己的业务逻辑即可
  - 不需要关心传入的内容是如何获得的
  - 或者依赖其他的外部变量是否已经发生了修改
- 确定输入的内容不会被任意篡改
  - 并且自己确定的输入 , 一定会有确定的输出
- react中就要求我们无论是函数还是class声明一个组件的时候
  - 这个组件都必须像一个纯函数一样 , 保护他们的props不被修改
- React非常灵活 , 但他也有一个严格的规则
  - 所有React组件都必须像纯函数一样保护它们的props不被修改

# 柯里化概念的理解

- 柯里化也是属于函数式编程里面一个非常重要的概念
  - 这是一种关于函数的高阶技术
  - 它不仅被用于JavaScript , 还被用于其他编程语言

#### 维基百科

- 在计算机科学中 , 柯里化(Currying) 又翻译为 ,卡瑞化 或加里化
- 是把接收多个参数的函数 , 变成接受一个单一参数 ,(最初函数的第一个参数) 的函数 
  - 并且返回接受余下的参数 ,而且返回结果的新函数的技术
- 如果你固定某些参数 , 你将得到接受余下参数的一个函数

#### 总结

- 只传递给函数一部分参数来调用它 , 让它返回一个函数去处理剩余的参数
- 这个过程就称之为柯里化
- 柯里化是一种函数的转换
  - 将一个函数从可调用的foo(a,b,c) 转换为可调用的foo(a)(b)(c)
  - 柯里化不会调用函数  他只是对函数进行转换 

```js
//普通函数
function foo(x, y, z){
console.log(x, y, z)
}
foo(10, 20 ,30)
//这个转换的过程叫做柯里化
//柯里化处理函数
function foo(x){
  return function(y){
    return function(z){
      console.log(x, y, z)
    }
  }
}

foo(10)(20)(30)


//箭头函数:柯里化写法
var foo = x {
  return y =>{
    return x =>{ 
      console.log(x, y, z)
    }
  }
}

//一行代码优化
//一行代码, 作为这行表达式的返回值
var foo = x => y => z=> console.log(x, y, z)
```



# 柯里化高级 - 自动柯里化函数

- 函数封装

```js
    function foo(x, y, z) {
      console.log(x + y + z)
    }
    function sum(sum1, sum2) {
      return sum1 + sum2
    }

    function loginfo(data, type, message) {
      console.log(`时间${data},类型${type},内容${message}`)
    }
    function Currying(fn) {
      function curry(...args) {

        if (args.length >= fn.length) {
            fn(...args)
          } else {
          return function (...Newargs) {
            return curry(...args.concat(Newargs))
          }
        }
      }

      return curry
    }

    var fooCurry = Currying(foo)
    fooCurry(12)(10)(22)
```





# 组合函数

- 组合函数是在JavaScript开发过程中一种对函数的使用技巧, 模式:
- 过程
- 现在需要对某一个数据进行函数的调用 , 执行两个函数fn1和fn2
  - 这两个函数依次执行
- 如果我们每次都需要进行两个函数的调用
  - 操作上就会显得重复
- 那么可以将这两个函数组合起来 , 自动依次调用
- 这个过程就是对函数的组合
  - 称之为组合函数

#### 组合函数封装

```js
    function double(num) {
      return num * 2
    }
    function pow(num) {
      return num ** 2
    }

    function composeFn(...fns) {
      // 边界判断
      var length = fns.length
      if (length <= 0) return
      for (var i = 0; i < length; i++) {
        var fn = fns[i]
        if (typeof fn !== "function") {
          throw new Error(`组合函数中${i}不是一个function`)
        }
      }

      return function (...args) {
        var result = fns[0].apply(this, args)

        for (var i = 0; i < length; i++) {
          var fn = fns[i]
          result = fn.apply(this, [result])
        }

        return result
      }
    }

    var newFn = composeFn(double, pow)
    console.log(newFn(100))
```

## with语句的使用

- 扩展作用域链

- 不建议使用 , 容易混淆视听和兼容性问题

- ```js
  with(){
    
  }
  ```



## eval函数

- 内建函数eval允许执行一个代码字符串
  - eval是一个特殊函数
    - 他可以将传入的字符串当做JavaScript代码来运行
  - eval会将最后一句执行语句的结果 , 作为返回值
- 不建议开发中使用eval
  - 可读性非常的差
  - 是一个字符串 , 容易在执行的过程中被刻意篡改
  - 必须经过JavaScript解释器 , 不能被JavaScript引擎优化

​	
