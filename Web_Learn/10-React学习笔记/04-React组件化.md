# React组件化

- React的组件相对于Vue更加灵活和多样
  - 按照不同的方式可以分成很多类型的组件
- 根据**组件的定义方式 **分为
  - 函数组件 ( Function Component )
  - 类组件 ( Class Component )
- 根据**组件内部是否有状态需要维护** 分为
  - 无状态组件 ( Stateless Component )
  - 有状态组件 ( Stateful Component )
- 根据**组件的不同职责** 分为
  - 展示型组件 ( Presentational Component )
  - 容器型组件 ( Container Component )

这些概念有很多重叠

但是他们最主要是关注数据逻辑和UI展示的分离

1. 函数组件、无状态组件、展示型组件主要关注UI的展示
2. 类组件、有状态组件、容器型组件主要关注数据逻辑



# 类组件

**类组件的定义有如下要求：**

- 组件的名称是大写字符开头（无论类组件还是函数组件）
- 类组件需要继承自 React.Component
- 类组件必须实现render函数

在ES6之前，需要通过create-react-class 模块来定义类组件

但是目前官网建议我们使用ES6的class类定义

**使用class定义一个组件**

- constructor是可选的
  - 我们通常在constructor中初始化一些数据
    - this.state
  - this.state中维护的就是我们组件内部的数据；
- render() 方法是 class 组件中唯一必须实现的方法；



# render函数的返回值

- **当** **render** **被调用时**
  - **它会检查** **this.props** **和** **this.state** **的变化并返回以下类型之一**

- React元素 : 通常通过 JSX 创建
  - <MyComponent /> 会被 React 渲染为自定义组件
  - \<div /\> 会被 React 渲染为 DOM 节点

​	无论是 <div /> 还是 <MyComponent /> 均为 React 元素



- **数组或** **fragments**：使得 render 方法可以返回多个元素

- **Portals**：可以渲染子节点到不同的 DOM 子树中
- **字符串或数值类型**：它们在 DOM 中会被渲染为文本节点
- **布尔类型或** **null**：什么都不渲染



# 函数组件

- 函数组件是使用function来进行定义的函数
  - 只是这个函数会返回和类组件中render函数返回一样的内容
- 函数组件有自己的特点
  - 没有生命周期，也会被更新并挂载，但是没有生命周期函数
  - this关键字不能指向组件实例（因为没有组件实例）
  - 没有内部状态（state）

# 组件的通信

## 父传子

- 父组件通过 **属性 = 值** 的形式来传递给子组件数据

- 子组件通过 props 参数获取父组件传递来的数据

  - class组件内部有自动给props做保存

- ```react
  import React, {component} from 'react'
  // props参数传递一个对象, 对象中包裹数据
  // 子类组件
  class Personal extends component {
    constructor(props){
      super()
      this.props = props
    }
    
    render() {
      const {name, age, address} = this.props
      return (
      	<div>
        	<h2>{name, age, address}</h2>
        </div>
      )
    }
  } 
  
  
  // 子函数组件
  function students(props) {
    const {name, age, address} = props
    
    return (
      <div>
      	<h2>{name + age + address}</h2>
      </div>
    )
  }
  
  // 父组件
  class App extends component{
    constructor() {
      super()
      
      this.state = {
        arr: [1, 2, 4, 5, 6, 7, 8]
      }
    }
    
    render() {
      const {arr} = this.state
      return (
      	<div>
        	<Personal name="liming" :arr={arr} age="10" address='邯郸'></Personal>
          <students name="呜呜呜呜" age="10" address='邯郸'></students>
        </div>
      )
    }
  }
  ```

#### 参数Props

- 对于父组件传递给子组件的数据，有时候我们可能希望进行类型验证
  - 项目中默认继承了Flow或者TypeScript
    - 那么直接就可以进行类型验证
  - 没有使用Flow或者TypeScript
    - 也可以通过 **prop-types 库**来进行参数验证

- **如果没有传递，我们希望有默认值呢？**
  - 我们使用defaultProps就可以了

## 子传父

- 在Vue中是通过自定义事件来完成的
- 在React中同样是通过Props来传递消息的
  - 让父组件给子组件传递一个回调函数
  - 在子组件中调用这个函数进行传参
