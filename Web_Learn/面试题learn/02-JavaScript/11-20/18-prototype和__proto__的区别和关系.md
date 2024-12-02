# Prototype和\_\_proto\__的区别

## Prototype

函数对象 (构造函数) 特有的属性

每个函数对象都是一个Prototype属性，Prototype是有一个对象

通常用于定义共享的属性和方法，可以**被构造函数创建的实例对象所继承**。

可以在构造函数的prototype上定义方法，以便多个实例对象共享这些方法，从而节省内存

主要用于原型继承，prototype是构造函数和实例对象之间的链接，用于共享方法和属性







## ——Proto——

每个对象（包括函数对象和普通对象）都具有的\_\_pro__属性

\_\_proto__指向对象的原型，也就是它的父对象

\_\_proto\_\_用于实现原型链，当访问一个对象的属性时，如果对象本身没有这个属性，JavaScript引擎会沿着原型链（通过\_\_proto\_\_属性）向上查找，直到找到属性或到达原型链的顶部（原型链的顶部通常是Object.prototype）

主要用于对象之间的继承，它建立了对象之间的原型关系







# 总结

Prototype和\_\_proto\_\_是不同的

但Prototype和\_\_proto\_\_在JavaScript中一起用于实现原型继承。

构造函数的Prototype对象会被赋予给实例对象的\_\_proto\_\_属性，从而建立了原型链





# 代码

```js
// 创建一个构造函数
function Foo(name) {
  this.name = name;
}

// 在构造函数的Prototype上定义方法
Foo.prototype.setName = function(name) {
  this.name = name;
  console.log("NewName", name)
}

// 创建一个实例对象
const foo1 = new Foo("foo1");

// 访问实例对象的属性和方法
console.log(foo1.name)

foo1.setName("foo2");

console.log(foo1.name);

// __proto__: 访问实例对象的原型, 指向Foo.prototype
console.log(foo1.__proto__ === Foo.prototype) // true
```

## 总结

定义一个构造函数Foo，然后在构造函数的Prototype上定义了一个方法setName。

接着，创建了一个Foo1实例对象，并访问了它的属性和方法。

最后验证了Foo1实例对象的\_\_proto\_\_属性指向构造函数Foo的Prototype对象

建立了原型链的关系