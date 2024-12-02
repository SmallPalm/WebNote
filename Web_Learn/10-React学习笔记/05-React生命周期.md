

# 生命周期

React生命周期大概分为三个阶段

- 装载阶段 : Mount
  - 组件第一次在DOM树中被渲染的过程
- 更新阶段 : Update
  - 组件状态发生变化，重新更新渲染的过程
- 卸载过程 : Unmount
  - 组件从DOM树中被移除的过程



React内部为了告诉我们代码当前处于组件哪个阶段

会对我们组件内部实现的某些函数进行回调

这些函数就是生命周期函数

谈React生命周期时

主要谈的类的生命周

因为函数式组件是没有生命周期函数的

当然可以通过hooks来模拟一些生命周期的回调

# 生命周期图示

https://i.postimg.cc/vZhNQkHT/8c0301b9c635dc99d359096a3743105.png



# 生命周期函数

## Constructor : 挂载时执行

- 如果不初始化 state 或不进行方法绑定
  - 就不需要为组件创建构造函数
- constructor通常只做两件事
  - 通过给this.state 赋值对象来初始化组件内部的state
  - 为事件绑定实例 ( this )

## ComponentDidMount : 挂载时调用

- 在组件完成挂载后 - 插入DOM树中时立即调用

- ComponentDIdMount函数主要做的操作

  - 依赖于DOM的操作在这里执行

  - 在此处发送网络请求

  - 可以添加一些订阅

    - 指在组件销毁之前
    - 取消或清理在组件挂载或更新期间所进行的订阅操作（例如事件监听器、数据流订阅等）
    - 以防止内存泄漏或意外行为
    - 会在ComponentWillUnmount函数取消订阅

  - 订阅操作

    - 向WebSocket服务器订阅消息。
    - 使用setInterval或setTimeout来设置定时任务。
    - 监听浏览器事件（例如，window resize事件）。
    - 订阅某个外部数据源（如Redux store、RxJS observable等）。

  - ```react
    import React, { Component } from 'react';
    
    class MyComponent extends Component {
      componentDidMount() {
        // 订阅一个事件
        window.addEventListener('resize', this.handleResize);
      }
    
      componentWillUnmount() {
        // 取消订阅这个事件
        window.removeEventListener('resize', this.handleResize);
      }
    
      handleResize = () => {
        // 处理窗口大小调整的逻辑
        console.log('Window resized');
      }
    
      render() {
        return (
          <div>
            <h1>My Component</h1>
          </div>
        );
      }
    }
    
    export default MyComponent;
    ```

## componentDidUpdate: 更新时调用

- 在数据进行更新时会被调用, 但首次DOM渲染不会执行此方法
- 会返回三个参数
  - prevProps
    - 数据更新前的props

  - prevState
    - 数据更新前的state

  - snapshot
    - getSnapShotBeforeUpdate()函数返回的数据

- 操作
  - 对DOM进行操作
  - 你对更新前后的 props 进行了比较
  - 也可以选择在此处进行网络请求
  - 例如，当 props 未发生变化时，则不会执行网络请求

## componentWillUnmount: 销毁时调用

- 在组件卸载及销毁之前直接调用
- 操作
  - 在此方法中执行必要的清理操作；
  - 清除 timer，取消网络请求或清除在 componentDidMount() 中创建的订阅等

# 不常用生命周期函数

- 详情图片https://i.postimg.cc/cCWDZ9zV/1.jpg

### getDerivedStateFromProps()

- state 的值在任何时候都依赖于 props时使用
  - state的数据有依赖props时, 在这个函数中做操作

- 该方法返回一个对象来更新state

### getSnapshotBeforeUpdate()

- 在componentDidUpdate()函数上执行

- 在React更新DOM之前回调的一个函数
- 可以获取DOM更新前的一些信息（比如说滚动位置）
  - 然后对更新之后数据信息做对比进行判断句操作

### shouldComponentUpdate(): 常用

在render数据更新时 但componentDidUpdate函数还没有调用

- 该方法有两个参数
  1. nextProps : 修改之后, 最新的props属性
  2. nextState : 修改之后, 最新的state属性
- 该方法返回值是一个Boolean类型
  - 返回值为true, 就调用render方法
  - 返回值为false , 就不调用render方法
  - 默认返回true , 也就是state发生改变, 就会调用render方法
- 例子
  - 在state中增加一个message属性
  - JSX中并没有依赖这个message
    - 那么它的改变不应该引起重新渲染
  - 但是因为render监听到state的改变
    - 就会重新渲染
      - 所以最后render方法还是被重新调用了

- 返回Boolean类型
- 定义Render是否渲染