- 通过父组件传递给子组件的函数
  - 子组件将数据通过参数的形式传递给父组件就行




# React中的插槽

- Vue中是通过Slow来完成的

- React这种对于这种需要插槽的请求非常灵活

- 方案一

  - 使用组件的Children子元素

  - 弊端：通过索引值获取传入的元素很容易出错

    - 不能精准的获取传入的原生

  - ```react
    // children实现插槽
    // 每个组件都可以获取到 props.children
    // 它包含组件的开始标签和结束标签之间的内容
    class NavBer extends Component {
      constructor(props) {
        super()
        this.props = props
      }
      render() {
        const { children } = this.props
        return (
        	<div>
            // first
          	<div>{children[0]}</div>
        		// container
            <div>{children[1]}</div>
        		// end    
            <div>{children[2]}</div>
          </div>
        )
      }
    }
    
    class App extends Component {
      render() {
        return (
        	<div>
          	<NavBer>
            	<h2>first</h2>
              <div>container</div>
              <h2>end</h2>
            </NavBer>
          </div>
        )
      }
    }
    ```

- 方案二

  - 使用Props属性来传递React元素

  - ```react
    class NavBer extends component {
      constructor(props){
        super()
        
        this.props = props
      }
      
      
      render() {
        const {leftSlot, containerSlot, rightSlot} = this.props
        return (
        	<div>
          	<div>{leftSlot}</div>
            <div>{containerSlot}</div>
            <div>{rightSlot}</div>
          </div>
        )
      }
    } 
    
    
    class App extends component {
      render() {
        const leftSlot = <h2>你好</h2>
        const container = <h2>container</h2>
        const rightSlot = <h2>你好</h2>
        return (
        	<div>
            <NavBer rightSlot={rightSlot} container={container} leftSlot={leftSlot}></NavBer>
          </div>
        )
      }
    }
    ```



# 非父子组件通信

- **非父子组件数据的共享**
- React提供了一个API: Context
- Context提供了一种在组件之间共享此类值的方式
  - 而**不必显式地通过组件树的逐层传递props**
- Context设计目的是为了共享那些对于**一个组件树**而言是 **全局** 的数据
  - 例如当前认证 的用户, 主题, 或首选语言



## Context 相关 API

- **React.createContext**

  - 创建一个需要共享的Context对象

  - 如果一个组件订阅了Context

    - 那么这个组件会从离自身最近的那个匹配的Provider中读取到当前的Context的值

  - defaultValue是组件在顶层查找过程中没有找到对应的Provider

    ```react
    const MyContext = React.createContext(defaultValue)
    ```

- **MyContext.Provider**

  - 每个Context对象都会返回一个Provider **React组件**

    - 它允许消费组件订阅Context的变化
    - 消费组件: 就是使用Value值的组件

  - Provider 接收一个Value的属性, 传递给消费组件

  - 一个Provider可以在这个组件树中的多个消费组件有对应关系

  - 多个Provider也可以嵌套使用

    - 里层的会覆盖外层的数据

  - 当Provider的Value值发送变化时, 它内部的所有消费组件都会重新渲染

    ```react
    <MyContext.Provider value={/* 某个值 */} />
    ```

- **Class.contextType**

  - 挂载在class 上的contextType属性会被重新赋值为一个由React.createContext() 创建的Context对象

  - 这可以使用this.context来消费最近Context上的那个值

  - 可以在任何生命周期中访问到它Context的值, 包括render函数中

    ```react
    MyClass.contextType = MyContext
    ```

- **Context.Consumer**

  - React组件可以订阅到context的变更
    - 可以在函数式组件中完成订阅context
  - 这个函数接收当前的context值, 返回一个React节点

  ```react
  <MyContext.Consumer 
    {value => /* 基于context值进行渲染 */}
    ></MyContext.Consumer>
  ```

  - 什么时候使用Context.Consumer呢？
    - 1.当使用**value的组件是一个函数式组件**时；
    - 2.当组件中需要使用多个Context时；

- context定义的default数据
- 当子组件没有在Provider中时
  - 但ContextType赋值给Context定义的属性时
    - 子组件访问不了Provider的Value属性的内容 ,但可以访问Context中的默认属性
