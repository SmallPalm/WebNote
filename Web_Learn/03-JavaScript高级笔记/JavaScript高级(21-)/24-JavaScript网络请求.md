# 前后端分离的优势

- 早期的网页都是通过后端渲染来完成的
  - 服务器端渲染 
    - SSR 缩写 server side render
- 客户端发出请求 -> 服务端接收请求并返回相应HTML文档 -> 页面刷新 , 客户端加载新的HTML文档

**服务器端缺点**

- 当用户点击页面中某个按钮向服务器发送请求时 
  -  页面本质上只是一些数据发生了变化 
  - 而此时服务器却要将整个页面重新渲染并在返回给浏览器加载
    - 这显然有悖于程序员的 DRY (don’ t repeat yourself) 原则
- 明明只是一些数据的变化却迫使服务器要返回整个HTML文档
  - 这本事也会给网络带宽带来不必要的开销

**AJAX**

- 页面数据变动时 , 只向服务器请求新的数据 ,
  - 并且阻止页面刷新的情况下, 动态的替换页面中展示的数据

## AJAX

- “ Asynchronous JavaScript And XML” 的缩写 (异步的JavaScript和XML)

- 是一种实现无页面刷新 ,获取服务器数据的技术
- AJAX最吸引人的就是它的 异步 特性
  - 可以在不重新刷新页面的情况下与服务器通信 , 交换数据 或者更新页面
- 使用AJAX最主要的两个特性做
  - 在不重新加载页面的情况下发送请求给服务器
  - 接受并使用从服务器发来的数据

# HTTP

**维基百科**

- 超文本传输协议 是一种用于分布式 协作式 和 超媒体信息系统的应用层协议  HTTP protocol
- HTTP是万维网的数据通信的基础 , 设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法
- 通过HTTP和HTTPS 协议请求 的资源 由统一资源的标识符来标识
  - 标识符 URI

HTTP是一个客户端 (用户) 和服务器 (网站) 之间**请求**和**相应**的标准

- 通过使用网页浏览器 , 网络爬虫 或者 其他的工具 ,
  - 客户端 发起一个HTTP请求到服务器上指定端口
    -  (默认端口为 80)
      - 我们称这个客户端为用户代理程序  HTTP Request
- 响应的服务器上存储着一些资源
  - 比如HTML文件和图像
    - 我们称	这个响应服务器为源服务器  HTTP Response



### 网页中资源的获取

- 我们网页中的资源通常是被放在Web资源服务器中, 由浏览器自动发生HTTP请求来获取 , 解析 , 展示的
- 目前我们页面中很多数据是动态展示的
  - 比如页面中的数据展示 ,搜索数据 ,表单验证 等等, 也是通过JavaScript中发送HTTP请求获取的

# HTTP的组成

- 一次HTTP请求主要包括 : 请求(Request)和响应(Response)

请求

- 请求行
  - 给网络来读取
- 请求头
  - 给服务器携带的一些额外信息
- 请求体
  - 本次要给服务器传的具体的参数

响应

- 响应行
  - 返回协议版本, 状态码, 
- 响应头
  - 返回本次数据的类型等等
- 响应体
  - 本次给浏览器返回的具体的内容

# HTTP的请求方式

在RFC中定义了一组请求方式 , 来表示要对给定资源执行的操作

- GET :  请求一个指定资源的表示形式
  - 使用get的请求应该只被用于获取数据
- HEAD : 请求一个与GET 请求的响应 相同的响应 但没有响应体
  - 比如在准备下载一个文件前 , 先获取文件的大小 , 在决定是否进行下载
- POST :  用于将实体提交到指定的资源
- PUT : 用请求有效载荷(payload) 替换 目标资源的所有当前表示
- DELETE : 删除指定的资源
- PATCH : 用于对资源应部分修改
- CONNECT : 建立一个到目标资源标识的服务器的隧道  , 通常用在代理服务器
- TRACE :  沿着到目标资源的路径执行一个消息环回测试

# HTTP的版本

- HTTP /1.1
  - 发布于1997年
  - 增加PUT DELETE等方法
  - 采用持久连接 (多个请求可以共用同一个TCP连接)



# HTTP Request Header

- 在 request (请求) 对象的 请求头 中也包含很多有用的信息 , 客户端会默认传递过来一些信息 

- content-type是这次请求携带的数据的类型

  - application/ x-www-form-urlencoded
    - 表示数据被编码成以 ‘&’ 分隔的键 - 值对
      - 同时以 = 分割键和值  key和value
  - application/ json 
    - 表示是一个json类型
  - text / plain :
    - 表示是文本类型
  - application/xml
    - 表示是xml类型
  - multipart / form-date
    - 表示是上传文件

- content-length : 文件的大小长度

- keep-alive

  - http是基于TCP协议的, 但是通常在进行一次请求和响应结束后会立刻中断
  - http1.0 中 如果想要继续保持连接
    -  浏览器请求头中 添加 connection: keep -alive
    - 服务器响应头中  添加 connection: keey-alive

  - http1.1中 , 所有连接默认是connection : keep-alive
    - 不同的web服务器会有不同的保持keep-alive的时间
    - node中默认是5秒, 也就是说这五秒那这个通道一直存在,

- accept-encoding

  - 告知服务器 ,客户端支持的文件压缩格式, 
    - 比如js文件可以使用gzip编码 , 对应 .gz文件

- accept

  - 告知服务器 ,客户端可接受文件的格式类型

- user-agent 

  - 客户端代理 相关的信息

# HTTP Response 响应状态码

- HTTP状态码 (HTTP Status Code) 用来表示HTTP响应状态的数字代码
  - HTTP状态码非常多, 可以根据不同的情况 , 给客户端返回不同的状态码
