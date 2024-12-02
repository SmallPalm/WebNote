# Node.js是什么

官方对Node.js的定义

- Node.js是一个基于V8 JavaScrip引擎的JavaScrip运行时环境
- 也就是说Node.js基于V8引擎来执行JavaScrip的代码
  - 但是不仅仅只有Node.js中不仅仅有V8引擎
- V8引擎可以嵌入到任何C++应用程序中
  - 无论是Chrome浏览器还是Node.js
    - 事实上都是嵌入了V8引擎来执行JavaScrip代码的
- 但是Chrome浏览器中 , 还需要解析, 渲染HTML , CSS等相关渲染引擎
  - 另外还需要提供支持浏览器操作的APl
    - 浏览器自己的事件循环等
- 在Node.js中我们也需要进行一些额为的操作
  - 比如
  - 文件系统读/写 : 对文件 (本地文件) 来进行操作
  - 网络IO :  网络的输入输出, 通讯相关的一些东西 
  - 加密  ,  压缩解压文件等操作

**Node程序是使用什么语言来编写**

- Node程序并没有使用js来程序代码
  - 但Node中有js代码 , 来方便我们做一些调用的方法的时候, 
    - 给我们一些API
  - Node中拥有的语言
    - JS(APl方法)
    - C++ (V8引擎)
    - C语言 (libuv)



## 浏览器和Node的区别

**浏览器和Node.js架构都嵌入了V8引擎**

![image-20231113111715911](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231113111715911.png)

# Node.js架构

- JavaScrip会经过V8引擎 , 在通过Node.js的Bindings
  - 将任务放在Libuv的事件循环中
- Libuv 是使用C语言编写的库
- Libuv 提供了事件循环 , 文件系统读写 , 网络IO , 线程池等内容
- ![image-20231113111729604](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231113111729604.png)

**electron使用JavaScript，HTML和CSS构建跨平台的桌面应用程序框架**

# Node.js的应用场景

1. 前端开发的库都是以Node包的形式来进行管理
2. npm , yarn , pnpm 工具成为前端开发使用最多的工具
3. 越来越多的公司使用Node.js作为Web服务器开发 , 中间件 , 代理服务器
4. 大量的项目需要借助Node.js来完成前后端渲染的同构应用
5. 资深前端工程师需要为项目编写脚本工具
   - 前端工程师编写脚本通常会使用JavaScrip
     - 而不是Python或者shell
6. 很多企业在使用Electron来开发桌面应用程序



# Node的安装

- Node.js是在2009年诞生的 , 目前版本是分别是LTS版本和Current版本
- LTS版本
  - 相对稳定一些, 推荐线上环境使用该版本
  - 公司开发 , 建议选择LTS版本
    - 面向工作 选择LTS版本
-  Current版本
  - 最新的Node版本 ,包含很多新特性
  - 学习使用 , 可以选择Current版本
    - 这些新特性不稳定
      - 不知道那天其中的那个新特性就消失了

## cmd指令

**--help**

- 查看支持程序都支持什么样的命令

**--version**

- 查看程序的版本号

# Nvm-window的指令

- Node版本管理工具 window版本
  - N : MAC OS系统 : 苹果系统电脑
  - Nvm : MAC OS 系统
  - Nvm-window : window系统
- nvm install latest
  - 安装最新的node的版本
- nvm install lts
  - 安装最新的稳定版的node
- nvm list
  - 展示目前安装的所有版本
- nvm use 版本号
  - 切换版本
- nvm install  版本号
  - 可以直接指定具体版本号安装
- nvm uninstall 版本号
  - 删除不需要的版本

# JavaScrip代码执行

-  JS文件执行
- 两种方式
  - 交给浏览器执行
  - 将代码载入到node环境中执行
- 浏览器执行
  - 需要通过让浏览器加载、解析html代码
  - 所以我们需要创建一个html文件
  - 在html中通过script标签 , 引入js文件
  - 当浏览器遇到script标签时
  - 就会根据src加载、执行JavaScript代码
