**域名请求服务器 , 需要IP地址 , DNS解析域名 , 转成IP地址 , 根据IP地址 , 找到服务器, 向服务器发起请求 , 在返回html页面**

# 浏览器的渲染

服务器传输解析的时候 , 只会html文件 , css和js文件都是在html里面在开始解析

服务器先请求一个index.html文件

- 在解析的过程中 , 如果当遇见html文件里面有
  - link的css文件
    - 在解析css文件
  - script文件
    - 在解析script文件



# 浏览器的内核

负责解析网页语法，并渲染（显示网页）

- Trident（三叉戟）：IE、360安全浏览器、搜狗高速浏览器、百度浏览器、UC浏览器
-  Gresto（壁虎）：Mozilla Firefox
- Webkit：Safari 、360急速浏览器、搜狗高速浏览器、移动浏览器、（安卓、IOS）
- Webkit->Bink：  Google  Chorme、  Edge

**不同的浏览器内核有不同的解析、渲染规则，所以同一网页不同内核的浏览器种的渲染效果也可能不同**。



render tree : 渲染树

- 浏览器先加载html , 从上外下 , 一行一行解析 , 
- 如果遇到了css , 加载对应的css  , 还会继续解析html
- 加载完成css在添加(attach)上给解析完成的html
- 然后在展示出来

![浏览器渲染](D:\OneDrive\桌面\浏览器渲染.jpg)

1. html经过解析生成DOM tree
2. css经过解析生成各种的规则树, CSSOM 
3. 给他应用到dom tree
4. 就会生成一个渲染层 , render tree
   1. layout , 对我们的render tree 来进行处理 
      1. 他进行的是记录个个节点的位置 , 大小 , 布局
      2. 每一个节点的位置大小就确定下来的
   2. painting : 展示

DOM : 对我们DOM Tree进行操作

- link元素不会阻塞DOM Tree的构建过程 , 但是会阻塞render Tree的构建过程
  - 这是因为render Tree在构建时 , 需要对应的CssOM Tree
- render Tree和DOM Tree并不是一一对应的关系
  - 比如对与display为none时的元素的css样式
    - 根本不会出现在render Tree中
- render Tree不会表示每个节点的尺寸 , 位置的信息
  - 布局 layout就是来确定呈现树中所有的节点的宽度, 高度和位置信息
- painting 转成屏幕上实际的像素点\



### 回流和重绘

- 回流reflow : (重排)
  - 第一次确定节点的大小和位置 , 称之为布局(layout)
  - 之后对节点的大小 , 位置修改计算称之为回流
- 什么情况引起回流
  - DOM结构发生改变(添加或移除节点)
  - 改变布局
  - 改变窗口尺寸
  - 调用getcomputedstyle方法获取尺寸 , 位置
    - 非常消耗浏览器性能
- 重绘 repaint
  - 第一个渲染内容称之为绘制
    - 之后重新渲染称之为重绘

1. 在开发中要尽量避免发生回流
   - 修改样式时, 尽量一次性修改
     - 比如通过css Text修改
     - 通过class修改
   - 尽量避免频繁的操作DOM
     - 可以在documentFragment或者父元素中将要操作的DOM操作完成 , 在一次性的操作
   - 尽量避免通过getComputedStyle获取尺寸位置等信息
   - 对某些元素使用position的absolute 或者fixed
     - 并不是不会引起回流 , 而是开销相对比较小,
       - 不会对其他元素造成影响

## 特殊解析 一 composite合成

- 绘制的过程 , 可以将布局后的元素绘制到多个合成图层中
  - 这是浏览器的一种优化手段
- 默认情况下 , 标准流的内容都是被绘制在同一个图层(layout)中的
- 而一些特殊的属性 , 会创建一个新的合成层 ,   并且新的图层可以利用GPU来加速绘制
  - 因为每一个合成层点都是单独渲染的
- 常见单独合成层
  - **3D transforms**
  - **video , canvas , iframe**
  - **opacity** : 动画效果发生时, 才会转变
  - **position: fixed**
  - **will - change** : 实验性的属性 , 提前告诉浏览器元素可以发生那些变化
  - **animation  / transform**设置了**opacity , transform**
- 分层确实可以提高性能, 但是它以内存管理为代价
  - 因此不应作为web性能优化策略的一部分 , 过渡使用

# script元素和页面解析的关系

- 浏览器在解析html的过程中 , 遇到script元素是不能继续构建DOM树的
- 停止继续构建 , 首先下载JavaScript代码 , 并执行JavaScript脚本
- 等到JavaScript脚本执行完成 , 在继续解析html , 创建DOM树

#### 为什么怎么做

- 因为JavaScript的作用之一就是操作DOM, 并且可以修改DOM
  - 等到DOM树构建完成并且渲染再执行JavaScript, 会造成严重的回流和重绘,  影响页面的性能
- 所有当遇到script元素时, 优先执行和下载JavaScript代码 , 在继构建DOM树

#### 新的问题

- 目前的开发模式中 , 脚本往往比html页面更 “重” , 处理时间需要更长
- 这样会造成页面的解析堵塞 , 在脚本下载 ,执行完成之前 , 用户在界面上什么都看不到

解决问题

- script元素给我们提供了两个属性(attribute):  **defer : async**

## defer属性

- 告诉浏览器不要等待脚本下载 , 而继续解析html , 构建DOM Tree
  - 脚本会由浏览器来进行下载，但是不会阻塞DOM Tree的构建过程
  - 如果脚本提前下载好了，它会等待DOM Tree构建完成，在DOMContentLoaded事件之前先执行defer中的代码
  - ![image-20240129111213036](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240129111213036.png)

- 另外多个带defer的 脚本是可以保存正确的顺序执行的
- defer可以提供页面性能 , 并且推荐放到head元素中
- defer仅适用外部元素 , 对于script默认内容会被忽略

##   async属性

- 特性与defer类似
- 是让一个脚本完全独立的
  - 浏览器不会因async脚本而阻塞
  - async不会能保证在DOMContentLoaded之前或者之后执行
  - 不能保证顺序
  - 它是独立下载 , 独立执行, 不会等待其他脚本
- ![image-20240129111237341](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240129111237341.png)

**defer**通常用于需要再文档解析后操作DOM的JavaScript代码,并且对多个script文件有顺序要求

**async**通常用于独立的脚步 , 对其他脚本 , 甚至DOM没有依赖的
