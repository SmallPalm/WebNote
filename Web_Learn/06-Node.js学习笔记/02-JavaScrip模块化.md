# 认识模块化开发

模块化开发

- 事实上模块化开发最终的目的是将程序代码分层一个个小的结构
- 这个结构中编写属于自己的逻辑代码
  - 有自己的作用域
  - 定义变量名词时不会影响其他的程序代码结构
- 这个结构可以将自己希望暴露的变量 , 函数 , 对象等导出
  - 给其他结构使用, 并且不影响其他结构中相同的变量, 函数, 对象等
- 也可以通过某种方式 , 导入另外结构中的变量 , 函数 , 对象等

**上面所提到的结构就是模块**

- 按照这种结构划分开发程序的过程 , 就是模块化

## JavaScript的缺陷

- 比如Var定义的变量作用域问题
- 比如JavaScript的面向对象并不能像常规面向对象语言一样使用class
- JavaScript没有模块化的问题

# 模块化的历史

- 在网页开发的早期 , Brendan Eich开发JavaScript仅仅作为一种脚本语言
  - 做一些简单的表单验证或动画实现等
    - 那个时候代码还是很少
- 这个时候我们只需要讲JavaScript代码写到</script>标签中即可
  - 并没有必要放到多个文件中来编写
    - 甚至流行：通常来说 JavaScript 程序的长度只有一行
- 但是随着前端和JavaScript的快速发展
  - JavaScript代码变得越来越复杂了
- Ajax的出现
  - 前后端开发分离, 意味着后端返回数据后
    - 我们需要通过JavaScript进行前端页面的渲染
- SPA的出现
  - 前端页面变得更加复杂了 
    - 包括前端路由 , 状态管理等等一系列复杂的需求
      - 需要通过JavaScript来实现
- 包括Node的实现
  - JavaScript编写复杂的后端程序 , 没有模块化的致命的硬伤
- 所有模块化开发已经是JavaScript一个非常迫切的需求
  - 但是JavaScript本身 , 直到ES6 (ES2015) 才推出了自己的模块化方案
  - 在此之前 ,为了让JavaScript支持模块化 , 涌现出了很多不同的模块化规范
    - AMD , CMD , CommonJS等

## 没有模块化带来的问题

1. 文件中的命名冲突
   - 解决办法:使用立即函数调用IIFE
2. 必须记得每一个模块中返回对象的命名
   - 才能在其他模块使用过程中正确的使用
3. 代码写起来混乱不堪
   - 每个文件中的代码都需要包裹在一个匿名函数中来编写
4. 在没有合适的规范情况下,  每个人,  每个公司都可能会任意命名
   - 甚至出现模块名称相同的情况

- 我们会发现，虽然实现了模块化
  - 但是我们的实现过于简单，并且是没有规范的。
- 我们需要制定一定的规范来约束每个人都按照这个规范去编写模块化的代码
  - 这个规范中应该包括核心功能
    - **模块本身可以导出暴露的属性**
      - **模块又可以导入自己需要的属性**
- JavaScript社区为了解决上面的问题
  - 涌现出一系列好用的规范
    - CommonJS , AMD , CMD



# CommonJS规范和Node关系

- 我们需要知道CommonJS是一个规范
  - 最初提出来是在浏览器以外的地方使用
    - 并且当时被命名为ServerJS
  - 但后来为了体现ServerJS的广泛性
    - 修改为CommonJS
      - 简称CJS
- Node 是CommonJS在服务器端一个具有代表性的实现
- Browserify 是CommonJS 在浏览器中的一种实现
  - Browserify:现在已经不用了
- Web Pack打包工具具备对CommonJS的支持和转换

Node中对CommonJS进行了支持和实现

- 开发中使用Node的过程中可以方便的进行模块化开发
  - 在Node中每一个JS文件都是一个单独的模块
  - 在这个模块中包括CommonJS规范的核心变量
    - Exports : 导出暴露的属性
    - Module.exports 
    - Require : 导入自己需要的属性 
  - 可以使用这些变量来方便的进行模块化开发
- 模块化的核心是导出和导入 , Node中对其进行了实现
  - exports和module.exports
    - 可以负责对模块中的内容进行导出
  - require函数
    - 可以帮助我们导入其他模块
    - （自定义模块、系统模块、第三方库模块）中的内容



# exports导出

- 注意 : exports是一个对象，
  - 我们可以在这个对象中添加很多个属性
    - 添加的属性可以被导出 ,被其他模块获取
    - ```js
      //util.js
      let name = "limingyu"
      exports.name = name
      ```
    
  - 另外一个文件中可以导入
  
    - ```js
      //main.js
      const util = require("./util.js")
      //重构
      const {name} = require("./util.js")
      ```
  
- 意味着main中的util变量等于exports对象

- 也就是require通过各种查找方式 , 最终找到了exports这个对象

- 并且将这个exports对象赋值给util变量

- util变量就是exports对象了

exports的本质

- exports和require指向是同一个对象 : 引入赋值

**模块 : 在node中每一个JS文件都可以是一个模块**

# Module.exports导出

- 但是Node中我们经常导出东西的时候
  - 又是通过Module.exports导出的
