# 为什么使用setState

- **因为React中的state没有做数据劫持**
  - **没有做数据劫持, 对于React来说就不知道State要做出改变**
  - **所以就需要一个明确的方法 : setState方法**
    - **来告诉当前的组件我要重新设置state了**
      - **就会重新render函数, 就会重新渲染组件**

- 开发中并不能直接通过修改state的值来让界面发送更新
  - 直接修改State值, React并不知道State的值发送变化
    - 所以React不会根据最新的State来重新渲染界面
  - React并没有实现类似于Vue的Object.defineProperty或者Proxy来劫持数据来进行监听
- 必须通过setState来告知React数据已经发送变化
- setState的方法是Component类中继承过来的

# setState异步更新

- setState修改数据
  - 内部做的是合并操作
  - Object.assign(this.state, newState)进行合并, 新属性将旧属性就行合并

- setState的新是异步的
  -  setState是异步的操作
  - 并不能在执行完setState立马拿到最新的state的结果
- 为什么setState设计为异步
  - setState设计为异步, 可以**显著的提升性能**
    - 如果每次调用setState都进行一次更新
      - 那么意味着render函数会被频繁调用，界面重新渲染，这样效率是很低的
    - 最好的办法应该是获取到多个更新，之后进行批量更新 
  - 如果同步更新了state，但是还没有执行render函数
    - 那么state和props不能保持同步 	
      - **state和props不能保持一致性**，会在开发中产生很多的问题
    - 例子 : state发生更新但是Render函数没有渲染父组件和子组件的数据就不会保存一致性
      - 因为父子组件关联这props



## setState为什么是异步的

- 如果 `Parent` 和 `Child` 在同一个 click 事件中都调用了 `setState` ，
- 这样就可以确保 `Child` 不会被重新渲染两次。
- 取而代之的是，React 会将该 state “冲洗” 到**浏览器事件结束的时候**，
  - **再统一地进行更新**。
- 这种机制可以在大型应用中得到**很好的性能提升**。

# 同步获取异步的结果

**如何可以获取到更新后的值**

1. 方式一 : setState的回调

   - setState( partialState ,  callback )

   - 第二个参数是一个回调函数, 这个回调函数会在更新后会执行

     ```react
     this.setState({
       message: '你好, coderwhy'
     }, () => {
       console.log(this.state.message) //你好 coderwhy
     })
     ```

2. 方式二 : 生命周期函数

   - 数据更新回调的componentDidUpdate()

     ```react
     componentDidUpdate(prevProps, prevState, snapshot){
       //prevProps: 更新前的props
       //provState: 更新前的state
     	//snapshot: getSnapShotBeforeUpdate()函数返回的数据  
      	 console.log(this.state.message)
     }
     ```



# setState异步?(React18之前)

- setState是异步的还是同步是需要区分出来的

- 在组件生命周期或React合成事件中

  - setState是异步的 

- 在setTImeout或者原生DOM事件中

  - setState是同步的

- setTimeout中更新

  ```react
  setTimeout(() => {
    this.setState({
      message: '你好 黎明宇'
    })
    
    console.log(this.state.message)
  }, 0)
  ```

- 原生DOM事件

  ```react
  componentDidMount() {
    const btnEl = document.getElementById('btn')
    
    btnEl.onClick(() => {
      this.setState({
        message: '你好, 虾婆婆'
      })
      
      console.log(this.state.message)
    })
  }
  ```

  



# 在React18之后

- 在React18之后，默认所有的操作都被放到了批处理中（异步处理)

- 如果希望代码可以同步会拿到，则需要执行特殊的flushSync操作

  - flushSync用react-dom中获取
  
  - ```react
    flushSync(() => {
    	this.setState({count: 112334})
    })
    console.log(this.state.count)
    ```





# flushSync函数

- 用于确保setState在同步情况下立即刷新更新
  - 主要用于在需要立即进行状态更新并确保这些更新在下一个步骤之前反映在界面上的情况
    - 这个特性在处理某些需要即时反馈的用户交互时特别有用。



React 的更新是批处理的，这意味着在事件处理程序中触发的多个状态更新通常会被合并为一次重新渲染

​	flushSync就由此而生