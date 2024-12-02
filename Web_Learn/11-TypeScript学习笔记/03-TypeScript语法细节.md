# 联合类型

- TS的类型系统允许我们使用多种运算符, 从 **现有类型中构建新类型**

第一种组合类型 : 联合类型

- 联合类型是由两个或多个其他类型组成的类型
  - 可以是其他类型组成的类型中的其中任何一个值
- 联合类型中的每一个类型被称之为联合成员

- ```TSX
  function foo(id: string|number){
      
      // 我们需要使用缩小（narrow）联合
      // TypeScript可以根据我们缩小的代码结构，推断出更加具体的类型；
  
      if(typeof id === "string"){
          string类型
      }else if(typeof id === "number"){
          number类型
      }
  }
  
  foo("123")
  foo(456)
  ```



# 类型别名

- 给编写的对象类型和联合类型
  - 一个别名
- 可以在多个地方进行复用

- ```tsx
  type point = {
      x: number,
      y: number
  }
  
  type ID = number|string
  ```



# 接口声明

- 编写的对象类型
  - 另一种声明方式就是通过接口来声明Value的类型的



# type和interface的区别

- 类型别名和接口interface非常相似
  - 在定义对象类型时, 大部分时候
    - 可以任意选择使用
- 接口interface的几乎所有特性都可以在type中使用

选择

- 如果是定义非对象类型

  - 通常使用Type
  - 如: Direction Alignment Function

- 定义对象类型时, interface和Type的区别

  - interface可以重复的对某个接口来定义属性和方法

  - type定义的是别名

    - 别名是不能重复的

  - ```tsx
    // 可以重复
    interface idPerson{
        
    }
    
    interface idPerson{
        
    }
    // 不可以重复, 在TS中会报错
    type person{
    
    }
    type person{
    
    }
    ```

# 交叉类型

- 联合类型是满足其中一个类型即可

- 交叉类型是需要满足多个类型

  - 使用&符号

- ```tsx
  type alignment = number & string
  ```

  - 表示的含义是number和string要同时满足

- 同时满足是一个number又是一个string的值吗

  - 其实是没有的，所以alignment其实是一个never类型

## 交叉类型的应用

- 在开发中, 我们使用交叉类型时, 通常是对对象类型进行交叉的

- ```tsx
  interface Colorful {
      color:string
  }
  
  interface IRun {
      running:() => {}
  }
  
  type NewType = Colorful & IRun
  
  const obj: NewType = {
      color : "red",
      running: function() {}
  }
  ```



# 类型断言as

- 有时候TypeScript无法获取具体的类型信息
  - 这个我们需要使用类型断言 (Type Assertions)





# 字面量类型

- 字面量类型: literal types

- ```tsx
  let message : "Hello" = "Hello"
  ```

- 默认情况下这么做是没有什太大意义的

  - 但是我们可以将多个类型联合在一起

- ```tsx
  type Alignment = 'left' | 'right' | 'center'
  
  function changeAlign(align: Alignment) {
      console.log(align)
  }
  
  changeAlign("left")
  ```





# 类型缩小

- 什么是类型缩小
  - 类型缩小的英文Type Narrowing
  - 类似于typeof count === 'number' 的判断语句
    - 用来改变TypeScript的执行路径
  - typeof count === 'number' 可以称之为类型保护
- typeof
- 平等缩小
- instanceof
- in 操作符

## Typeof

- ```tsx
  type Id = number | string
  
  function foo(id: Id) {
      if(typeof id === string){
          id.toUpperCase()
      }else if(typeof id === number) {
          id.toString()
      }
  }
  ```

## in操作符

- ```tsx
  type Fish = {swim: () => void}
  type Dog = {run: () => void}
  
  function move(animal: Fish | Dog) {
    	// 判断swin是否是那个类型的方法  
      if( 'swin' in animal){
  		animal.swin()
      }else{
          animal.run()
      }
  }
  ```



# TypeScript函数类型

- 在使用函数的过程中, 函数有参数类型, 有返回值类型, 也有函数本身的自己的类型

- 可以编写函数类型的表达式

  - 表达式: Function Type Expression
  - 来表示函数类型

- ```tsx
  type CalcFn = (n1: number, n2: number) => number
  
  function Calc(fn: Calcfn) {
      return fn(10, 20)
  }
  
  
  function sum(n1, n2){
      return n1 + n2
  }
  Calc(sum)
  ```



# TypeScript函数类型解析

- (n1: number, n2: number) => void 表示一个函数的类型
- TypeScript的参数名不可以省略



