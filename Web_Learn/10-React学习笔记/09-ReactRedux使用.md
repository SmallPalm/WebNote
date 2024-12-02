# react-redux使用

redux和react没有直接的关系

你完全可以在React, Angular, Ember, jQuery, or vanilla JavaScript中使用Redux。

但是redux依然是和React库结合的更好，因为他们是通过state函数来描述界面的状态，Redux可以发射状态的更新，让他们作出相应



# Provide

在React-redux中有一个Provide

使用Provide进行包裹最外层的App组件，并传入一个store

在所有的组件都可以使用store





# Connect

Connect是一个高阶组件

```js
import { PureComponent } from "react" 
import { storeContext } from "./storeContext"
// connect 函数接收两个参数：mapStateToProps 和 mapDispatchToProps
// mapStateToProps: 用于将 store 中的 state 映射到组件的 props 中
// mapDispatchToProps: 用于将 dispatch 映射到组件的 props 中
function connect(mapStateToProps, mapDispatchToProps) {

  // 返回一个高阶组件 (HOC)，用于包装传入的组件 (WrappedComponent)
  return function (WrappedComponent) {

    // 创建一个新的组件 NewComponent，它继承自 PureComponent
    class NewCommponent extends PureComponent {
      constructor(props, context) {
        super(props)
        console.log(context)
        // 在构造函数中，将 store 的 state 和 action 初始化到组件的 state 中
        this.state = {
          // 通过 mapStateToProps 映射 store 中的 state
          storeState: mapStateToProps(context.getState()),
          // 通过 mapDispatchToProps 映射 store 的 dispatch 方法
          storeAction: mapDispatchToProps(context.dispatch)
        }
      }

      // 组件挂载时订阅 store 的变化
      componentDidMount() {
        // 订阅 store，监听 state 的变化
        this.unsubscribe = this.context.subscribe(() => {
          // 每次 store 更新时，调用 setState 更新组件的 state
          this.setState({
            storeState: mapStateToProps(this.context.getState())
          })
        })
      }

      // 组件卸载时取消订阅  
      componentDidCatch() {
        // 调用取消订阅的函数，避免内存泄漏
        this.unsubscribe()
      }

      // 渲染函数，返回被包装的组件，传递组件的 props 以及映射后的 storeState 和 storeAction
      render() {
        console.log("render", this.context)
        return <WrappedComponent {...this.props} {...this.state.storeState} {...this.state.storeAction} />
      }
    }
    // 通过Context中的Provide获取store
    // 在App中进行包裹Provide传入Store
    NewCommponent.contextType = storeContext
    // 返回新创建的组件
    return NewCommponent
  }
}

export default connect
```







redux中保存的counter是一个本地定义的数据 

我们可以直接通过同步的操作来dispatch action，state就会被立即更新。

但是真实开发中，redux中保存的很多数据可能来自服务器，我们需要进行异步的请求，再将数据保存到redux中。

# 理解中间件

redux也引入了中间件（Middleware）的概念

- 中间件的目的是在dispatch的action和最终达到的reducer之间，扩展一些自己的代码
- 比如日志记录、调用异步接口、添加代码调试功能等等

发送异步的网络请求添加对应的中间件

- 使用React-thunk库



redux-thunk是如何做到让我们可以发送异步的请求呢？

- 我们知道，默认情况下的dispatch(action)，action需要是一个JavaScript的对象； 

- redux-thunk可以让dispatch(action函数)，action可以是一个函数；

- action会在dispatch派发时直接进行调用

- 该函数会被调用，并且会传给这个函数一个dispatch函数和getState函数； 

  - dispatch函数用于我们之后再次派发action； 

  - getState函数考虑到我们之后的一些操作需要依赖原来的状态，用于让我们可以获取之前的一些状态；





# 使用redux-thunk

在创建store时传入应用了middleware的enhance函数

通过applyMiddleware来结合多个Middleware, 返回一个enhancer

 将enhancer作为第二个参数传入到createStore中；

```js
const store = createStore(reducer, composeEnhancers(applyMiddleware(thunk)))
```

定义返回一个函数的action

注意：这里不是返回一个对象了，而是一个函数

该函数在dispatch之后会被执行

```js
export const fetchMultiData = () => {
  //如果是一个普通的action,应该直接返回一个对象

  // 直接返回一个函数,redux默认是不支持的
  // 需要安装中间值Redux-thunk, 在dispatch中派发function
  // 当派发时, 这个函数就是立即执行
  // 这个派发的function, 会接收两个参数, 分别是dispatch和getState
  return async (dispatch, getState) => {
    const res = await axios.get('http://123.207.32.32:8000/home/multidata')
    const data = res.data.data
    console.log("getState", getState())
    dispatch(setBanners(data.banner.list))
    dispatch(setRecommends(data.recommend.list))
  }
} 
```









# combineReducers函数

用于Redux代码拆分之后的合并Reducer函数



合并的方式是通过每次调用reducer函数自己来返回一个新的对象

redux给我们提供了一个combineReducers函数可以方便的让我们对多个reducer进行合并

```js
const reducer = combineReducers({
  counter: counterReducer,
  multidata: multidataReducer
})
```



combineReducers是如何实现的呢

事实上，它也是将我们传入的reducers合并到一个对象中

- 最终返回一个combination的函数（相当于我们之前的reducer函 数了）

在执行combination函数的过程中

- 它会通过判断前后返回的数据是否相同来决定返回之前的state还是新的state

新的state会触发订阅者发生对应的刷新，而旧的state可以有效的组织订阅者发生刷新

```js
// combineReducers实现原理
function reducer (state = {}, action) {
  // react源码
  // 会进行判断,那个key的值发生了变化, 重新调用 
  // 没有进行action的就不会进行重新调用的优化
  // state.counter在第一次访问时,为undefined, 使用拆分之后的Reducer函数中默认的state
  //简单化: 直接全部调用
  return {
    counter: counterReducer(state.counter, action),
    multidata: multidataReducer(state.multidata, action)
  }
}
```

