# Hook

Hooks是React 16.8中新增特性

主要在函数式组件中使用

在不编写class的情况下使用state以及其他React的特性: 如生命周期



# Class VS Function：before Hooks

class组件可以定义自己的state，用来保护组件内部的数据状态

- 函数组件不可以，生成的变量得不到持久化
  - 因为当组件重新渲染，函数会被重新调用都会产生新的临时变量

class组件有自己的生命周期， 在对应的生命周期中完成自己的逻辑

- 如果在函数中进行某些逻辑，这意味函数每次重新调用都会重新执行某些逻辑

class组件可以在状态改变时只会重新执行render函数

以及希望重新调用的生命周期componentDidUpdate等生命周期

- 函数组件在状态改变时，不会重新渲染
  - 并且就是重新渲染，状态重新生成，还是之前的状态
  - 没有什么地方可以在函数内部只调用一次



# Class issue

复杂组件变得难以理解

- 当业务增多，class组件会变得越来越复杂
- componentDidMount中，可能就会包含大量的逻辑代码
  - 还需要在componentWillUnmount中移除
- class实际上逻辑非常难以拆分
  - 增加代码复杂度

难以理解的class

- 学习ES6的class是学习React的一个障碍
- 必须搞清楚this的指向到底是谁

组件复用状态很难

- 为了一些状态的复用我们需要通过高阶组件
- 学习的redux中**connect**或者react-router中的**withRouter**
  - 这些高阶组件设计的目的就是为了状态的复用
- 者类似于Provider、Consumer来共享一些状态
  - 但是多次使用Consumer时，我们的代码就会存在很多嵌套



# Hooks Arise

arise：产生，出现

Hooks总结

- 它可以让我们在不编写class的情况下使用state以及其他的React特性

Hook的使用场景

Hooks的出现基本可以代替之前所以使用class组件的地方

Hook只能在函数组件中使用，不能在类组件，或者函数组件之外的地方使用

**完全可选的**：无需重写任何已有代码就可以在一些组件中尝试 Hook

**100% 向后兼容的**：Hook 不包含任何破坏性改动。

Hook 已发布于 **v16.8.0**。
