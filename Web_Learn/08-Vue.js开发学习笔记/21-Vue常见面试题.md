# 1.vue基础

Vue是用于构建用户界面的**渐进式**JavaScript框架

基于HTML，CSS和JavaScript构建，并提供了一套声明式，组件化的编程模型



## 1.1. Vue.js的Characteristic

Characteristic：特点，特征

- 易用：Vue.js是一个渐进式框架，相比于其他框架，更简单，易学，上手快
- 灵活：可以在一个库和一套完整的框架之间自如伸缩
- 高效：虚拟DOM，省心的优化
- 双向绑定：开发效率高
- 项目工程化



## 1.2. 什么是MVVM

MVC和MVVM都是一种软件的体系结构

- MVC是Model - View - Controller 的简称
- MVVM是 Model - View - ViewModel 的简称

通常称Vue是一个MVVM的框架

但官方说， Vue并没有遵守MVVM的模型，但整个设计是受到MVVM的启发

**MVVM：**

1. **Model（模型）**：代表应用程序的数据和业务逻辑。
2. **View（视图）**：用户界面，用于展示数据和接收用户输入。
3. **ViewModel（视图模型）**：作为Model和View之间的中介，负责业务逻辑的处理，并将数据从Model传递到View，同时处理用户在View上的交互。

MVVM模式通过**数据绑定技术**，使得View的变化自动反映在ViewModel上，反之亦然，从而实现了双向绑定。

**MVC**：

1. **Model**：负责业务逻辑和数据管理。
2. **View**：负责显示数据（模型）和接收用户指令，不包含业务逻辑。
3. **Controller**：作为View和Model之间的中介，接收用户的输入并调用模型和视图进行相应的处理。
   - 当Model改变时，通常需要Controller显式地更新View。



## 1.3. SPA页面的理解，优缺点是什么

- SPA：Single Page Application

在Web页面 **initialize** 时加载 相应的HTML ，Javascript和CSS。

- 一旦页面加载完成，SPA不会因为用户的操作而进行重新加载页面或跳转
- 取而代之是利用路由机制实现HTML的内部变换
  - UI 与 用户的交互，避免页面重新加载

优点

- 用户体验好，快，内容的改变不需要重新加载整个页面，避免不必要的跳转和重复渲染
- SPA相对 对 Server 的 压力小
- 前后端职责分离，架构清晰

缺点

- 首次加载耗时多：为实现单页面Web应用功能及显示效果，需要在加载页面的时候将HTML，Javascript，CSS统一加载，部分页面按需引入加载
- 前进后退路由管理：由于单⻚应⽤在⼀个⻚⾯中显示所有的内容，所以不能使⽤浏览器的前进后退 功能，所有的页面切换需要⾃⼰建⽴堆栈管理
- SEO难度较大：由于所有的内容都在一个页面中动态替换显示，所以在SEO上其有着天然的弱势



## 1.4. v-show和v-if的区别

用法上区别

v-show不能用来template标签中

本质的区别

v-show元素无论是否需要显示到浏览器上

- 它的DOM实际都是有存在的，只是通过CSS的display属性来进行切换

v-if当条件为false时

- 对应的DOM根本不会渲染到DOM中

开发中如何进⾏选择呢

- 如果我们的原⽣需要在显示和隐藏之间频繁的切换，那么使⽤v-show
- 如果不会频繁的发⽣切换，那么使⽤v-if；





## 1.5. 数组中那些方法会触发视图的更新

Vue将监听的数组的变更方法进行了包裹

所以它们也将会处触发视图更新

- push()
  - **作用**：向数组末尾添加一个或多个元素，并返回新数组的长度。
- pop()
  - **作用**：删除数组末尾的元素，并返回该元素。若数组为空，则返回 `undefined`
- shift()
  - **作用**：删除数组开头的元素，并返回该元素。若数组为空，则返回 `undefined`。
- unshift()
  - **作用**：向数组开头添加一个或多个元素，并返回新数组的长度。
- splice()：直接修改数组
  - **作用**：可以添加、删除或替换数组中的元素。返回被删除的元素。
  - **用法**：`array.splice(start, deleteCount, item1, item2, ...)`
- sort()
  - **作用**：对数组中的元素进行排序，默认按字符编码顺序排序。
- reverse()
  - **作用**：反转数组中的元素顺序。

其它数组的⽅法: 

- 但是某些⽅法不会替换原来的数组，⽽是会⽣成新的数组
- ⽐如 filter()、concat() 和 slice()，使⽤ 这些⽅法将不会触发视图更新。



## 1.6.  Vue中v-for的key 有什么作用

在使用V-for进行列表渲染时，我们通常会给元素或者组件绑定一个key属性

