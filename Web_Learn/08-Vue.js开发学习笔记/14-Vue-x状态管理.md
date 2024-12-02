# 什么的状态管理

- 在开发中
  - 我们会的应用程序需要处理各种各样的数据
  - 这些数据需要保证在我们应用程序中的某个位置
    - 对于这个数据的管理
  - 称之为是状态管理

管理状态

-  在Vue开发中，使用组件化的开发方式
  - 而在组件中定义data或者在setup中返回使用的数据
  - 这些数据我们称之为state；
    - state  : 状态
- 在模块template中我们可以使用这些数据
  - 模块最终会被渲染成DOM
    - 我们称之为View
- 在模块中我们会产生一些行为事件
  - 处理这些行为事件时
  - 有可能会修改state
  - 这些行为事件我们称之为actions



# 复杂的状态管理

- JavaScript开发的应用程序, 已经变得越来越复杂
  - JavaScript需要管理的状态越来越多, 也是更加复杂
  - 这些状态包括
    - **服务器返回的数据**
    - **缓存数据**
    - **用户操作产生的数据**等等
  - 也包括一些UI的状态
    - 比如某些元素是否被选中
    - 是否显示加载动画效果
    - 当前分页等
- 当我们的应用遇到**多个组件共享状态**时
  - 单向数据流的简洁性很容易被破坏
  - 多个视图 , 组件 , page依赖于同一状态(变量)
  - 来自不同的视图的行为需要变更同一状态
- 是否通过组件数据的传递来完成
  - 对于一些简单的状态(变量) 
    - 确实可以通过**props的传递**或者**Provide的方式**来共享状态
  - 但是对于复杂的状态管理来说
    - 显然通过传递和共享的方式是不足以解决问题的
    - 需要使用状态管理



# VueX的状态管理

- 管理不断变化的state本身是非常困难的
  - state : 状态
- 状态之间相互会存在依赖
  - 一个状态的变化会引起另一个状态的变化
  - View页面也有可能会引起状态的变化
- 当应用程序复杂时
  - state在什么时候
    - 因为什么原因而发生了变化
    - 发生了怎么样的变化
    - 会变得非常难以控制和追踪
- 这样就诞生状态管理
- 将组件的内部状态抽离出来
  - 以一个全局单例的方式来管理

这就是Vuex背后的基本思想

- 在这种模式下
  - 我们的组件树构成了一个巨大的 “视图View”
- 不管在树的哪个位置
  - 只需要引入状态管理库
  - 任何组件都能获取状态或者触发行为
- 通过定义和隔离状态管理中的各个概念
  - 并通过强制性的规则来维护视图和状态间的独立性
    - 我们的代码边会变得更加结构化和易于维护、跟踪；
- Vue-Components : Vue组件
- Dispatch : 派发事件
- Actions : 行动
- Backend APl : 后端API
- Commit : 提交
- Mutation : 改变 : 事件
- Mutate : 改变状态

![image-20240118193316295](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118193316295.png)

# 创建Store

- 每一个Vuex应用的核心就是store（仓库）
  - store本质上是一个容器
    - 它包含着你的应用中大部分的状态（state）
- **Vuex和单纯的全局对象有什么区别呢?**
  - 第一：Vuex的状态存储是响应式的
    - 当Vue组件从store中读取状态的时候
      - 若store中的状态发生变化
      - 那么相应的组件也会被更新
  - 第二：不能直接改变store中的状态
    -  改变store中的状态的唯一途径就显示**提交 (commit) mutation**
    - 这样使得我们可以方便的跟踪每一个状态的变化
      - 从而让我们能够通过一些工具帮助我们更好的管理应用的状态

# 单一状态树

- **Vuex 使用了单一状态树**
  - 用一个对象就包含了全部的应用层级的状态
  - 采用的是SSOT，Single Source of Truth
    - 也可以翻译成单一数据源
- **这也意味着，每个应用将仅仅包含一个** **store 实例**
  - 单状态树和模块化并不冲突
- **单一状态树的优势**
  - 如果你的状态信息是保存到多个Store对象中的
    - 那么之后的管理和维护等等都会变得特别困难
  - 所以Vuex也使用了单一状态树来管理应用层级的全部状态
  - 单一状态树能够让我们**最直接的方式找到某个状态的片段**
  - 而且在之后的维护和调试过程中
    - 也可以非常方便的管理和维护





# 获取store中的状态

- **如果我们有很多个状态都需要获取话，可以使用mapState的辅助函数**

  - mapState的方式一：对象类型

  - mapState的方式二：数组类型

  - 也可以使用展开运算符和来原有的computed混合在一起

# 状态管理的五个选项

# State

## 在setup中使用mapState

- 在setup中如果我们单个获取装是非常简单的
  - 通过useStore拿到store后去获取某个状态即可
  - 但是如果我们需要使用 mapState 的功能呢
