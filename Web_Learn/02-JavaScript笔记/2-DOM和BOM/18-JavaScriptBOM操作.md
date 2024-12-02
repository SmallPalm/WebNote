# 认识BOM

- BOM : 浏览器对象模型 
  - 由浏览器提供的用于处理文档之外的所有内容的其他对象
  - 比如navigator , location , history 等对象
- JavaScript有一个非常重要的运行环境就是浏览器
  - 浏览器本身又作为一个应用程序(JavaScript)需要对其本身进行操作
  - 通常浏览器会有对应的对象模型(BOM , Browser , Object , Model)
  - 我们可以将BOM看成是连接JavaScript脚本与浏览器窗口的桥梁
- BOM主要包括的对象模型
  - window : 包括全局属性, 方法, 控制浏览器窗口相关的属性, 方法
  - location : 浏览器连接到对象的位置 (URL)
  - history : 操作浏览器的历史
  - navigator : 用户代理(浏览器) 的状态和标识 (很少用到)
  - screen : 屏幕窗口信息(很少用到)



# window对象

- 全局对象
  - ECMAscript其实是有一个全局对象的
    - 在node中是global对象
    - 在浏览器中是window对象
- 浏览器窗口对象
  - 作为浏览器窗口时, 提供了对浏览器操作的相关的API
- 当然 ,  这个两个视角存在大量重叠的地方 , 所以不需要刻意去区分它们
  - 事实上对于浏览器和Node全局对象名称不一样 ,目前已经指定了对应的标准
    - globalThis
    - 并且大多数浏览器都支持它
  - 放在window对象上的所有属性都可以被访问
  - 使用var定义的变量会被添加到window对象中
  - window默认给我们提供了全局的函数和类
    - setTimeout , Math , Date , Object

# window对象的作用

- window包含大量的东西
  1. 包含大量的属性
     - localStorage(本地存储)
       - 浏览器某一种存储的方案
     - console
     - location
     - history
     - 大概60多个属性
  2. 方法
     - open : 打开一个新的链接
     - 大概40多个方法
  3. 事件
     - hashchange
       - 路由实现原理
       - 监听浏览器链接的改变
       - 监听页面是否改变
     - 大概30多个事件
  4. 包含从EventTarget继承过来的方法

# location对象常见的属性

- location对象用于表示window上当前链接到的URL信息
- 常见的属性
  - href : 当前window对应的超链接URL(整个URL)
  - protocol : 当前的协议
  - host : 主机地址
  - hostname : 主机地址(不带端口)
  - port : 端口
  - pathname : 路径
  - search : 查询字符串
  - hashchange : 哈希值
- 对应的常用方法
  - assign : 赋值一个新的URL , 并且跳转到该URL中
  - replace : 打开一个新的URL , 并且跳转到该URL中
  - reload : 重新加载页面 , 可以传入一个Boolean类型



# URLSearchParams

- 搜索字符串
- 定义一些实用的方法来处理URL的查询字符串
  - 可以将一个字符串转成URLSearchParams
  - 也可以将一个URLSearchParams类型转成字符串
- URL常见的方法有如下
  - get : 获取搜索参数的值
  - set : 设置一个搜索参数和值
  - append : 追加一个搜索参数和值
  - has : 判断是否有某个搜索参数
- 中文会使用encodeURIComponent和decodeURIComponent进行编码和解码





# 前端路由核心

- 修改了URL , 但页面不进行刷新
  - 修改hash值
  - 修改history

# history对象常见属性和方法

- history对象允许我们访问浏览器曾经的会话历史记录

- 两个属性

  - length : 会话中的记录条数

  - state : 当前保留的状态值

- 五个方法
  - back() : 返回上一页
  - forward() : 前进下一页
  - go() : 加载历史中的某一页
    - 类似于上面的两个方法 , 只是可以设置层级
  - pushState() : 打开一个指定的地址
    - 修改URL , 但是页面不刷新
  - replaceState() : 打开一个新的地址, 并且使用replace

**history 和 hash 目前是vue , react等框架实现路由的底层原理**





# navigator对象(开发很少使用)

- navigator对象表示用户代理的状态和标识等信息



# screen对象

- 主要记录的是浏览器窗口外面的客户显示器的信息
