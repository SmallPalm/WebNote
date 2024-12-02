# 什么是Pinia

- Pinia
  - （发音为/piːnjʌ/，如英语中的“peenya”）
  - 是最接近piña（西班牙语中的菠萝）的词
- Pinia开始于大概2019年
  - 最初是作为一个实验为Vue重新设计状态管理
  - 让它用起来像组合式API（Composition API）
- 从那时到现在
  - 最初的设计原则依然是相同的
  - 并且目前同时兼容Vue2、Vue3
    - 也并不要求完全使用Composition API
- Pinia本质上依然是一个状态管理的库
  - 用于跨组件、页面进行状态共享
    - 这点和Vuex、Redux一样

# Pinia和Vuex的区别

- 已经有Vuex了吗？为什么还要用Pinia呢
  -  Pinia 最初是为了探索 Vuex 的下一次迭代会是什么样子
    - 结合了 Vuex 5 核心团队讨论中的许多想法
  -  最终，团队意识到Pinia已经实现了Vuex5中大部分内容
    - 所以最终决定用Pinia来替代Vuex
- 与 Vuex 相比
  - Pinia 提供了一个更简单的 API
  - 具有更少的仪式
  - 提供了 Composition-API 风格的 API
- 最重要的是
  - 在与 TypeScript 一起使用时具有可靠的类型推断支持

和Vuex相比，Pinia有很多的优势

- 如mutations 不再存在
  - 他们经常被认为是非常冗长
  - 他们最初带来了 devtools 集成，但这不再是问题
- 更友好的TypeScript支持
  - Vuex之前对TS的支持很不友好
- 不再有modules的嵌套结构：
  - 你可以灵活使用每一个store
    - 它们是通过扁平化的方式来相互使用的
- 也不再有命名空间的概念
  - 不需要记住它们的复杂关系



# 使用Pinia

- 创建一个pinia并且将其传递给应用程序

![image-20240120134425662](D:\Typora\Typora笔记\Typora笔记\HY前端学习\image-20240120134425662.png)

![image-20240120134436688](D:\Typora\Typora笔记\Typora笔记\HY前端学习\image-20240120134436688.png)





# 认识Store

- 什么是Store
  - 一个Store (如: pinia) 是一个实体
  - 它持有为绑定到你组件数的状态和业务逻辑
    - 也就是保存了全局的状态
- 它有点像始终存在, 并且每个人都可以读取和写入的组件
- 可以在应用程序中**定义任意数量的store来管理状态**



**store三个核心概念**

- state , getters , actions
- 等同于options API组件的data , computed , methods
- 一旦store被实例化
  - 就可以**直接在store上访问state , getters 和 actions中定义的任何属性**



# 定义store

- 定义Store
  - store 需要 使用 pinia中的defineStore() 定义
  - 并且他需要一个唯一名称, 作为第一个参数的传递
  - ![image-20240120140034285](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120140034285.png)
  - **这个** **name**，也称为 **id**
    - 是必要的，Pinia **使用它来将 store 连接到devtools**
  - 返回的函数统一使用useX作为命名方案，这是约定的规范
    - 社区约定俗成的规范

## 使用定义Store

- Store在它被使用之前是不会创建的
  - 我们可以通过**调用use函数**来使用Store
- Store获取到后不能被解构，那么会失去响应式
  -  为了从 Store 中提取属性同时保持其响应式
    - 需要使用storeToRefs()
- ![image-20240120140431331](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120140431331.png)



# State

- state是store的核心部分
  - 因为state是用来帮助我们管理状态的。
- 在 Pinia 中，状态被定义为返回初始状态的函数

## 操作state

- **读取和写入 state**
  -  默认情况下，可以通过 store 实例访问状态来直接读取和写入状态
  - ![image-20240120140631870](D:\Typora\Typora笔记\Typora笔记\HY前端学习\image-20240120140631870.png)
- 重置 State
  - 可以通过调用 store 上的 $reset() 方法将状态 重置 到其初始值
  - ![image-20240120140704495](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120140704495.png)
- 改变State
  - 除了直接用 store.counter++ 修改 store
    - 还可以调用 $patch 方法
      - 它允许您使用部分“state”对象同时应用多个更改
      - ![image-20240120140758041](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120140758041.png)
- 替换state
  - 您可以通过将其 $state 属性设置为新对象来替换 Store 的整个状态
    - ![image-20240120140828637](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120140828637.png)



# Getters

- **Getters相当于Store的计算属性**
  - 它们可以用 defineStore() 中的 getters 属性定义
  - getters中可以定义接受一个state作为参数的函数



## 访问Getters

- 在组件中访问当前store的Getters

  - store.getters

- 在getters中访问自己的其他 getters

  - 通过this来访问到当前精store实例的所有除自己之外, 其他属性
  - this.getters

- 访问其他store的getters

  - 引入其他的store, 直接使用
    - use xxxx.getters

- Getters也可以返回一个函数，这样就可以接受参数

  - ![image-20240120141327646](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120141327646.png)

  - ![image-20240120141356932](D:\Typora\Typora笔记\Typora笔记\HY前端学习\image-20240120141356932.png)

# Actions

- **Actions 相当于组件中的 methods**
  - 可以使用 defineStore() 中的 actions 属性定义
    - 并且它们非常适合定义业务逻辑
  - 和getters一样
    - 在action中可以通过this访问整个store实例的所有操作

## 执行异步操作

- Actions中是支持异步操作的

  - 并且我们可以编写异步函数，在函数中使用await

  - ![image-20240120142028101](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120142028101.png)

  - # ![image-20240120142048179](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240120142048179.png) 