key属性有什么作用呢

- key属性主要用在Vue的虚拟DOM算法，在新旧nodes对比时辨识VNodes（虚拟DOM）
- 如果不使用key，Vue会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法
- 使用key时，它会基于key的变化重新排列元素的顺序，并且会移除/销毁key不存在的元素

key是VNode的唯一标记，通过这个key，diff操作可以更准确，更快速的达到复用节点，更新视图的目的。复用节点就需要通过移动元素的位置来达到更新的目的



## 1.7. computed和method有什么区别

对于包含**响应式数据计算的逻辑**，应该使用计算属性，因为计算属性是有缓存的

相同点

- 都可以通过this进行访问
- 都可以对一些数据进行处理和计算

不同点

- computed底层会有缓存，性能更高
- computed会基于它们的依赖关系进行缓存
- 在数据不发送变化时，计算属性是不需要重新计算的
  - 但是如果依赖的数据发送变化，在使用时，计算属性依然会重新进行计算



## 1.8. 什么是双向绑定 v-model的本质

双向绑定：

- 当数据发送变化的时候，视图也发生变化，当视图发生变化的时候，数据也会跟着同步变化
- v-model是语法糖，它负责监听用户的表单元素中的输入事件来更新数据

表单元素使用v-model的本质

- v-bind绑定value的值
- v-on绑定input事件监听到函数，函数会获取最新的值，并赋值到绑定的属性中

```jsx
<input type="text" :value="message" @input="message = $event.target.value">
```

组件使用v-model的本质

- 将其value attribute 绑定到一个名叫 modelValue 的Prop上
- 在input事件被触发时，将新的值通过自定义的update：modelValue事件抛出（发出）

```vue
<Counter v-model="addCounter"></Counter>
// 等于
<Counter v-bind:modelvalue="addCounter" @update:modelvalue="addCounter = $event"></Counter>
```



## 1.9. data选项为什么是函数不是对象

JavaScript中的**对象是引用类型的数据**

- 当多个实例引用同一个对象时，只要一个实例对这个对象进行操作，其他实例中的数据也会发生变化

在Vue中，我们更多是想要复用组件，那就需要每个组件都有自己的数据，不会被其他的因素所影响，组件之间不会相互干扰

- 所以组件的数据不能写成对象的形式，而是要写成函数形式，数据以函数返回值的形式来定义
- 使用函数定义
  - **函数作用域**：
    - 函数有自己的作用域，这意味着在函数内部定义的变量（如 `let` 和 `const`）在函数外部是不可见的。每次函数调用时，这些变量都会重新初始化。
  - **闭包**：
    - 函数可以创建闭包，即函数可以访问其外部作用域的变量，但这些变量对于外部作用域来说是不可见的。这允许函数内部的变量保持私有。
  - **函数调用时的重新初始化**：
    - 每次调用函数时，函数内部的变量都会被重新初始化。这意味着即使函数是引用类型，每次调用时都会创建一个新的执行上下文，其中包含新的变量副本。

这样当每次复用组件的时候，就会返回一个新的data

每个组件都会有自己的私有数据空间

可以维护各自的数据，不会干扰其他组件的正常运行



## 1.10. data中某个属性的值发生改变时，视图会立即执行同步重新渲染吗

不会立即同步执行，重新渲染。

- Vue实现响应式并不是数据发生变化之后DOM立即重新渲染
  - 而是按照一定的策略进行DOM的更新的

Vue在更新DOM时是异步执行的，只要监听到数据变化，Vue将开启一个队列，并缓冲在同一事件中循环中发生的所有数据变更

如果同一个watcher被多次渲染，只会被推入到队列中一次，这种在缓冲时去除的重复数据对于避免不必要的计算和DOM操作是非常重要的

然后，在下一个的事件循环中 tick 中，Vue刷新队列并执行实例（这是已经去重）



## 1.11. Sass是什么，如何在Vue中安装和使用

- sass是一种CSS预处理器语言，除此之外，less，stylus也是常见的CSS预处理器语言

sass安装

1. 使用npm安装（sass-loader，css-loader等加载程序）
2. 在webpack.config.js中配置sass加载程序



## 1.12. 在Vue.js开发环境下调用API接口，如何避免跨越

- 在vue.config.js中的devServer选项中的proxy中配置反向代理
- 在vite.config.js中的Server选项中的proxy中配置反向代理
- 后端直接配置cors



## 1.13. v-if和v-for一起使用的弊端及解决办法

Vue.js 中使用最多的两个指令就是v-if和v-for，因此开发者们可能会想要同时使⽤它们。虽然不 建议这样做，但有时确实是必须的，于是我们想提供有关其⼯作⽅式的指南

