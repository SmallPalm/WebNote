# 认识前端路由

- 路由其实是网络工程中的一个术语
  - 在架构一个网络时 , 有非常重要的两个设备就是路由器和交换器
- 事实上 , 路由器主要维护的是一个映射表
  - 自己的电脑的私网IP由路由器分配
- 映射表会决定数据的流向

- 映射表

  - 每一个IP地址都会映射到一台设备上面

    - 如何映射到每一台设备上

    - 会找到设备上的mac地址

    - ```路由器的映射表
      映射表的映射关系
      ip地址经1 -> mac1地址
      ip地址经2 -> mac2地址
      ip地址经3 -> mac3地址
      ```

- 路由的概念在软件工程中出现

  - 最早是在后端路由中实现的
  - 原因是web的发展主要经历了这样一些阶段

- 后端路由阶段

- 前后端分离阶段

- 单页面富应用 SPA

# 后端路由阶段

- 早期的网站开发整个HTML页面是由**服务器来渲染**的
  - 服务器直接生产渲染好对应的HTML页面
    - 返回给客户端进行展示
-  但是, 一个网站, **多页面服务器如何处理呢**
  - 一个页面有自己对应的网址, 也就是URL
  -  URL会发送到服务器
    - 服务器会通过正则对该URL进行匹配,
      - 并且最后交给一个Controller进行处理
  - Controller进行各种处理
    - 最终生成HTML或者数据, 返回给前端
- 上面的这种操作, 就是**后端路由**
- 当我们页面中需要请求不同的**路径**内容时
  - 交给服务器来进行处理
    - 服务器渲染好整个页面
      - 并且将页面返回给客户端
- 这种情况下渲染好的页面
  - 不需要单独加载任何的js和css
    - 可以直接交给浏览器展示
  - 这样也有利于SEO的优化

## **后端路由的缺点**

- 一种情况是整个页面的模块由后端人员来编写和维护的
-  另一种情况是前端开发人员如果要开发页面
  - 需要通过PHP和Java等语言来编写页面代码
- 通常情况下HTML代码和数据以及对应的逻辑会混在一起
  - 编写和维护都是非常糟糕的事情



# 前后端分离阶段

- 前端渲染的理解

  - 每次请求涉及到的静态资源都会从**静态资源服务器获取**
    - 这些资源**包括HTML+CSS+JS**
      - 然后在前端对这些请求回来的资源进行渲染
  - 需要注意的是
    - 客户端的每一次请求
    - 都会从静态资源服务器请求文件
  - 同时可以看到
    - 和之前的后端路由不同
      - 这时后端只是负责提供API了

- **前后端分离阶段**

  - 随着Ajax的出现, 有了前后端分离的开发模式

  - 后端只提供API来返回数据
    - 前端通过Ajax获取数据
    - 并且可以通过JavaScript将数据渲染到页面中
  - 这样做最大的优点就是前后端责任的清晰
    - 后端专注于数据上
    - 前端专注于交互和可视化上
  - 并且当移动端(iOS/Android)出现后
    - 后端不需要进行任何处理
    - 依然使用之前的一套API即可
  - 目前比较少的网站采用这种模式开发

**单页面富应用阶段**

- 其实SPA最主要的特点就是在前后端分离的基础上加了一层前端路由
  - 也就是**前端来维护一套路由规则**

前端路由的核心

- 改变URL，但是页面不进行整体的刷新

# 单页面SPA

- SPA : single page web application
- 在请求网站时
  - 会先渲染Header
  - 在header会有几个按钮
    - 点击按钮
    - 会修改URL地址
    - 内容发生改变
      - 但是头部不会重新渲染
      - 网站不会重新刷新
- 映射关系由前端来维护
  - 称之为前端路由
- 一个url对应一个组件



# URL的hash

- 前端路由是如何做到URL和内容进行映射 
  - 监听URL的改变
