# 认识jQuery

- jQuery : 是一个快速 , 小型且功能丰富的 JavaScript 库
  - 官网对 jQuery的描述
- 使HTML文档遍历 ,操作,事件处理 , 动画和Ajax 之类的事件变得更加简单
- 具有易于使用的APl , 可在多种浏览器中使用
- JQuery 结合多功能性和可扩展性 , 改变了数百万人的编写JavaScript的方法



# 库和框架的概念

- 随着JavaScript的普及
  - JavaScript社区认识到代码中存在非常多相同的逻辑是可复用的
  - 因此社区就开始对这些相同的逻辑的代码封装一个JavaScrip文件中
  - 这个封装好的JavaScript文件就可称为JavaScrip库或JavaScrip框架
- 库
  - JavaScrip库是一个预先编写好并实现了一些特定功能的代码片段的集合
  - 一个库中包含了很多的函数 ,变量等 , 可根据需求引入到项目使用
  - 一些常见的库 有 JQuery day.js和Lodash等
- 框架
  - JaVAScript框架是一个完整的工具集
    - 可帮助塑造和组织你的网站或应用程序
  - 提供一个结构来构建整个应用程序
    - 开发人员在结构的规则内更安全 , 更高效的工作



# JQuery优点和缺点

- 优点
  - 易于学习 : 相对于其他的前端框架 , JQuery更易于学习
  - 它支持JavaScrip的编码风格
  - 少写多做
  - 提供了丰富的功能
  - 提高开发工作效率
  - 跨浏览器支持
- 缺点
  - JQuery代码库一直在增长
    - 自JQuery1.5起超过200KB
  - 不支持组件化开发
  - JQuery更适合DOM操作
    - 涉及到开发复杂的项目时, JQuery能力有限

jquery本质是一个JavaScript库

- 该库包含了 :  DOM操作 选择器 事件处理 动画 和Ajax等核心功能



# 认识CDN

- CDN称之为内容分发网络 
  - CDN它是一组分布在不同地理位置的服务器相互连接形成的网络系统
  - 通过这个网络系统 , 将Web内容存放在距离用户最近的服务器
  - 可以更快 , 更可靠地将web内容发生给用户
  - CDN不但可以提高资源的访问速度 , 还可以分担源站的压力
- 理解CDN
  - CDN会将资源缓存到遍布全球的网站 
    - 用户请求获取资源时
  - 可就近获取CDN上缓存的资源
    - 提供资源访问的速度 , 同时分担源站的压力
- 常见的CDN服务
  - 自己购买的CDN服务 
    - 需要购买开通CDN服务
      - 会分配一个域名
  - 开源的CDN服务
    - 国际上使用比较多的是
      - unpkg JSDelivr CDNjs BootCDN

# 认识jQuery函数

- jQuery是一个工厂函数 ( 别名 $ ) , 
  - 调用该函数 , 会根据传入参数类型来返回匹配到元素的集合
    - 一般把该集合称之为jQuery对象
  - 如果传入假值
    - 返回一个空的集合
  - 如果传入选择器
    - 返回在document中所匹配到元素的集合
  - 如果传入元素
    - 返回包含该元素的集合
  - 如果传入HTML字符串
    - 返回包含新创建元素的集合
  - 如果传入回调函数
    - 返回的是包含document元素集合
      - 并且当文档加载完成会回调该函数
  - 因为函数也是对象, 所以该函数还包含了很多已封装好的方案
    - 如 , jQuery.noConfilct
- jQuery函数的参数
  - jQuery ( selector  [ , content])
    - selector 是 字符串选择器
    - context  是 匹配元素时的上下文
      - 默认值为document

# 认识jQuery对象

- jQuery对象是一个包含所匹配到元素的集合 , 该集合是类数组 ( array-like)对象
  - jQuery对象是通过调用jQuery函数来创建  
  - jQuery对象中会包含 N ( > = 0 ) 个匹配到的元素
  - jQuery对象原型中包含了很多已封装好的方法
    - 例如 DOM操作 , 事件处理 ,动画等方法

## jQuery对象 与 DOM Element的区别

- 获取方式的不同
  - DOM Element 是通过原生方式获取 , 例如 document,querySelector()
  - JQuery对象是通用调用jQuery函数获取, 例如 : jQuery(“”)
- jQuery对象是一个类数组对象 , 
  - 该对象中会包含所选中的DOM Element的集合
- jQuery对象的原型上扩展非常多实用的方法
  - DOM Element 则是W3C规范中定义的方法和属性

## jQuery对象 与 DOM Element 的转换

- jQuery对象转成DOM element
  - .get(index) : 获取 jQuery 对象中索引中的DOM元素
    - index 一个从零开始的整数 指示要检索的元素
    - 如果index超出范围 ( 小于负数元素或等于或大于元素数 )
      - 则返回undefined
  - .get() : 没有参数 , 将返回jQuery对象中所有DOM元素的数组
- DOM Element 转成 jQuery 对象
  - 调用jQuery函数或者$函数
  - 例如 : $ ( 元素 )

# jQuery的选择器

- 通用选择器 ( * )
- 基本选择器 (id , class , 元素)
- 属性选择器 ( [attr] [atrr = ‘value’])
- 后代选择器 (div > span , div span)
- 兄弟选择器 (div + span , div ~ span)
  - 交集选择器 (div.container)	
- 伪类选择器 (:nth-chlid() , :nth-of-type() , :not() )
  - 但不支持状态伪类
    - 如 :hover
- 内容选择器 ( : empty ,  :has(selector) )
  - empty : 指选中的元素没有子元素或文本
  - has : 指选中的元素是否存在某个子元素
- 可见选择器 ( :visible , :hidden )
- jQuery扩展选择器 ( :eq() , :odd() , :even , :first , :last )
- jQuery原型上的方法 , 大部分支持链式调用
  - jQuery方法会继续返回jQuery , 就可以继续调用

****

#   Attribute和property属性

- Attribute属性
  - 如id name class 等 html属性
- property属性
  - 是在属性的原型上面的

**Attribute**

- .attr(attributeName)
  - 获取匹配元素集和中第一个元素的属性值，
  - 底层调用了原生的 getAttribute() API.attr(attributeName, value)
- .attr(attributes)
  - 为每个匹配元素设置一个或多个属性，
  - 底层调用了原生的 setAttribute() API
- .removeAttr(attributeName)
  - 在匹配到元素的集中，给每个元素删除一个属性。
  - 底层调用了原生的 removeAttribute() API

**property**

- .prop(propertyName)
  - 获取匹配到元素集合中第一个元素的属性值
- .prop(propertyName，value)、.prop(propertys)
  - 为每个匹配元素设置一个或多个属性。
- removeProp(propertyName)
  - 删除匹配元素集的属性,( 只能删除用户自定义添加的prop，不能删除元素本身的属性 )。