- 常见HTTP状态码
  - 200 
    - ok
      - 客户端请求成功
  - 201
    - Created
      - POST请求 , 创建新的资源
  - 301
    - Moved Permanently
      - 请求资源的URL已经修改, 响应中会给出新的URL
  - 400
    - Bad Request
      - 客户端的错误 ,服务器无法或者不进行处理
  - 401
    - Unanthorized
      - 未授权的错误 , 必须携带请求的身份信息
  - 403
    - forbidden
      - 客户端没有权限访问, 被拒接
  - 404
    - Not Found
      - 服务器找不到请求的资源
  - 500
    - Internal Server Error
      - 服务器遇到了不知道如何处理的情况
  - 503
    - service Unavailable
      - 服务器不可用, 可能处理维护或者重载状态 , 暂时无法访问

# HTTP Response Header

- 比较少去读取Response
- 常用一个lenght



# AJAX发送请求

- AJAX是异步的JavaScript和XML
  - 它可以使用JSON , XML HTML 和 text文本 等格式发送和接收数据
- 完成AJAX请求
  1. 创建网络请求和AJAX对象, 使用XMLHttpRequest
  2. 监听XMLHttpRequest对象 的 状态的变化 ,或者 监听onload事件(请求完成时触发)
  3. 配置网络请求 (通过open方法)
  4. 发生send网络请求

**对象的属性**

- Response : 获取结果
- readyState : 获取state状态 
- timeout : 给浏览器设置请求服务器时间
  - 浏览器达到过期时间还没有获取到对应的结果时 , `取消本次请求`


# XMLHttpRequest的state状态

- 事实上 ,我们在一次网络请求中看到状态发生了很多次变化
- 状态 : UNSENT
  - 值 : 0
    - 描述 : 代理被创建 ,但尚未调用open() 方法
- 状态 : OPENED
  - 值 : 1
    - 描述 : open() 方法已经被调用
- 状态 : HEADERS_RECEIVED
  - 值 : 2
    - 描述 : send() 方法已经被调用 , 并且头部和状态已经可获取
- 状态 : LOADING
  - 加载中, ResponseText 属性 已经包含部分数据
- 状态 : DONE
  - 下载操作已完成

注意: 这个状态并非是 Http的响应状态 , 而是记录XMLHtppRequest对象的状态变化

- http响应状态通过 status获取

## http响应的状态status

- XMLHttpRequest的state是用于记录xhr对象本身的状态变化 , 并非针对Http的网络请求状态
- 如果我们希望获取Http响应的网络状态 , 可以通过status和statusText来获取



## open()方法的第三个值

通常来说, 网络请求是异步执行的

- 就是在网络请求的过程中, 下面的代码直接执行

将open的第三个参数设置为false时

- 网络请求就变成同步执行
  - 就是说必须在网络请求完成之后, 才会执行下面的代码



# XMLHttpRequest事件监听

- readystatechange : 监听状态的改变
- loadstart : 请求开始
- progress :  一个响应数据包到达 
  - 此时整个Response body 都在Response中
    - 监听响应体的进度的
- abort : 调用xhr.abort() 取消了请求
- error : 发生连接错误
  - 例如 : 域错误, 不会发生诸如404这类的Http错误
- load : 请求成功完成
- timeout : 由于请求超时而取消了该请求
  - 仅发生在设置了timeout的情况下
- loadend :  在load ,error , timeout 或 abort 之后触发

# 响应数据和响应类型他

- 发生了请求后, 我们需要获取对应的结果 ,Response属性
  - XMLHttpRequest对象的Response属性返回响应的正文内容
  - 返回的类型取决于ResponseType的属性设置
- 通过ResponseType可以设置获取的数据类型
  - 如果将ResponseType的值设置为空字符串 ,则会使用“**text**”作为默认值
- 和 ResponseText , ResponseXML的区别
  - 早起通常服务器返回的数据是普通的文本和XML
    - 所有我们通常会通过ResponseText 和 ResponseXML来获取响应的结果
  - 之后将它们转换成JavaScript对象的形式
  - 目前服务器基本返回的都是json数据
    - 所以直接设置为JSON即可

# GET和POST请求传递参数

- 常见的传递给服务器数据的方式有如下几种
  - 方式一 : GET请求的query参数
  - 方式二 : POST请求 x-www-form-urlencoded 格式
  - 方式三 : POST请求 FormFData 格式
  - 方式四 : POST请求 JSON 格式

# 延迟时间timeout和取消请求

- 在网络请求的过程中 , 为了避免过长的时候服务器无法返回数据
  - 通常我们会为请求设置一个超时时间: timeout
    - 当达到超时时间后依然没有获取到数据
      - 那么这个请求会被自动被取消掉
    - 默认值为 0 表示没有设置超时时间
- 我们也可以通过abort方法强制取消请求



# Fetch和Fetch API

- Fetch可以看做是早期的XMLhttpRequest的替代方案
  - 它提供了一种更加现代的处理方案
- Fetch的返回值是一个promise
  - 提供了一种更加优雅的处理结果方式
    - 在请求发生成功时 , 调用resolve回调then
    - 在请求发生失败时 , 调用reject回调catch
- 不像XMLhttpRequest一样, 所有的操作都在一个对象上



## Fetch函数的使用

- input 
  - 定义要获取的资源地址 ,可以是一个URL字符串 ,也可以使用一个Request对象类型(实验性特性)
- init : 其他初始化参数
  - method : 请求使用的方法 
    - get , post
  - header : 请求的头信息
    - 设置传递服务器的类型
  - body : 请求的body信息
    - 传递服务器的内容
