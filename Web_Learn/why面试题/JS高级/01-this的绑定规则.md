# this绑定

#### 1. 默认绑定

独立函数调用，函数没有被绑定到某个对象上进行调用

- this指向window
- 严格模式下，this指向undefined

#### 2. 隐式绑定

通过某个对象发起的函数调用，在调用对象内部有一个对函数的引用

- this指向发起调用的对象

#### 3. 显示绑定

明确this指向的对象，第一个参数相同并要求传入一个对象

#### 4. new绑定

- 创建空对象
- this绑定到创建的空对象中
- 将函数的显示原型赋值给这个对象作为它的隐式原型
- 执行函数体中的代码
- 将这个对象默认返回





# 显示绑定细节显示绑定是指通过 `call`、`apply` 和 `bind` 方法手动指定函数中的 `this` 指向。以下是 `call`、`apply` 和 `bind` 这三个方法的区别：

### 1. **`call` 方法**

- **功能**: 立即调用函数，并显式指定 `this` 的值和参数。
- **参数**: 第一个参数是 `this` 的值，后续参数是传递给函数的参数。
- **返回值**: 函数执行的结果。

**示例**:

```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Alice' };

greet.call(person, 'Hello', '!'); // 立即调用，输出: "Hello, Alice!"
```

### 2. **`apply` 方法**

- **功能**: 与 `call` 类似，立即调用函数并显式指定 `this` 的值。
- **参数**: 第一个参数是 `this` 的值，第二个参数是一个包含传递给函数的参数的数组或类数组对象。
- **返回值**: 函数执行的结果。

**示例**:

```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Bob' };

greet.apply(person, ['Hi', '.']); // 立即调用，输出: "Hi, Bob."
```

### 3. **`bind` 方法**

- **功能**: 不立即调用函数，而是返回一个新的函数，`this` 的值永久绑定到指定的对象。返回的新函数可以在稍后调用。
- **参数**: 第一个参数是 `this` 的值，后续参数是传递给新函数的参数。
- **返回值**: 绑定了指定 `this` 值的新函数。

**示例**:

```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Charlie' };

const boundGreet = greet.bind(person, 'Hey'); // 返回一个新函数
boundGreet('!'); // 需要调用才会执行，输出: "Hey, Charlie!"
```

### **总结**：

1. **调用时间**:
   - `call` 和 `apply`: 立即调用函数。
   - `bind`: 返回一个新的绑定函数，需要手动调用。
2. **参数传递**:
   - `call`: 参数按顺序逐个传递。
   - `apply`: 参数作为数组传递。
   - `bind`: 参数可以在绑定时传递（预设参数），也可以在调用时传递。
3. **用法场景**:
   - 使用 `call` 和 `apply` 立即执行需要指定 `this` 的函数。
   - 使用 `bind` 延迟执行或者在需要保存 `this` 绑定的场合