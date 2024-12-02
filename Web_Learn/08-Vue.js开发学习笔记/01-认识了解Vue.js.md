# 认识Vue

- Vue : view
  - 一套用于**构建用户界面**的**渐进式 JavaScript 框架**
- 它基于标准HTML , CSS 和 JavaScript 构建
  - 并提供了一套声明式的 ,  组件化的编程模型
  - 高效地开发用户界面 , 无论任务简单或复杂

什么是渐进式框架

- 表示我们可以在项目中一点点来引入和使用Vue
  - 而不一定需要全部使用Vue来开发整个项目

目前前端流行的是三大框架

- Vue
  - Vue国内的占有率是最高的
- React
  - React国内外的占有率都是非常高
- Angular
  - 入门门槛较高 : 需要使用TypeScript
  - 国内市场占有率较低
  - 但本身非常优秀的框架



## Vue3

- 2020年9月19日发布正式版
  - 命名One Piece
- 更好的性能
- 更小的包体积
- 更好的TypeScript集成
- 更优秀的API设计

**Vue的本质就是一个JavaScript的库**

# 原生开发和Vue开发

原生开发和Vue开发的模式和特点

- 涉及两种不同的编程范式
- 命令式编程 和 声明式编程
- 命令式编程关注
  - How to do
    - 如何做 , 怎么做
  - 自己完成整个How的过程
- 声明式编程
  - What to do
    - 该做什么
  - 由框架完成How的过程

**原生开发**

- 每完成一个操作 , 都需要通过JavaScript编写一条代码
  - 来给浏览器一个指令
  - 这样编写的代码的过程称之为**命令式编程**

Vue开发

- 会再**createApp函数中传入的对象中声明需要的内容**
  - 传入
    - template : 模板
    - data : 数据
    - methods : 方法
  - 这个传入的结合的编写代码的过程称之为声明式编程
- 目前Vue React Angular 小程序的编程模式
  - 都是声明式编程

# MVVM模型

- MVC和MVVM都是一种软件的体系结构
  - MVC是Model – View –Controller的简称
  - 是在前期被使用非常多的框架的架构模式
    - 比如iOS、前端
- MVVM是Model-View-ViewModel的简称
  - 是目前非常流行的架构模式

通常情况下，我们也经常称Vue是一个MVVM的框架

- Vue官方其实有说明
  - Vue虽然并没有完全遵守MVVM的模型
  - 但是整个设计是受到它的启发的

![image-20231201180742351](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231201180742351.png)



# data属性

- data属性是传入一个函数 , 并且该函数需要返回一个对象
  - 在Vue2.x的时候
    - 也可以传入一个对象
    - 虽然官方推荐是一个函数
  - 在Vue3.x的时候
    - 必须传入一个函数
    - 否则就会直接在浏览器中报错
- data中返回的对象会被Vue的响应式系统检测劫持到
  - 之后对该对象的修改或者访问
    - 都会在劫持中被处理
- 所有我们在template或者app中通过 {{counter}} 访问counter
  - 可以从对象中获取到数据
- 所以我们修改counter的值时
  - app中的 {{counter}}也会发生改变

# methods属性

- methods属性是一个对象
  - 通常我们会在这个对象中定义很多的方法(函数)
- 这些方法 函数 可以被绑定到模板中
  - 在定义的方法中 ,可以**使用this关键字**
    - **可以直接访问到data中返回的对象的属性**
- methods中的函数不能使用箭头函数
- 官方文档有这么一段描述
  - 注意 , 不应该使用箭头函数来定义method函数
  - 理由是箭头函数绑定了父级作用域的上下文
    - 所以this将不会按照期望指向组件实例
    - 因为它们不能通过 `this` 访问组件实例

## 问题一：不能使用箭头函数

- 在`methods`中要使用`data`返回对象中的数据
  - 那么这个`this`是必须有值的
    - 并且应该可以通过`this`获取到`data`返回对象中的数据
- 那么我们这个this能不能是window
  - 不可以是window
    - 因为window中我们无法获取到data返回对象中的数据
  - 但是如果我们使用箭头函数
    - 那么这个this就会是window了
- 为什么this就会是window
  -  这里涉及到箭头函数使用this的查找规则
  - 箭头函数会在自己的上层作用于中来查找this

## 问题二：this到底指向什么

- 事实上Vue的源码当中就是对methods中的所有函数进行了遍历
  - 并且通过bind绑定了this
- 对methods中的所有的函数进行遍历
  - 在将所有遍历出来的每一个函数
    - 通过bind的方法绑定data中返回的对象的代理对象proxy



****
