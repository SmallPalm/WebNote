# 为什么需要redux

React主要负责帮助我们管理视图

state如何维护最终还是我们自己来决定；

- JavaScript需要管理的状态越来越多，越来越复杂
- React是在视图层帮助我我们解决了DOM的渲染过程
- 但是State依然是留给我们自己来管理
- 这些状态包括**服务器返回的数据**、**缓存数据**、**用户操作产生的数据**等等
- 包括一些**UI的状态**，比如**某些元素是否被选中**，**是否显示加载动效**，**当前分页**

管理不断变化的State是非常困难的

当应用程序复杂时，state在什么时候，因为什么原因而发生了变化，发生了怎么样的变化，会变得非常难以控制和追踪

> 状态之间相互会存在依赖
>
> 一个状态的变化会引起另一个状态的变化
>
> View页面也有可能会引起状态的变化

-  无论是组件定义自己的state
- 还是组件之间的通信通过props进行传递
- 也包括通过Context进行数据之间的共享

Redux就是一个帮助我们管理State的容器

Redux是JavaScript的状态容器，提供了可预测的状态管理

- Redux除了和React一起使用之外
  - 它也可以和其他界面库一起来使用（比如Vue）
    - 并且它非常小（包括依赖在内，只有2kb）

# Redux的核心理念 - Store

定义统一的规范来操作这段数据，跟踪整个数据的变化

- 当跟踪数据的变化时, 在一个项目中有多个组件使用或监听数据时
- 在其中某一个组件中数据发生变化, 其他组件的也跟着发送变化



# Redux的核心理念 - action

Redux要求我们通过action来更新数据

- 所有数据的变化，必须通过派发（dispatch）action来更新
-  action是一个普通的JavaScript对象，用来描述这次更新的type和content

> 强制使用action的好处是可以清晰的知道数据到底发生了什么样的变化
>
> 所有的数据变化都是可跟追、可预测的

通过函数来定义，返回一个action



# Redux的三大原则

1. 单一数据源
   - 整个应用程序的state被存储在一颗object tree中，并且这个object tree只存储在一个 store 中
   - Redux并没有强制让我们不能创建多个Store，但是那样做并不利于数据的维护
   - 单一的数据源可以让整个应用程序的state变得方便维护、追踪、修改
2. State是只读的
   - 唯一修改State的方法一定是触发action，不要试图在其他地方通过任何的方式来修改State
   - 这样就确保了View或网络请求都不能直接修改state，它们只能通过action来描述自己想要如何修改state
   - 这样可以保证所有的修改都被集中化处理，并且按照严格的顺序来执行，所以不需要担心race condition（竟态）的问题
3. 使用纯函数来执行修改
   - 通过reducer将 旧state和 actions联系在一起，并且返回一个新的State
   - 随着应用程序的复杂度增加，我们可以将reducer拆分成多个小的reducers，分别操作不同state tree的一部分
   - 但是所有的reducer都应该是纯函数，不能产生任何的副作用



# Redux的使用过程

1. 创建init对象，作为需要保存的状态
2. 创建Store来存储init对象
   - Store是在Reducer函数中传入
   - 可以通过State.getState来获取当前的State
3. 通过action来修改state
   - 通过dispatch来排放action
   - action通常是一个对象，携带type和其他数据
   - 在Reducer函数中获取action进行修改State
4. 修改reducer中的和处理代码
   - reducer是一个纯函数，不能直接修改state
   - 通过传入的state，不进行修改，而是返回一个浅拷贝的state
5. 通过subscribe方法来监听store的变化





# Redux结构划分

如果我们将所有的逻辑代码写到一起，那么当redux变得复杂时代码就难以维护。

接下来，我会对代码进行拆分，将store、reducer、action、constants拆分成一个个文件。 

创建store/index.js文件

创建store/reducer.js文件

创建store/actionCreators.js文件

创建store/constants.js文件
