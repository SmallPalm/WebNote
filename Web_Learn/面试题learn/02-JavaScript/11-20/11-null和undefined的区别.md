# null 和 undefined 区别

## undefined  : 未定义的, 不明确的

当 声明 (statement) 变量 (variable) 但 没有 初始化 变量时 , 此时 变量的值 为 undefined

当 访问对象属性 或 数组元素中 **不存在的属性 或 索引** 时 , 也会返回undefined

当 函数没有返回值时 , 默认返回undefined

如果函数的参数没有转递 或 没有被提供值时, 函数参数的值为undefined

``` js
let x
console.log(x) // undefined

const obj = {}
console.log(obj.property) // undefined
// example: 例子
function exampleFun() {}
console.log(exampleFun()) // undefined

function add(a, b) { return a + b}
console.log(add(2)) // NaN
//非数字（NaN）是指无效数字。所有其他数字都是有效的
```



****

## Null : 无约束力的，无效的

null 是 一个特殊的关键字 , 表示一个空对象指针

null 通常 用于 显式地指示一个变量或属性的值是空的

null 是 一个 赋值的操作 , 用来表示 没有值 或 空

null 通常需要主动 赋值 给 变量, 而不是 自动分配的默认值

null 是 原型链的 顶层

所以对象 都继承自 Object 原型对象, Object 原型对象 的原型 是 null

```js
const a = null
console.log(a) // null

const obj = { a: 1 }
const proto = obj.__proto__
console.log(proto.__proto__) // null
```

