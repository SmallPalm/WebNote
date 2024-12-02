1. 常用方法

Object.keys( obj ).length = 0

JSON.stringify(obj) === “{}”

for in 遍历判断



常用方法处理不了object中Symbol属性的情况

使用严谨方法

Reflect.ownKeys(obj).length === 0

**返回一个包含所有自身属性 (不包含继承属性 ) 的数组**

- **类似于Object.keys()**

因为它能够一次性获取对象的所有属性，包括字符串键和 `Symbol` 键。这样可以准确判断对象是否为空，而不会遗漏任何属性类型。