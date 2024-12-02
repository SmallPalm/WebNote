iterator : 迭代器

Generator : 生成器



# 什么是迭代器

- 迭代器 , 使用户在容器对象 ( container, 例如链表 或 数组) 遍历访问的对象 
  - 使用该接口无需关心对象的内部实现细节
    - 在各种编程语言中的实现, 迭代器的实现方式各不相同 , 但是基本都有迭代器 : 如Java , Python
- 迭代器的定义 , 我们可以看出来 ,迭代器是帮助我们对某个数据结构进行遍历的对象
- 在JavaScript中, 迭代器也是一个具体的对象, 这个对象需要符合迭代器协议
  - 在迭代器协议定义了产生了一系列值的标准方式 , (无论是有限还是无限个都可以)
  - 在JavaScript中这个标准就是一个特定的next方法
- next方法有如下的要求
  - 一个无参数或者一个参数的函数, 返回一个应当拥有以下两个属性的对象
  - done (返回boolean类型)
    - 如果迭代器可以产生序列中的下一个值 , 就为false
      - 这等价于没有指定done 这个属性
    - 如果迭代器已将序列迭代完毕 则为true ,
      - 这种情况下 , value 是可选的
        - 如果value依然存在, 即为迭代结束返回默认值
    - value
      - 迭代器返回的任何JavaScript值, 
        - done为true时,可省略
          - 因为返回的默认值是undefined

就是里面有一个特定的函数,  有了一个这个函数 [Symbol.iterator]

在这个函数里面做一些操作

这个对象就是一个可迭代对象

但是对象是一个可迭代对象的时候,

 只能是可迭代对象才能用的方法 , 对象也就可以用了

# 可迭代对象

- 它和迭代器是不同的概念
- 当一个对象实现了iterator protocol协议时 , 他就是一个可迭代对象
- 这个对象的要求是必须实现 @@iterator方法 
  - 在代码中我们使用的就是Symbol.iterator访问该属性
- 好处
  - 当一个对象变成一个可迭代对象的时候, 就可以进行某些迭代操作
    - 比如for...of操作时, 其实就会调用它的 @@iterator方法

# 原生迭代器对象

- 事实上我们平时创建的很多原生对象已经实现了可迭代协议
  - 会生成一个可迭代对象的
- String , Array , Map , Set , arguments对象, NodeLise集合



# 可迭代对象的应用

可迭代对象可以被用在

- JavaScript中语法
  - for ..of 
  - 展开语法...
  - yield* (后续学习)
  - 解构赋值
- 创建一些对象
  - new Map
  - new WeakMap
  - new Set
  - new WeakSet
- 方法的调用
  - Promise.all
  - Promise.race
    - Array.from 

# 迭代器的中断

- 迭代器在某些情况下会再没有完全迭代的情况下中断
  - 比如遍历的过程中通过break , return , throw中断了循环操作
  - 比如在解构的时候, 没有解构所有的值
- 这个时候我们想要监听中断的话 , 可以添加return方法





# 生成器

- 生成器是ES6中新增的一种函数控制, 使用的方案
  - 它可以让我们更加灵活的控制函数可以什么时候继续执行. 暂停执行等
- 生成器函数也是一个函数 ,但是和普通函数的区别
  - 生成器函数需要在function的后面加上一个符号 *
  - 生成器函数可以通过yield关键字来控制函数的执行流程
  - 生成器函数的返回值是一个Generator对象
    - **生成器事实上是一种特殊的迭代器**

# 生成器函数的执行

- 生成器函数foo的执行体不会执行,
  - foo函数只会返回一个生成器对象
    - 而是需要调用生成器对象中的next方法才会执行
- 当迭代器的next是会有返回值
  - 很多时候我们不希望生成器的next的返回值是一个undefined
    - 这个时候我们可以通过yield来返回结果
- yield后面的代码, 代表了next调用的返回值

# 生成器传递参数 - next函数

- 函数既然可以暂停来分段执行
  - 那么函数应该是可以传递参数的
    - 分段来传递参数
- 调用next函数 给他传递参数
  - 那么这个参数会作为上一个yield语句的返回值
    - 也就是说我们是为本次函数代码块执行提供了一个值

# 生成器提前结束 - return函数

- 生成器对象调用return函数
  - 就会提前结束当前函数
    - 之后调用next不会继续生成值

# 生成器抛出异常 - throw函数

- 给生成器函数内部抛出异常
  - 抛出异常后我们可以在生成器函数中捕获异常
    - 但是在catch语句中不能继续yield新的值
      - 但是可以在catch语法外使用yield继续执行中断的函数



# 生成器代替迭代器

- 生成器是一种特殊的迭代器
  - 在某些情况我们可以使用生成器来代替迭代器
- 使用yield* 来生产一个可迭代对象
  - 这个时候相当于一种yield的语法糖
    - 只不过会**依次迭代**这个**可迭代对象**
      - **每次迭代其中个一个值**

# 异步迭代器

在 JavaScript 中，异步迭代器（Asynchronous Iterators）用于处理异步数据流。这种迭代器允许你逐步处理异步操作的结果，而不是等待所有操作完成后再处理。

### 异步迭代器的基本概念

异步迭代器是一个对象，它实现了以下两个方法：

- `next()`：返回一个 `Promise`，该 `Promise` 解析为一个对象，该对象有 `value` 和 `done` 属性。`value` 是迭代器返回的值，`done` 是一个布尔值，表示迭代是否完成。
- `[Symbol.asyncIterator]()`：返回异步迭代器本身。

### 示例

以下是一个简单的异步迭代器示例：

```
javascript复制代码async function* asyncGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

(async () => {
  for await (const value of asyncGenerator()) {
    console.log(value); // 输出 1, 2, 3
  }
})();
```

### 解释

1. **创建异步生成器**：`async function*` 用于定义一个异步生成器。异步生成器函数内部可以使用 `yield` 关键字来逐步生成值。
2. **使用 `for await...of` 循环**：`for await...of` 循环用于异步迭代器。它会自动处理 `Promise`，等待每个值的解析，然后继续迭代。

### 异步迭代器的应用

异步迭代器在处理流式数据、延迟加载、或者与 API 的异步交互时非常有用。例如，你可以使用异步迭代器来逐步读取文件内容、处理网络请求等。

### 结合 `async` 和 `await`

异步迭代器通常与 `async` 和 `await` 配合使用，简化异步操作的处理。例如：

```
javascript复制代码async function fetchItems() {
  // 模拟从 API 获取数据
  return new AsyncIterable([
    Promise.resolve('Item 1'),
    Promise.resolve('Item 2'),
    Promise.resolve('Item 3')
  ]);
}

(async () => {
  const asyncIterable = await fetchItems();

  for await (const item of asyncIterable) {
    console.log(item); // 输出 'Item 1', 'Item 2', 'Item 3'
  }
})();
```

### 自定义异步迭代器

你也可以自定义异步迭代器对象。例如：

```
javascript复制代码const asyncIterable = {
  async *[Symbol.asyncIterator]() {
    yield 'a';
    yield 'b';
    yield 'c';
  }
};

(async () => {
  for await (const value of asyncIterable) {
    console.log(value); // 输出 'a', 'b', 'c'
  }
})();
```

这个例子展示了如何自定义一个对象，使其成为异步迭代器。