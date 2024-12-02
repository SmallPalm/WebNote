ForEach和Map都是JavaScript中用于数组迭代的两个不同的数组方法

**forEach**

- 对数组的每个元素执行一次提供的函数
- 没有返回值, 即返回undefined
- 不能被中断, 即使在回调函数中抛出错误, 它也会继续处理数组的其余元素
- 不支持数组的链式调用

**map**：

- `map` 方法创建一个新数组，其结果是原数组中的每个元素都调用一次提供的函数后的返回值。
- `map` 返回一个新数组，不修改原数组。
- `map` 可以被中断，如果在回调函数中返回 `undefined`，则新数组在该位置的元素也会是 `undefined`。
- `map` 支持链式调用，可以在其返回的新数组上继续调用其他数组方法。

# **使用场景**

- 当你需要对数组的每个元素执行某些操作，并且不关心结果时，可以使用 `forEach`。
- 当你需要对数组的每个元素执行操作，并且需要将结果作为新数组返回时，应该使用 `map`。



```js
let numbers = [1, 2, 3, 4];

// 使用 forEach 打印数组的每个元素
numbers.forEach(function(number) {
  console.log(number);
});

// 使用 map 创建一个新数组，其中包含原数组每个元素的平方
let squares = numbers.map(function(number) {
  return number * number;
});
console.log(squares); // 输出: [1, 4, 9, 16]
```