- 在2.x版本中在一个元素上同时使用v-if和v-for时，v-for会优先生效
- 在3.x版本中v-if总是优先于v-for生效



## 1.14. 谈谈你对 keep-alive 的了解

keep-alive 是Vue内置组件，可以使被包含的组件保留状态，避免重新渲染

特性

- 一般结合路由和动态组件一起使用，⽤于缓存组件。

include：包括

exclude：不包括

- 提供include和exclude属性，两者都支持字符串和正则表达式
  - include 表示只有名称匹配的组件会被缓存。
  -  exclude 表示任何名称匹配的组件都不会被缓存。 
  - 其中 exclude 的优先级⽐ include ⾼。

- 对应两个钩⼦函数 activated 和 deactivated 。 
  - 当组件被激活时，触发钩⼦函数 activated。
  -  当组件被移除时，触发钩⼦函数 deactivated。

## 1.15. Vue的插槽的作用和平时开发中的应用

插槽的作⽤

- ⽀持在⽗组件⾃定义⼦组件中的个内容
- 让⼦组件更具有通⽤性，不必限定死某个内容

插槽平时开发中的应用

- 在封装组件时，如果组件中的某个内容是动态的或不确定的，就可以使⽤插槽来代替了
- 在使⽤第三⽅库时，往往会通过使⽤插槽类⾃定义第三⽅组件中的某些内容



# 2. Component组件

## 2.1 父子组件的生命周期顺序

加载渲染过程

- 父 beforeCreate
- 父 Create
- 父 beforeMount
- 子 beforeCreate
- 子 Create
- 子 beforeMount
- 子 Mounted
- 父 Mounted

子组件更新过程

- 父 beforeUpdate
- 子 beforeUpdate
- 子 Updated
- 父 Undated

父组件更新过程

- 父 beforeUpdate
- 父 Updated

销毁过程

- 父 beforeDestroy
- 子 beforeDestroy
- 子 Destroyed
- 父 Destroyed



## 2.2 组件通讯

- 父传子：props
  - 子组件通过props来接收父组件传递的属性值
- 子传父：$emit
  - 子组件通过emit触发事件传递，父组件通过监听对应的事件来接收数据
- Provide/inject
  - 父组件提供内容，子或孙组件可以注入父组件提供的内容
- 组件实例
  - 通过ref来拿到组件的实例，调用实例的属性或方法进行传值
- 事件总线
  - 可以自己编写EventBus插件来进行通讯，或使用第三方的事件总线库
- 使用Vuex/Pinia
  - 使用全局状态管理进行全局共享数据



## 2.3 什么是生命周期函数，Vue组件的生命周期函数有那些

生命周期函数

- 生命周期函数是一些回调函数，在某个时间会被Vue源码进行内部回调
- 通过对生命周期函数的回调，可以知道目前组件正在进行什么阶段

Vue2

- beforeCreate：组件实例在创建之前
- created：组件被创建完成
- beforeMount：组件template准备被挂载
- mounted：组件template已经被挂载
  - 可以获取DOM,可以使⽤DOM
- beforeUpdate: 准备更新DOM
- updated: 更新DOM
  - 根据最新数据⽣成新的VNode,⽣成新的虚拟DOM,转换为真实的DOM
- beforeUnmount: 卸载之前
- unmounted: DOM 元素被卸载完成

Vue3

1. **setup()**: 这是 Composition API 的入口函数。在 `setup()` 函数中，你可以定义响应式的数据、计算属性、方法和生命周期钩子。
2. **onBeforeMount()**: 在挂载之前调用。在这个阶段，组件实例已经被创建，但 DOM 尚未挂载。
3. **onMounted()**: 在挂载之后调用。在这个阶段，组件已经被挂载到 DOM 上，可以执行 DOM 操作或执行副作用。
4. **onBeforeUpdate()**: 在更新之前调用。在这个阶段，响应式数据已经更新，但 DOM 尚未重新渲染。
5. **onUpdated()**: 在更新之后调用。在这个阶段，响应式数据已经更新，并且 DOM 也已经重新渲染。
6. **onBeforeUnmount()**: 在卸载之前调用。在这个阶段，组件即将被销毁。
7. **onUnmounted()**: 在卸载之后调用。在这个阶段，组件已经被销毁。
8. **onActivated()**: 用于 `keep-alive` 缓存的组件激活时调用。
9. **onDeactivated()**: 用于 `keep-alive` 缓存的组件停用时调用。
10. **onErrorCaptured()**: 当捕获一个来自子孙组件的错误时被调用。
11. **onRenderTracked()**: 开启了跟踪的组件在依赖项被追踪时调用。
12. **onRenderTriggered()**: 开启了跟踪的组件在依赖项触发重新渲染时调用。