- Node环境执行
  - 首先电脑上需要安装Node.js环境
    - 安装过程中会自动配置环境变量
  - 可以通过终端命令node js文件的方式
    - 来载入和执行对应的js文件；

# Node的REPL

- REPL是Read-Eval-Print Loop的简称
  - 翻译为 : 读取 - 求值 - 输出   循环
- REPL 是一个简单的 , 交互式的编程环境
- 事实上,  浏览器的console就可以看成一个REPL
- Node也给我们提供了一个REPL环境
  - 直接在命令行中输入node然后敲回车

# Node程序传递参数

- 正常情况下执行一个node程序 , 直接跟上我们对应的文件即可
  - node index.js
- 在某些情况下执行node程序的过程中 , 我们可能希望给node传递一些参数
  - node index.js env=development coderLi
    - node index.js 20 30 limingyu : 传递参数

- 从程序中获取到传递的参数
  - 获取参数其实是在process的内置对象中的
  - 如果我们直接打印这个内置对象
    - 其他的一些信息，比如版本、操作系统等
      - 里面包含特别多的信息
  - 其中内置对象process中的argv属性
    - argv是一个数组 , 里面包含了我们传递的参数

## 为什么叫argv

- 在C/C++程序中的main函数中
  - 实际上可以获取到两个参数
- argc :  argument counter的缩写
  - 是传递参数的个数
- argv :  argument vector : 的缩写
  - 传入的是具体参数
  - vector : 向量 ,  矢量  : 在程序中表示的是一种数据结构
- 在C++ ,  Java中都有这种数据结构
  - 是一种数组结构
- 在JavaScrip中也是一个数组 , 里面存储一些参数的信息

# Node的输出

- console.log()
  - 最常用的输入内容的方式
- console.clear
  - 清空控制台
- console.trace
  - 打印函数的调用栈
- 等等



# 全局对象

- Global对象
- module exports require 会在模块化中讲到
- Buffer

## Node中特殊的全局对象

- 有一些全局对象实际上是模块中的变量
  - 只是每个模块都有 , 看来像是全局对象
- \__dirname  __filename exports module require
- \__dirname
  - 获取当前文件所在的路径：
- __filename
  - 获取当前文件所在的路径和文件名称

## 常见的全局对象

- process对象
  - process提供了Node进程中相关的信息
  - 比如Node的运行环境 , 参数信息等
  - 一些环境变量获取到process 的 env中
- Console对象
  - 提供了简单的调试控制台

定时器函数

- 在Node中使用定时器有好几种方式

- **setTimeout(callback, delay[, ...args])**
  - callback在delay毫秒后执行一次
- **setInterval(callback, delay[, ...args])**
  - callback每delay毫秒重复执行一次
- **setImmediate(callback[, ...args])**
  - callbackI / O事件后的回调的“立即”执行
    - 这里先不展开讨论它和setTimeout(callback, 0)之间的区别
    - 因为它涉及到事件循环的阶段问题 : 后期学习
- **process.nextTick(callback[, ...args])**
  - 添加到下一次tick队列中	
    - 具体的讲解，也放到事件循环中说明；



# global对象

- global是一个全局对象
  - 事实上前端我们提到的方法
  - process , console , setTimeout等都有被放到global中
- 在新的标准中还是一个globalThis
  - 也是指向全局对象
  - 类似于浏览器中的window

## global和window的区别

- 在浏览器中
  - 全局变量都是在window上的
    - 比如有document、setInterval、setTimeout、alert、console等等
- 在Node中
  - 我们也有一个global属性
    - 并且看起来它里面有很多其他对象。

- 但是在浏览器中执行的JavaScript代码
  - 如果我们在顶级范围内通过var定义的一个属性
    - 默认会被添加到window对象上

- 但是在node中
  - 我们通过var定义一个变量
    - 它只是在当前模块中有一个变量
      - 不会放到全局中：