# Hooks

Hooks指useState，useEffect这类的统称

使用Hooks有两个额外的规则

- 只能在函数最外层调用Hook，不能在循环，条件判断或者子函数中调用
  - 函数的第一层作用域的最上层中使用hooks
- 只能在React的函数组件中进行调用Hooks，不能在其他Javascript函数中调用Hooks



# useState

useState需要从react中导出，是一个函数

传入参数：初始化值，如果不设置为undefined

返回值：数组，包含两个元素

- 元素一：当时状态的值：变量
- 元素二：设置状态值的函数

useState会帮助我们定义一个 state变量

useState 是一种新方法，它与 class 里面的 this.state 提供的功能完全相同。 

- 一般来说，在函数退出后变量就会”消失”，而 state 中的变量会被 React 保留。





# useEffect

副作用：side Effects

side：一边，一旁，侧边

- 完成一些类似于class中生命周期的功能

类似于网络请求、手动更新DOM、一些事件的监听，都是React更新DOM的一些副作用

- 对于完成这些功能的Hook被称之为 Effect Hook

useEffect的解析

- 通过useEffect的Hook，可以告诉React需要在渲染后执行某些操作
-  useEffect要求我们传入一个回调函数，在React执行完更新DOM操作之后，就会回调这个函数
-  默认情况下，无论是第一次渲染之后，还是每次更新之后，都会执行这个 回调函数
  - 因为函数组件重新渲染了，useEffect重新回调函数

useEffect

- 参数一：执行的回调函数
- 参数二：当前useEffect在那些State发送变化时，进行重新回调：Array Type

useEffect传入的**回调函数A本身**可以有一个返回值，这个返回值是另外一个**回调函数B**

```js
EffectCallback = () => (void | (() => void | undefined))
```

在一个参数回调函数中返回一个回调函数

- 这是Effect可选的清除机制
-  如此可以将添加和移除订阅的逻辑放在一起

React 何时清除 effect？

- React 会在组件更新和卸载的时候执行清除操作；
- 正如之前学到的，effect 在每次渲染的时候都会执行；

如果一个函数我们不希望依赖任何的内容时，也可以传入一个空的数组 []：

那么这里的两个回调函数分别对应的就是componentDidMount和componentWillUnmount生命周期函数了





# useContext

在类组件中使用共享的Context有两种方法

- 通过类名.contextType = ThemeContext方法，在类中获取Context
- 多个Context或者在函数组中通过ThemeContext.Consumer方法传入函数，从参数中获取context

useContext允许我们通过Hook来直接获取某个Context的值

```jsx
function ContextHook() {
  const user = useContext(userContext)
  const theme = useContext(themeContext)
  
  return (
  	<div>ContextHook</div>
  )
}
```







# useReducer

useReducer仅仅是useState的一种替代方案

数据是不会共享的，它们只是使用了相同的counterReducer的函数而已

所以，useReducer只是useState的一种替代品，并不能替代Redux

- 在某些场景下，如果**state的处理逻辑比较复杂**，我们可以**通过useReducer来对其进行拆分**
- 或者这次修改的state需要依赖之前的state时，也可以使用；

```jsx
// 只是用来Redux中Reducer的写法
function counterReducer(state, action) {
  switch(action.type) {
    case "increment":
      return {...state, counter: state.counter + action.counter}
  	case "decrement":
  		return {...state, counter: state.counter - action.counter}
		default:
      return state
  }
}
 
function Counter() {
  const [state, dispatch] = useReducer(counterReducer, {counter: 999})
}
```

# 理解函数式组件中函数的执行和创建

当组件重新渲染时, 组件内部的function都会在内存中重新创建

因为在第一次时, function执行完成后改变数据, 组件重新渲染, function因执行完成, 被垃圾回收销毁

所以当组件每一次渲染时, 内部的function都是重新创建, 这会影响性能

# useCallback

useCallback实际的目的是为了进行性能的优化

- useCallback会返回一个函数的 memoized（记忆的） 值（返回的是一个函数）
- 在依赖不变的情况下，多次定义的时候，返回的值是相同的

