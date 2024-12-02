# typeof 操作符

确定一个值的基本数据类型 , 返回一个表示数据类型的字符串

```js
typeof 42 // "number"
typeof "Hello" // "string"
typeof true // "boolean"
typeof undefined // "undefined"
typeof null // "object" (这是typeof的一个常见的误解)
typeof [1, 2, 3] // "object"
typeof { key: "value" } // "object"
typeof function() {} // "function"
```

typeof null 返回 “object” 是历史遗留问题, 不是很准确



# Object.prototype.toString

用于获取更详细的数据类型信息

```js
Object.prototype.toString.call(42) // "[object Number]"
Object.prototype.toString.call("Hello") // "[object String]"
Object.prototype.toString.call(true) // "[object Boolean]"
Object.prototype.toString.call(undefined) // "[object Undefined]"
Object.prototype.toString.call([1, 2, 3]) // "[object Array]"
Object.prototype.toString.call({ key: "value" }) // "[object Object]"
object.prototype.toString.call(function() {}) //"[object Function]"
```



# instanceof

用于检查对象是否属于某个类的实例

```js
const obj = {}
obj instanceof Object //true
const arr = []
arr instanceof Array // true
function Person() {}
var person = new Person()
person instanceof Person // true
```



# Array.isArray

用于检查一个对象是否是数组

```js
Array.isArray([1, 2, 3]) // true
Array.isArray("Hello") // false
```

