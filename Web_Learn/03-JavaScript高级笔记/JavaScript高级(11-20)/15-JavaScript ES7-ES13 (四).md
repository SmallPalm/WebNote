# ES7

### Array includes

- 在ES7之前
  - 如果我们想判断一个数组中是否包含某个元素
    - 需要通过 indexOf 获取结果，并且判断是否为 -1。
- 在ES7中
  - 我们可以通过includes来判断一个数组中是否包含一个指定的元素
    - 根据情况，如果包含则返回 true，否则返回false

### ****** 运算符

- ES7之前，计算数字的乘方需要通过 Math.pow() 方法来完成

- 可以对数字来计算乘方

# ES8

### **Object . values**

- 之前我们可以通过Object. keys 获取一个对象所有的key
- ES8中提供了 Object . values 来获取所有的value值

### **Object . entries**

- 通过Object . entries 可以获取到一个数组 
  - 数组中会存放可枚举属性的键值对数组
- 可以针对 对象, 数组, 字符串进行操作

### **PadStart / PadEnd**

- 对字符串需要对其进行前后填充
  - 来实现某些格式化的效果



# ES10

### Flat

- 将一个数组, 按照制定的深度 , 递归遍历数组 , 
  - 并将所有元素与遍历到的子数组中的元素合并成为一个新数组

### FlatMap

- 首先使用映射每一个元素 , 然后将结果压缩成一个新数组
  - FlatMap 是先进行Map操作, 在做Flat操作
  - FlatMap 中的Flat相当于深度为1

### Object FromEntries

- 跟Entries 是对应的
  - 完成转换
- 也可以转换URLSearchParams

### trim

- 去除字符串首尾的空格
- trimStart
- trimEnd



# ES11

### Bigint

- 在早期的JavaScript中, 我们不能正确的表示过大的数字
  - 大于 MAX_SAFE_INTEGER的数值, 表示的可能是不正确的
- 引入新的数据类型 , BigInt 用于表示大的整数

- Bigint 的表示方法 是在数值的最后添加一个n

### Nullish Coalescing Operator

- 增加了空值合并操作符
  - ?? : 空值合并操作符

### Optional Chaining

**可选链** 

- 当我们在一个对象里面去掉调用函数时
  - 如果当前函数里面没当前该函数，
    - 那将不会往下进行
- 主要作用是让我们的代码在进行null和undefined判断时更加清晰和简洁



### for in 标准化

- 在ES11之前，
  - 虽然很多浏览器支持for...in来遍历对象类型
    - 但是并没有被ECMA标准化。
- 在ES11中
  - 对其进行了标准化
    - for...in是用于**遍历对象的key**的



# ES12

### FinalizationRegistry

- FinalizationRegistry 对象可以让你再 , 对象被垃圾回收时 请求一个回调
  - FinalizationRegistry 提供了一种方法 
    - 当一个在注册表中注册的对象被回收时, 请求在某个时间点上调用一个清理回调 
      - 清理回调称之为 finalizer
- 可以调用=register方法 , 注册任何你想要清理的回调的对象 , 传入该对象和所含的值

### WeakRef

- 如果我们默认将一个对象赋值给 另一个引用, 那么这个引用是一个强引用

  - 如果我们希望是一个弱引用 , 可以使用WeakRef

  - ```js
    let obj = {name:"linmingfyu"}
    let info = new WeakRef(obj) //弱引用
    ```



### 逻辑运算符简写

```js
let message = message + "leqw"
let message += "leqw"

let message = message || "hello world"
let message ||= "Hello world"

let message = message ?? "默认值"
let message ??= "默认值"

let obj = {
  name:"limingyu"
}
let obj = obj && obj.name
let obj &&= obj.name
```

### String.replaceAll

- 字符串替换全部

- ```js
      const string = " lk , le ,li ,li ,lk"
      const st2 = string.replace("lk", "limngyu")
      const st23 = string.replaceAll("li", "limingyu")
  ```



# ES13

### .at()

- 通过索引, 打印索引所对应的值
- 数组 和 字符串

### Object.hasOwn

- Object新增静态方法 ( 类方法)
  - 用于判断一个对象中是否有某个自己的属性
- 跟Object.prototype.hasOwnProperty区别
  - 官方解释 :  代替
- 区别
  - 防止对象内部有重写hasOwnProperty
  - 对于隐式原型指向null的对象, hasOwnProperty无法进行判断

### class类中新字段

- 实例公共字段 : Instance public fields
  - 实例私有字段 : Instance private fields

-  类属性 (Static)
  - 静态公共字段 : Static public fields
  - 静态私有字段 :  static private fields
- 静态块 : static block
  - 等到加载解析 当前class 类 的时候  , 就会执行对应的静态代码块
    - 而且只会执行一次
  - 只会在第一次代码执行是加载出来
  - 一般情况下对class 类 做一些初始化的操作时 , 使用静态