```js
const memoizedCallback = useCallback(
	// 当前回调函数返回到memoizedCallBack中， 但依旧在多次渲染时，多次定义
  () => {},
  
  // 依赖的状态
  /**
   *  1.当为第二个参数: 为空数组时不依赖任何的数据, 就等于依赖没有发生改变
   *  2.那么就不会重新创建function, 会一直引用当前的function
   *  3.这样看不会创建多个function, 看似解决了性能问题
   *  4.但是现在会有一个闭包陷阱的问题, 这个函数中的state, 不会改变了
   *  5.当数据改变时, 一直被引用的function还是指向之前旧的值, 那么数据就不会发生变化了
   *  6.数组有依赖的值时, 必须要写入
   * 
   *  const handleClick = useCallback(() => {
   *    console.log("handleClick")
   *    setCounter(counter + 1)
   *  }, [])
   * */ 
  []
)
```

**理解第一个参数**

- 当参数二依赖数据不变的情况下, 多次渲染组件， 参数一回调函数依旧会多次定义, 
  - 只是返回的值相同时, 会保留返回值的函数, 不会多次定义

**useCallback性能优化的点**

- 当需要将一个函数传递给子组件时, 最好使用useCallback进行优化, 将优化后的代码, 传递给子组件

- 这样可以避免因为父组件的重新渲染, 导致子组件进行无用重复的多次渲染

**总结**

- 当父组件的其他数据发生改变时, 组件内的所有函数都需要重新定义 
- 如果父组件给子组件中传入函数, 当父组件中的函数重新定义, 子组件的props中的值发生改变, 这就代表子组件也需要重新渲染 
- 而useCallback可以解决这个问题 
- 只有自己的依赖数据发生改变时, 才会重新定义函数, 否则不会重新定义函数 
- 这样**子组件也不需要重新渲染** 

**闭包陷阱**

闭包陷阱：在 React 组件中，**闭包常常会导致我们捕获了旧的状态值**，特别是当状态更新依赖于前一个状态时。比如如果直接在 useCallback 中使用 counter，它可能会捕获旧的 counter 值，从而导致状态更新不正确。

- 使用使用useRef解决问题

```jsx
  const counterRef = useRef()
  counterRef.current = counter
  // 做法二(进一步优化): 使用useRef, 使组件多次渲染, 不会多次定义函数, 避开闭包陷阱
  // 函数不会重新定义, 子组件不会多次渲染, 没有闭包陷阱
  // 组件在多次渲染时, useRef返回同一个值, 不会生成新的对象, 是一个持久的对象
  const handleClick3 = useCallback(() => {
    console.log("handleClick3")
    // ref.current每一次获取都是最新的值
    setCounter(counterRef.current + 1)
    //counterRef.current 中保存的值，即使组件重新渲染，counterRef 对象不会重新初始化，它仍然保持着之前的状态。
  }, []) // 依赖项为空数组，意味着这个函数只会在组件初次渲染时创建一次
```



# useMemo

useMemo实际的目的也是为了进行性能的优化。

- useMemo返回的也是一个 memoized（记忆的） 值； （返回值是一个值，不是函数）
- 在依赖不变的情况下，多次定义的时候，返回的值是相同的；
- compute：计算，估算
- expensive: 代价高的

```js
const memoizedVariable = useMemo(() => computeExpensiveValue(a,b), [a,b]) 
```



进行大量的计算操作，是否有必须要每次渲染时都重新计算

- 如果值没有变，就不需要每次渲染重新计算

对子组件传递相同内容的对象时，使用useMemo进行性能的优化

```js
// 3.useCallback和useMemo进行对比
 function fn() {
  console.log('fn函数执行了')
 }
// useCallback: 对函数进行优化, 判断是否需要重新定义
const foo = useCallback(fn, [])
// useMemo: 对函数的返回值进行优化, 判断值是否需要重新定义
const bar = useMemo(() => fn, [])
```



# useRef

useRef返回的对象，在函数重新渲染时， 对象不会重新创建， 保持上一次的引用

useRef返回一个ref对象，返回的ref对象再组件的整个生命周期保持不变

最常用的ref是两种用法： 

用法一：引入DOM（或者组件，但是需要是class组件）元素；

用法二：保存一个数据，这个对象在整个生命周期中可以保存不变；



# useImperativeHandle

通过useImperativeHandle可以值暴露固定的操作：

通过useImperativeHandle的Hook，将传入的ref和useImperativeHandle第二个参数返回的对象绑定到了一起； 

所以在父组件中，使用 inputRef.current时，实际上使用的是返回的对象； 