# 调用签名

- 调用签名 : Call Signatures

- 函数除了可以调用, 也可以有自己的属性值

- 函数类型表达式 不支持 声明属性值

- 但可以在对象类型中写一个调用签名

  - 跟函数类型表达式不相同的写法
  - 注意这个语法跟函数类型表达式稍有不同
    - 在参数列表和返回的类型之间用的是 : 而不是 =>

  ```TS
  interface ICalcFn {
    name: string
    (n1: number, n2: number): void
  }
    
    function calc(calcFn: ICalcFn) {
      // 函数中有自己的属性值, 也可以调用使用  
      calcFn.name
      calcFn(10, 20)
    }
  ```



# 构造签名

- JavaScript函数也可以使用new 操作符调用

  - 当被调用的时候
  - TypeScript会认为这是一个构造函数(constructor)
    - 因为new 会产生一个新对象

- ```ts
  interface IPerson {
    new(name: string) : Person
  }
  
  calss Person {
    name:string
    constructor(name: string){
      this.name = name
    }
  }
  
  function factory(ctor: IPerson) {
    return new ctor("liming")
  }
  
  factory(person)
  ```



# 函数参数的可选类型

- 可以执行函数中的某一个传参是可选的

  - 可选类型的参数需要在必选参数的后面

- ```ts
  function foo(x: number, y?:number){}
  foo(10)
  foo(29,39)
  ```

- 如果可选参数不传入值, 那么可选参数的类型是 undefined类型

  - 可选参数? : number | undefined

# 默认参数

-  从ES6开始, JavaScript是支持默认参数值的

  - TypeScript也支持默认参数值的

  ```ts
  function foo(x: number, y: number = 65) {}
  foo(10, 29)
  // number | undefined
  foo(10)
  ```

# 剩余参数

- ES6开始的, JavaScript支持剩余参数
  - 剩余参数语法允许我们将一个**不定数量的参数放到一个数组**中

```ts
function foo(...nums: number[]) {}
function bar(...object: string | number | any[]){}
function ber(...agms: object | undefined[])
```



# 函数重载

- 在TypeScript中, 我们可以去编写不同的重载签名(overload signatures)
  - 来表示函数可以以不同的方式来进行调用
  - 一般是编写两个或者以上的重载签名
    - 在编写一个通用的函数以及实现

```ts
function sum(a1: number, a2: number): number
function sum(a1: string, a2: string): string
function sun(a1: any, a2: any): any {
  return a1 + a2
}
```

- 方法重载 : 简单封装一个数组
  - 使数组更加好用,通过index删除返回index,通过object删除返回object

```ts
class ArrayEN {
  constructor(public arr: object[]) {}
  
  get(Index: number){
    return this.arr[Index]
  }
  
  delete(value: number): number
  delete(value: object): object
  delete(value: number | object): number | object {
    this.arr = this.arr.filter((item, index) => {
      if (typeof value === "number") {
        return value !== index;
      } else {
        return value !== item;
      }
    });
    return value;
  }
}
```

- 构造器重载 : 一个图片的面积

  - 这个图形可能是传参可以是对象也可能是长宽

  ```ts
  interface OJType{
      width?:number,
      height?:number
  }
  class Graph{
      public width:number;
      public height:number;
  
      constructor(width?:number,height?:number)
      constructor(side?:OJType)
      constructor(v1:any,v2?:any){
          if(typeof v1==='object'){
              this.width=v1.width;
              this.height=v1.height
          }else{
              this.width=v1;
              this.height=v2;
          }
      }
  
      getArea(){
          const {width,height}=this;
          return width*height
      }
  }
  
  const g=new Graph(10,10);
  console.log(g.getArea())
  ```



# 可推导的this类型

- Vue3的Composition API中很少见到this
  - Composition API主要通过函数来组织逻辑，而不是类方法
    - 在这种情况下，`this`并不是必需的
      - 因为函数中的状态和方法可以通过闭包或直接返回来实现。
- React的Hooks开发中也很少见到this了
  - React Hooks设计用于函数组件，函数组件本身没有`this`的概念
    - 状态和副作用通过Hook管理，而不是类的方法。
  - Hooks避免了类组件中的`this`绑定问题
  - 以前在类组件中，开发者需要显式绑定`this`
    - 例如在构造函数中使用`this.method = this.method.bind(this)`
  - Hooks通过闭包的方式消除了这种需求，使代码更简洁。

## 总结

- ​	
- **避免上下文绑定问题**：消除了类组件中的`this`绑定问题，使代码更直观和简洁。
