# 认识对象的原型

- 原型有什么用
  - 当我们通过**[[get]]**方法获取一个属性对应的value时
    1. 他会优先在自己的对象中查找 , 如果找到直接返回
    2. 如果没有返回 , 那么会再原型对象中查找



- JavaScript当中每个对象都有一个特殊的内存属性[[prototype]]
  - 这个特殊的对象也可以指向另一个对象
- 这个对象的用处
  - 当我们通过引用对象的属性key来获取一个value时
    - 他会触发Get的操作
  - 这个操作会首先检查该对象是否有对应的属性
    - 如果有就使用它
  - 如果对象中没有该属性 , 那么会访问对象[[prototype]]内置属性中指向的对象上的属性
- 只要是对象都会有这样一个内置属性



**获取方法**

- 通过对象的__proto__属性可以获取到
  - 但这个是早期浏览器自己添加上去的
    - 存在一定的兼容性问题
- 通过Object.getprototypeOf方法可以获取到



# 函数的原型prototype

- 所用的函数都有一个prototype的属性(注意 :  不是_proto_)
- 将函数看成是一个普通的对象时,它是具备__proto __   (隐式原型)
  - 查找key对应的value时 , 会找到原型身上
- 将函数看成是一个函数时 , 它是具备prototype    (显示原型)
  - 用来构建对象时, 给对象设置隐式原型的



# new操作符

- 创建空对象
- 将这个空对象赋值给this
- 将函数的显示原型赋值给这个对象作为它的隐式原型
- 执行函数体中的代码
- 将这个对象默认返回



## 函数原型prototype的属性

- 事实上函数原型对象上面是有一个属性的 : **constructor**
- 默认情况下原型上都会添加一个属性叫做 constructor 
  - 这个constructor指向函数对象



## 重写原型对象

- 如果我们需要再原型上添加过多的属性
  - 通常我们会重写整个原型对象



# 原型链概念

每个 JavaScript 对象都有一个内部链接到另一个对象的链接，这个链接就是原型（prototype）。这个另一个对象也有自己的原型，形成一个链条，称为原型链。对象的 `__proto__` 属性（或在 ES6 中，`Object.getPrototypeOf` 方法）指向它的原型。

```js
// 创建一个对象
const person = {
  name: 'Alice',
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

// 创建另一个对象，继承 person
const student = Object.create(person);
student.study = function() {
  console.log('I am studying');
};

console.log(student.name); // Alice
student.greet(); // Hello, my name is Alice
student.study(); // I am studying


// 在这个示例中：

// student 对象通过 Object.create(person) 创建，继承了 person 对象。
// 当访问 student.name 时，student 本身没有 name 属性，所以 JavaScript 沿着原型链查找，在 person 对象上找到了 name 属性。
// student.greet() 方法也是沿着原型链在 person 对象上找到的。
```

#### 内置对象和原型链

所有的 JavaScript 对象最终都会继承自 `Object.prototype`，这是原型链的顶端。



### 原型链的查找过程

当访问对象的属性时，JavaScript 引擎会执行以下步骤：

1. 检查对象本身是否有该属性。
2. 如果没有，则检查对象的原型（即 `__proto__`）。
3. 继续沿着原型链向上查找，直到找到该属性或到达原型链的顶端（`null`）。
4. 如果最终没有找到该属性，则返回 `undefined`。



### 总结

- 原型链是 JavaScript 对象继承机制的基础。
- 对象可以通过原型链继承属性和方法。
- 查找属性时，JavaScript 引擎会沿着原型链逐级查找，直到找到该属性或到达 `null`。



# 创建原型链

```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const student = new Person('Bob');
console.log(student.name); // Bob
student.greet(); // Hello, my name is Bob

```

在这个示例中：

1. `Person` 构造函数用于创建新的对象实例。
2. `Person.prototype.greet` 定义了所有 `Person` 实例共享的方法。
3. `student` 对象实例化自 `Person`，因此继承了 `Person` 的原型方法。