```jsx
import React, { forwardRef, memo, useImperativeHandle, useRef } from 'react'

// forwardRef的做法本身没有什么问题，但是我们是将子组件的DOM直接暴露给了父组件
// 直接暴露给父组件带来的问题是某些情况的不可控
// 父组件可以拿到DOM后进行任意的操作
// 但是，事实上在上面的案例中，我们只是希望父组件可以操作的focus，其他并不希望它随意操作

const Home = memo(forwardRef((props, ref) => {
  const refDom = useRef()

  // 子组件对父组件中传入的ref做处理
  // 将传入的ref和useImperativeHandle第二个参数返回的对象绑定到了一起
  useImperativeHandle(ref, () => ({
    // 在父组件中使用 Ref.current时，实际上使用的是返回的对象；
    focus() {
      refDom.current.focus()
    },
    setValue(value) {
      refDom.current.value = value
    }
  }))

  return (
    <div>
      <h2>Home</h2>
      <input type="text" ref={refDom} />
    </div>
  )
}))

function App() {
  const inputRef = useRef()
  return (
    <div>
      <Home ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>聚焦</button>
      <button onClick={() => inputRef.current.setValue('abc')}>设置值</button>
    </div>
  )
}

export default App
```

# useLayoutEffect

用法和Effcet相同

就是两个Hook执行时机不同

useLayoutEffect 和 useEffect区别

- useEffect会在渲染的内容更新到DOM上后执行，不会阻塞DOM的更新
  - DOM更新后执行
- useLayoutEffect会在渲染的内容更新到DOM上之前执行，会阻塞DOM的更新
  - DOM更新前执行





# 自定义Hook

自定义Hook本质上只是一种函数代码逻辑的抽取，严格意义上来说，它本身并不算React的特性

**定义函数时，使用use开头，在React中就是一个Hook**

**在自定义Hook中，可以使用React自带的Hook**





# Redux Hooks

在之前的redux开发中，为了让组件和redux结合起来，我们使用了react-redux中的connect：

- 但是这种方式必须使用高阶函数结合返回的高阶组件； 
- 并且必须编写：mapStateToProps和 mapDispatchToProps映射的函数；

useSelector的作用是将state映射到组件中： 

- 参数一：将state映射到需要的数据中； 
- 参数二：可以进行比较来决定是否组件重新渲染；
  - 因为如果中两个组件使用都获取相同的redux中的state， 就需要对比一下数据有没有被改变， 默认一个组件会影响子组件的渲染

useSelector默认会比较我们返回的两个对象是否相等；

- 如何比较呢？ const refEquality = (a, b) => a === b
- 也就是我们必须返回两个完全相等的对象才可以不引起重新渲染

useDispatch非常简单，就是直接获取dispatch函数，之后在组件中直接使用即可； 

我们还可以通过useStore来获取当前的store对象；

```jsx
import React, { memo } from 'react'
import { useSelector, useDispatch, shallowEqual } from 'react-redux'
import { addCountAction, subCountAction, changeMassage } from '../store/actionCreators'
// 当父子组件共用一个state中的数据中, 父组件值改变子组件也会被渲染
// 在useSelector中传入第二个参数
// shallowEqual: 对数据做浅比较, 如果数据没有改变, 就不会重新渲染

// 参数一：将state映射到需要的数据中
// 参数二：可以进行比较来决定是否组件重新渲染
function App() {
  const count = useSelector(state => state.count)
  const dispatch = useDispatch()
  const addCount = () => {
    dispatch(addCountAction(1))
  }
  const subCount = () => {
    dispatch(subCountAction(1))
  }
  
  console.log("App render")

  return (
    <div>
      <p>{count}</p>
      <button onClick={addCount}>+</button>
      <button onClick={subCount}>-</button>
      {/* 子组件不会因为获取的counter， 影响到message组件中获取参数时的重新渲染 */}
      <Message></Message>
    </div>
  )
}

// 默认会比较我们返回的两个对象是否相等
// 如何比较呢？ const refEquality = (a, b) => a === b
// 也就是我们必须返回两个完全相等的对象才可以不引起重新渲染
const Message = memo((props) => {
  const dispatch = useDispatch()
  const { message } = useSelector(state => (
    {
      message: state.message
    }
  ), shallowEqual)
// shallowEqual: 对数据做浅比较, 如果数据没有改变, 就不会重新渲染
  function mwwassage() {
    dispatch(changeMassage("我是Message组件"))
  }

  console.log("Message render")
  return (
    <div>
      <h2>{message}</h2>
      <button onClick={mwwassage}>修改message</button>
    </div>
  )
})
export default App
```