- **默认情况下，Vuex并没有提供非常方便的使用mapState的方式，这里我们进行了一个函数的封装**
  - ![image-20240118194840623](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118194840623.png)

# Getters

相当于computed计算属性

在getters中的对象的set方法, get方法

- 有两个参数
- 第一个是state
- 第二个是getters
  - getters可以获取自己本身中函数

## getters的返回函数

- getters中的函数本身
  - 可以返回一个函数
- 那么在使用的组件中相当于可以一直调用这个函数

## mapGetters的辅助函数

- 在options API中使用mapGetters
  - ![image-20240118195803687](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118195803687.png)
- 在composition API中使用mapGetters
  - ![image-20240118200004280](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118200004280.png)



# Mutation

- **更改 Vuex 的 store 中的状态的唯一方法是提交 mutation**
  - 提交 :commit

## Mutation携带数据

- 很多时候我们在提交mutation的时候
  - 会携带一些数据
  - 这个时候我们可以使用参数
    - 第一个参数 : state
    - 第二个参数 : payload
      - payload为对象类型
        - **对象风格的提交方式**
        - ![image-20240118200311358](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118200311358.png)

## Mutation常量类型

- 创建个文件
  - 里面专门定义相关的Mutation事件的常量名
- ![image-20240118200423157](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118200423157.png)

**定义mutation**

- ![image-20240118200434919](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118200434919.png)

**提交mutation**

- ![image-20240118200450229](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118200450229.png)



## mapMutations辅助



## 函数

- options API定义
  - ![image-20240118200559765](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118200559765.png)
- Composition API定义
  - ![image-20240118200627486](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118200627486.png)

## Mutation重要原则

- 一个重要的原则就是Mutaiton必须是同步函数
  -  这是因为devtool工具会记录mutation的日记
  - 每一条mutation被记录
    - devtools都需要捕捉到前一状态和后一状态的快照
  -  但是在mutation中执行异步操作
    - 就无法追踪到数据的变化
- **所以Vuex的重要原则中要求 mutation必须是同步函数**
  - 如果我们希望在Vuex中发送网络请求的话需要如何操作
    - 使用actions



# Actions

- Actions类似于mutations , 不同在于

  - Actions提交的是mutations, 而不是直接改变 变更state

- Actions可以包含任何异步操作

  - 就是在Actions中发生网络请求
  - 收到的数据在提交在Mutations中
    - 在Mutations中修改state状态

- **在Actions中有一个非常重要的参数context**

  - context是一个和store实例均有相同方法和属性的context对象

  - 所以我们可以从其中获取到commit方法来提交一个mutation

  - 或者通过 context.state 和 context.getters 来获取 state 和

    getters

## Actions的分发操作

- 如何使用actions进行actions的分发
  - 分发使用的是store上的dispatch函数
  - 就是在组件中给actions传递数据
  - ![image-20240118201844836](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118201844836.png)



## actions的辅助函数

- ![image-20240118201915779](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118201915779.png)



## actions的异步操作

- **Action 通常是异步的，那么如何知道 action 什么时候结束呢**
  - 我们可以通过让actions的函数中返回Promise
    - 在组件中获取到的Promise的then中来处理完成后的操作
- ![image-20240118202056256](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118202056256.png)



# Module

- 什么是Module

  - 由于使用单一状态树
    - 应用的所有状态会集中到一个比较大的对象
    - 当应用变得非常复杂时
      - store 对象就有可能变得相当臃肿；
        - 就是store中的对象太多了
        - 使用module给仓库中的对象进行分配管理
  - 为了解决以上问题
    - Vuex 允许我们将 store 分割成**模块（module）**
  - 每个模块拥有自己的 state、mutation、action、getter
    - 甚至是嵌套子模块
  - ![image-20240118202844108](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118202844108.png)

  

## module的局部状态

- 对于模块内部的 mutation 和 getter
  - 接收的第一个参数是**模块的局部状态对象**
    - 如果在局部模块状态对象中没有找到
      - 会去index总仓库中寻找

## module的命名空间

默认情况下

- 模块内部的action和mutation仍然是注册在**全局的命名空间**中的
- 这样使得多个模块能够对同一个 action 或 mutation 作出响应
  - Getter 同样也默认注册在全局命名空间

- 如果我们希望模块具有更高的封装度和复用性
  - 可以添加 namespaced: true 的方式使其成为带命名空间的模块
- 当模块被注册后
  - 它的所有 getter、action 及 mutation 
    - 都会自动根据模块注册的路径调整命名；
- ![image-20240118203404223](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118203404223.png)
  - rootState : 根store
  - rootGetters : 根getters

## module修改或派发根组件

- 如果我们希望在action中修改root中的state，那么有如下的方式
- ![image-20240118203508640](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240118203508640.png)