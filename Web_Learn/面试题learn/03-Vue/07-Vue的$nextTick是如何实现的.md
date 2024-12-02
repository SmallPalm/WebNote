# Vue的$nextTick是如何实现的

1. 当调用this.$nextTick(callback)时，会将 回调函数存储在一个队列中，以便稍后执行
2. 当检查当前是否正在进行DOM更新周期。如果是，它会将CallBack函数推到一个专门用于**在更新周期结束后执行的队列中**
3. 如果当前不再DOM更新周期中，Vue.js会使用Javascript的Promise或者MutationObserver，这具体取决于浏览器的支持情况，来创建一个微任务（microtask）
4. 微任务是Javascript引擎在执行栈清空后立即执行的任务。因此，回调函数会在下一个微任务中被执行，这确保了它在下一次DOM更新周期之前执行
5. 一旦当前的执行者清空，JavaScript引擎就会检查并执行微任务队列中的任务，其中包括$nextTick的回调函数





# $nextTick

`$nextTick` 是一个非常有用的实例方法，它允许你在下次 DOM 更新循环之后执行代码。

这通常用于在 DOM 更新后立即执行某些操作，比如在数据变化之后立即获取更新后的 DOM 元素的尺寸或位置。

## 原理

`$nextTick` 的工作原理基于 JavaScript 的异步更新队列。Vue 在检测到数据变化时，不会立即更新 DOM，而是将所有数据变化放入一个异步队列。在同一事件循环中，如果多次更改数据，Vue 会将这些更改合并，从而避免不必要的计算和 DOM 更新。然后，在下一个事件循环“tick”中，Vue 刷新队列并更新 DOM。



## 运行方式

1. **数据变化**：当你更改 Vue 实例的数据时，Vue 会将这些变化放入异步队列。
2. **调用 `$nextTick`**：你可以在数据变化后立即调用 `$nextTick` 方法。这会将一个回调函数放入下一个事件循环的队列中。
3. **事件循环**：浏览器的事件循环会处理所有的异步任务。在当前事件循环结束时，Vue 会清空异步队列并更新 DOM。
4. **执行回调**：一旦 DOM 更新完成，`$nextTick` 的回调函数就会被调用。这时，你可以安全地访问更新后的 DOM，或者执行依赖于 DOM 更新的任何操作。

### 示例代码

```vue
<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello'
  },
  methods: {
    updateMessage: function() {
      this.message = 'Updated';
      this.$nextTick(function () {
        // 这个回调将在 DOM 更新后执行
        console.log('The message has been updated to: ' + this.message);
      });
    }
  }
});
  
 //在这个例子中，当 updateMessage 方法被调用时，message 数据会更新。然后，$nextTick 确保回调函数在 DOM 更新后执行。
</script>


```

## 使用场景

- **获取更新后的 DOM 元素**：在 DOM 更新后立即获取元素的尺寸或位置。
- **执行依赖于 DOM 更新的操作**：例如，滚动到页面的某个位置，或者在 DOM 更新后立即触发某个动画。
- **避免不必要的计算**：如果你在数据变化后立即执行某些操作，而这些操作依赖于 DOM 的更新，使用 `$nextTick` 可以避免在 DOM 未更新时进行这些操作。