- URL的hash
  - URL的hash也就是锚点(#)
    - 本质上是改变window.loaction的href属性
  - 我们可以通过直接赋值location.hash来改变href
    - 但是页面不发生刷新
- hash的优势就是兼容性更好
  - 在老版IE都可以运行
  - 但是缺陷是有一个 #
    - 显得不像一个真实的路径



# HTML5的History

- history接口的Html5新增的
  - 它有六种模式改变URL而不刷新页面
- replaceState
  - 替换原来的路径
- pushState
  - 使用新的路径
- popState
  - 路径的回退
- go
  - 向前或向后改变路径
- forward
  - 向前改变路径
- back
  - 向后改变路径



# 认识vue-router

- 目前前端流行的三大框架
  - 都有自己的路径实现
    - Angular的ngRouter
    - react的ReactRouter
    - Vue的Vue-Router
- Vue-Router是Vue.js的官方路由
  - 它与Vue.js核心深度集成
    - 让用Vue.js构建单页面应用SPA变得非常容易

- Vue-router是基于路由和组件的
  - 路由用于设定访问路径
    - 将路径和组件映射起来

  - 在Vue-router的单页面应用中
    - 页面的路径的改变就是组件的切换



## 路由的使用步骤


创建路由对象

- routes : 映射关系
- history : 设置url的模式
  - 是hash
  - 还是history

让路由对象生效

app.use(router)

router-view的占位符

router-link进行路由的切换

## 路由的默认路径

- 默认情况下, 进入网站的首页
  -  我们希望<router-view>渲染首页的内容
-  默认没有显示首页组件, 必须让用户点击才可以
- **让路径****默认跳到到首页,
  - 并且<router-view>渲染首页组件**
- **routes中配置了一个映射**
  -  path配置的是根路径: /
  - redirect是重定向,
    - 也就是我们将根路径重定向到/home的路径下
      -  这样就可以得到我们想要的结果了

# router-link

- **to属性：**
  - 是一个字符串
    - 或者是一个对象
- **replace属性：**
  - 设置 replace 属性的话
  - 当点击时，会调用 router.replace()，而不是 router.push()；
- **active-class属性：**
  - 设置激活a元素后应用的class
    - 默认是router-link-active
-  **exact-active-class属性：**
  -  链接精准激活时
  - 应用于渲染的 <a> 的 class
  - 默认是router-link-exact-active

# 路由懒加载

- **当打包构建应用时**
  - **JavaScript 包会变得非常大，影响页面加载**
- 如果我们能把不同路由对应的组件分割成不同的代码块
  - 然后当路由被访问的时候才加载对应组件，这样就会更加高效
- 也可以提高首屏的渲染效率
-  其实这里还是我们前面讲到过的webpack的分包知识
  - 而Vue Router默认就支持动态来导入组件
  - 这是因为component可以传入一个组件
    - 也可以接收一个函数
      - 该函数 需要返回一个Promise
  -  而import函数就是返回一个Promise

# **路由的其他属性**

- name属性：路由记录独一无二的名称；
- meta属性：自定义的数据

# 动态路由基本匹配

- **我们需要将给定匹配模式的路由映射到同一个组件**
  - 在Vue Router中
    - 我们可以在路径中使用一个动态字段来实现
    - 我们称之为 路径参数
    - ![image-20231224204832161](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224204832161.png)

## 获取动态路由的值

- **在User中如何获取到对应ID的值**
- 在template中，直接通过 $route.params获取值；
- 在created中，通过 this.$route.params获取值；
- 在setup中，我们要使用 vue-router库给我们提供的一个hook useRoute；
  - 该Hook会返回一个Route对象，对象中保存着当前路由相关的值；



# NotFound

-  对于哪些没有匹配到的路由，我们通常会匹配到固定的某个页面
- 比如NotFound的错误页面中
  - 这个时候我们可编写一个动态路由用于匹配所有的页面
  - ![image-20231224204954712](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224204954712.png)

我们可以通过 $route.params.pathMatch获取到传入的参数



# 路由的嵌套

- 在一个页面本身,也可能会在多个组件之间来回切换
  - 需要使用嵌套路由
  - 在组件中也使用 router-view 来占位之后需要渲染的组件
  - ![image-20231224205125545](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205125545.png)

# 代码的页面跳转

- 希望通过代码来完成页面的跳转，比如点击的是一个按钮
  - ![image-20231224205202569](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205202569.png)

- 也可以传入一个对象
  - ![image-20231224205217110](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205217110.png)

- 在setup中编写的代码，那么通过 useRouter 来获取
  - ![image-20231224205234173](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205234173.png)

## query方式的参数

- 通过query来传递参数：

- ![image-20231224205250801](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205250801.png)

在界面中通过 $route.query 来获取参数

![image-20231224205320101](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205320101.png)





# 动态添加路由

- 某些情况下我们可能需要动态的来添加路由
  - 比如根据用户不同的权限，注册不同的路由
  - 这个时候我们可以使用一个方法 addRoute
- **如果我们是为route添加一个children路由，那么可以传入对应的name**
  - ![image-20231224205428146](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205428146.png)
  - ![image-20231224205437453](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205437453.png)

## 动态管理路由的其他方法

**删除路由三种方式**

- 方式一：添加一个name相同的路由
  - ![image-20231224205534267](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205534267.png)
- 方式二：通过removeRoute方法，传入路由的名称；
  - ![image-20231224205542306](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205542306.png)
- 方式三：通过addRoute方法的返回值回调；
  - ![image-20231224205552470](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205552470.png)

**路由的其他方法补充**

- router.hasRoute()：检查路由是否存在
- router.getRoutes()：获取一个包含所有路由记录的数组。





# 路由导航守卫

- vue-router 提供的导航守卫
  - 主要用来通过**跳转或取消的方式守卫导航**
- **全局的前置守卫beforeEach是在导航触发时会被回调的**

1. 判断用户是否登录
2. 根据逻辑进行不同的处理
3. 需要在路由导航守卫
   1. 进行路由拦截
   2. 没有登录进行登录页面
   3. 使用导航守卫进行回调
      1. 执行代码直接跳转页面



**beforeEach**

- 它有两个参数
  - to：即将进入的路由Route对象
  - from：即将离开的路由Route对象
- 它有返回值

- false：取消当前导航；

- 不返回或者undefined：进行默认导航；

- 返回一个路由地址：

  - 可以是一个string类型的路径；

  - 可以是一个对象
    - 对象中包含path、query、params等信息

![image-20231224205817667](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205817667.png)

![image-20231224205826549](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205826549.png)

## 其他导航守卫

- 目的都是在某一个时刻给予我们回调
  - 让我们可以更好的控制程序的流程或者功能

失活的组件 : 离开的组件

![image-20231224205858903](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231224205858903.png)

1. **beforeRouterLeave**
2. **回调beforeEach**
   1. 默认return false
   2. 可以设置return 返回的路径 /login
      1. 之后继续的操作就针对login来做
3. /user/123 -> /user/321
   1. **回调boforeRouteUpdate函数**
4. 在路径配置
   1. routes: [ { path, component, **回调beforeEnter函数** }]
5. **解析**异步组件
   1. 懒加载 () =>import
6. about组件
   1. **回调beforeRouteEnter**(next){
   2. this -> 获取不到组件实例
   3. 和最后一步相关联**next**(instance) =>{
   4. instance : 获取about组件实例
   5. }
   6. }
7. **回调beforeResolve**
   1. 异步组件被解析之后 , 在跳转页面之前
8. 进行导航
9.  确定进入导航中
   1. **回调afterEach()**
10. About template  -> DOM更新
11. 调用beforeRouteEnter的next传入的回调函数