- exports 和 Module.exports 有什么关系或者区别那
- 通过维基百科对CommonJS规范的解析
  - CommonJS中是没有Module.exports的概念的
  - 但是为了实现模块的导出
    - Node中使用的是Module的类
      - **每一个模块都是Module的一个实例**
        - **也就是module**
  - 所以在Node中真正用于导出的其实根本不是exports
    - 而是Module.exports
- 但是, exports也可以导出
  - 这是因为Module对象的exports属性是exports对象的一个引用
  - 也就是说 Module.exports = export



1. 1.在三者项目引用的情况下，修改exports中的name属性到底发生了什么
   - **三者项目引用的情况下 , 谁修改对象中的属性 , 其他的项目都会发生改变**
2. 2.在三者引用的情况下，修改了main中的bar的name属性，在bar模块中会发生什么
   - bar模块中的对象的属性就会发送改变
3. 3.如果module.exports不再引用exports对象了，那么修改export还有意义吗？
   - 没有意义 , 已经根本用不到了



# require导入

- require是一个函数 , 可以帮助我们引入一个文件 (模块) 中导出的对象

require的查找规则

- 导入格式
  - require(X)

**情况一**

- X是一个Node核心模块 , 比如 path , http
  - 直接返回核心模块 , 并且停止查找
  - Node核心模块 : Node中的内部内置的模块

**情况二** 

- X是以 ./ 或 ../ 或  / (根目录) 开头的
- 第一步 : 将X当做一个文件在对象的目录下查找
  - 如果有后缀名
    - 按照后缀名的格式查找对应的文件
  - 如果没有后缀名 : 查找文件后缀名的顺序
    1. 将会直接查找文件X
    2. 查找文件X.js文件
    3. 查找文件X.json文件
    4. 查找文件X.node文件
- 当第一步没有找到对应的文件 , 将X作为一个目录
  - 查找目录下面的index文件
    1. 查找X / index.js文件 
    2. 查找X / index.json文件
    3. 查找X / index.node文件

**情况三**

- 情况一和情况二没有找到
- 在会从内到外, 一层一层目录查找node.modules文件夹
  - 查找node.modules文件夹**中的含X的文件夹或文件**
    - 如果找到文件夹或文件**再通过情况二查找**
- 查找node.modules文件夹路径
  - ![image-20231115115359336](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231115115359336.png)
- 如果上面的路径中都没有找到，那么报错：not found

# 模块的加载过程

结论一

- 模块在被第一次引入时 , 模块中的JS代码会被执行一次

结论二

- 模块被多次引入时 , 会被缓存, 最终只加载(运行)一次
  - 模块只会加载运行一次
  - 这是因为每个模块对象module都有一个属性 : loaded
  - 为false表示还没有加载
  - 为true表示已经加载了
    - 当模块加载运行一次后, loaded就会从false变为true
    - 模块第二次加载运行时,  loaded已经为true, 就不会执行了

结论三

- 如果有循环引入 , 那么加载顺序是使用一种数据结构
  - 图结构
- 图结构在遍历的过程中 , 有深度优先搜索 和 广度优先搜索
  - Node采用的是深度优先算法
  - ![image-20231115144139574](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231115144139574.png)
  - 执行顺序: main -> aaa -> ccc ->ddd -> eee -> bbb
  - 解析aaa文件时, 发现有导入其他文件, 就进入其他文件解析
    - 直到没有文件, 返回main文件执行下一行代码
      - 模块执行过后 , 在通过bbb文件导入解析, 也不会再执行解析

# CommonJS规范缺点

- CommonJS加载模块是同步的
  - 同步的意味着只有等到对应的模块加载完毕
    - 当前模块中的内容才能被运行
  - 这个在服务器不会有什么问题
    - 因为服务器加载的js文件都是本地文件
      - 加载速度非常快
- 如果将它应用于浏览器呢
  - 浏览器加载js文件需要先从服务器将文件下载下来
    - 之后再加载运行
  - 那么采用同步的就意味着后续的js代码都无法正常运行
    - 即使是一些简单的DOM操作
- 所以在浏览器中 ,我们通常不使用CommonJS规范
  - 当然在webpack中使用CommonJS是另外一回事
    - 因为它会将我们的代码转成浏览器可以直接执行的代码
- 在早期为了可以在浏览器中使用模块化
  - 通常会采用AMD或CMD

- 但是目前一方面现代的浏览器已经支持ES Modules
  - 另一方面借助于webpack等工具可以实现对CommonJS或者ES Module代码的转换
    - 所以AMD和CMD已经使用非常少了

# AMD规范

- AMD主要是应用于浏览器的一种模块化规范
  - AMD是Asynchronous Module Definition（异步模块定义）的缩写
    - 它采用的是异步加载模块
  - 事实上AMD的规范还要早于CommonJS
    - 但是CommonJS目前依然在被使用
      - 而AMD使用的较少了
- 我们提到过
  - **规范只是定义代码的应该如何去编写**
    - 只有有了具体的实现才能被应用
- AMD实现的比较常用的库是require.js和curl.js；

# CMD规范

- CMD规范也是应用于浏览器的一种模块化规范
  - CMD 是Common Module Definition（通用模块定义）的缩写
    - 它也采用的也是异步加载模块
- 但是它将CommonJS的优点吸收了过来
  - 但是目前CMD使用也非常少了
- CMD也有自己比较优秀的实现方案：**Sea.JS**
