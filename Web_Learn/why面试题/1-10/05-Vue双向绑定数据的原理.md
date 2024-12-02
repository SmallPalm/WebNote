Vue.js 的双向绑定是通过 `v-model` 指令实现的

它本质上是对数据劫持（data reactivity）和事件监听的语法糖。

在 Vue 中，双向绑定的实现主要依赖于以下几个步骤：

**数据劫持（Data Reactivity）**：

- Vue 使用 `Object.defineProperty` 方法对数据对象的属性进行劫持，从而能够监听到属性的变化。
- 当组件实例被创建时，Vue 会对它的数据对象进行递归遍历，使用 `defineProperty` 将每个属性都转换为 getter/setter。
- 当属性被读取时，getter 函数会被调用；当属性被修改时，setter 函数会被调用。

**依赖收集（Dependency Collection）**：

- 当组件渲染过程中访问到某个数据属性时，Vue 会记录这个属性的依赖（即当前的渲染 watcher）。

- 这样，当数据属性发生变化时，Vue 知道应该通知哪些 watcher 进行更新。

**派发更新（Dispatch Update）**：

- 当数据属性发生变化时，setter 函数会被调用，它会通知 Vue 的依赖系统，触发依赖于该数据的 watcher。

- 这个过程会使得视图重新渲染，确保数据的变更能够反映到界面上。

**事件监听（Event Listening）**：

- 对于 `v-model` 绑定的表单输入元素，Vue 会监听输入事件（如 `input`、`change` 等），并在事件触发时更新绑定的数据。

- 这样，当用户在输入框中输入数据时，Vue 能够实时更新数据，实现双向绑定。

**合成（Synthesized）**：

- Vue 将数据劫持和事件监听结合起来，提供了 `v-model` 指令，使得开发者可以很方便地在模板中实现双向绑定。

举个例子，当你在 Vue 模板中使用 `v-model` 绑定一个输入框时：

html

```html
<input v-model="message">
```

Vue 内部会做以下处理：

- 创建一个计算属性，用于读取 `message` 的值。
- 创建一个 watcher，用于在 `message` 变化时更新 DOM。
- 监听 `input` 事件，当用户输入时，更新 `message` 的值。

这样，`message` 的值和输入框的内容就实现了双向绑定。任何一方的更新都会触发另一方的更新，确保数据的一致性。

需要注意的是，Vue 3 引入了 Composition API 和响应式 API 的新变化，使用了 Proxy 代替了 `defineProperty`，以支持更广泛的数据结构和更高效的依赖追踪。但是，双向绑定的核心原理和实现方式并没有太大变化。