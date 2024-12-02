# 目前前端开发的架构图

![image-20231120155007569](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231120155007569.png)



# 内置模块path

- path模块用于对路径和文件进行处理 , 提供了很多好用的方法
- Mac OS , Linux 和 window上的路径是不一样的
  - window上会使用 \或者 \\\来作为文件路径的分隔符
    - 当然目前也支持 /
  - 在Mas OS , Linux 的Unix操作系统上使用 / 来作为文件路径的分隔符
- 当我们的代码路径是 使用 window上支持路径 分隔符
  - 当我们在将代码部署到Mas OS系统 会出现问题
- 在window上使用 \ 来作为分隔符开发了一个应用程序
  - 要部署到Linux上面时应该怎么办
  - 显示路径会出现一些问题
- 所以为了屏蔽他们之间的差异
  - 在开发中对于路径的操作我们可以使用path模块
- 可移植操作系统接口
  - Portable Operating System Interface 缩写为POSIX
  - Linux 和Mac OS都实现了POSIX接口
  - window部分电脑实现了POSIX接口

# path常见的API

- 从路径中获取信息
  - dirname : 获取文件的父级文件夹
  - basename : 获取文件名
  - extname : 获取文件扩展名
- 路径的拼接 : path.join
  - 如果我们希望将多个路径进行拼接
    - 但是不同的操作系统可能使用的是不同的分隔符
  - 这个时候我们可以使用path.join函数
- 拼接绝对路径 : path.resolve
  - path.resolve () 方法会把一个路径或路径片段的序列解析为一个绝对路径
  - 给定的路径的序列是从右往左被处理的
    - 后面每个path被依次解析
    - 直到构造完成一个绝对路径
  - 如果在处理完所有给定path的段之后
    - 还没有生成绝对路径
    - 则使用当前工作目录
  - **生成的路径被规范化并删除尾部斜杠**
    - 零长度path段被忽略
- 如果没有path传递段 , path.resolve() 将返回当前工作目录的绝对路径
- 斜杠\前面没有点 ,那么他本身就是一个绝对路径
- 如果没有指定磁盘, 那么会找到自身文件的所在的磁盘
- 斜杠\前面两个点, 找到的是他的上上层目录



# 认识webpack

事实上随着前端的快速发展

- 目前前端的开发已经变的越来越复杂了

- 比如开发过程中我们需要**通过模块化的方式来开发**
- 比如也会使用一些**高级的特性来加快我们的开发效率或者安全性**
- 比如**通过ES6+、TypeScript开发脚本逻辑**
  - 通过sass、less等方式来编写css样式代码
- 比如开发过程中
  - 我们还希望**实时的监听文件的变化来并且反映到浏览器上**
    - 提高开发的效率
- 比如开发完成后我们还需要**将代码进行压缩**
  - **合并以及其他相关的优化**

但是对于很多的前端开发者来说 ,并不需要思考这些问, 日常的开发中根本就没有面临这些问题

- 这是因为目前前端开发
  - 我们通常都会直接使用三大框架开发
    - **Vue、React、Angular**
- 但是事实上
  - 这三大框架的创建过程我们都是**借助于脚手架（CLI）**的
- 事实上**Vue-CLI、create-react-app、Angular-CLI**
  - 都是基于webpack来帮助我们构建模块化、less、TypeScript、打包优化等
- 这是因为webpack支持模块化、less、TypeScript、打包优化等

## 脚手架依赖webpack

- **Vue-CLI、create-react-app、Angular-CLI**
  - 都是依赖于webpack

## webpack理解

- webpack是一个静态的模块化打包工具
  - 提供于现代的JavaScript应用程序
  - 模块化 
    - 支持ES6版本的ESmodule
    - 支持Node中的CommonJS
- 打包 : bundler
  - webpack 可以将帮助我们进行打包
    - 所以他是一个打包工具
- 静态的 : static
  - 这样表述的原因是我们最终可以将代码打包
    - 打包后的代码最终是一个静态资源
      - 部署到静态服务器
- 模块化 : module
  - webpack默认支持各种模块化开发
    - ES Module
    - CommonJS
    - AMD , CMD等
- 现代的 : modern
  - 目前前端的开发已经变的越来越复杂了
    - 才催生了webpack的出现和发展

## 打包过程

![1700484579332](D:\WX\WeChatFiles\WeChat Files\wxid_setv95mitnio22\FileStorage\Temp\1700484579332.png)



# Vue项目加载的文件

- JavaScript的打包
  - 将ES6转换成ES5的语法
  - TypeScript的处理 将其转换成JavaScript
- CSS的处理
  - CSS文件模块的加载 , 提取
  - Less , Sass 等预处理器的处理
- 资源文件img , font : 
  - 图片img文件的加载
  - 字体font文件的加载
- HTML资源的处理
  - 打包HTML资源文件
- 处理Vue项目的SFC文件 , Vue文件 ;



## Webpack的使用

Webpack的运行是依赖Node环境的，所以我们电脑上必须有Node环境

- 从webpack4版本开发需要安装两个
  - 安装目前分外两个 : webpack , webpack-cli
- webpack-cli : 在命令行使用webpack必须要用的东西

## webpack , webpack-cli关系

- 在命令行执行webpack命令
  - 会执行node_modules下的.bin目录下的webpack
  - **webpack在执行时是依赖webpack-cli**的 ,如果没有安装就会报错
  - **而webpack-cli中代码执行时  , 才是真正利用webpack进行编译和打包的过程**
  - 所以在安装webpack时 , 我们需要同时安装webpack-cli
  - 第三方的脚手架事实上是没有使用webpack-cli的
    - 而是类似自己的vue-service-cli的东西
- ![image-20231120211231661](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231120211231661.png)

# Webpack的默认打包



- 在目录下的命令行中直接执行 webpack 命令
  - npx webpack
- 生成一个dist文件夹
  - 里面存放一个main.js的文件
  - 就是我们打包之后的文件
- 这个文件中的代码被压缩和丑化了
  - 另外我们发现代码中依然存在ES6的语法
  - 比如箭头函数、const等
  - 这是因为默认情况下webpack并不清楚我们打包后的文件
    - 是否需要转成ES5之前的语法
- 后续我们需要通过babel来进行转换和设置

我们发现是可以正常进行打包的

- webpack是如何确定我们的入口的呢
- 事实上，当我们运行webpack时
- webpack会查找当前目录下的 src/index.js作为入口
  - 所以，如果当前项目中没有存在src/index.js文件，那么会报错
- 当然，我们也可以通过配置来指定入口和出口
  - npx webpack --entry ./src/main.js --output-path ./build
  - --entry ./src/main.js : 入口
  - --output-path ./build : 出口

## 创建局部的webpack

- 第一步：创建package.json文件，用于管理项目的信息、库依赖等
  - npm init
- 第二步：安装局部的webpack
  - npm install webpack webpack-cli -D
- 第三步：使用局部的webpack
  - npx webpack
- 第四步：在package.json中创建scripts脚本，执行脚本打包即可
  - ![image-20231120215019960](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231120215019960.png)
  - npm run build

# Webpack配置文件

- 在通常情况下，webpack需要打包的项目是非常复杂的
  - 并且我们需要一系列的配置来满足要求，默认配置必然是不可以的

- 我们可以在根目录下创建一个webpack.config.js文件
  - 来作为webpack的配置文件
  - ![image-20231120215130996](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231120215130996.png)
- 继续执行webpack命令，依然可以正常打包

但是如果我们的配置文件并不是webpack.config.js的名字，而是其他的名字呢

- 比如我们将webpack.config.js修改成了 lmy.config.js；
- 这个时候我们可以通过 --config 来指定对应的配置文件
  - webpack --config lmy.config.js
- 但是每次这样执行命令来对源码进行编译会非常繁琐
  - 所以我们可以在package.json中增加一个新的脚本
  - ![image-20231120215247649](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231120215247649.png)
  - 之后我们执行 npm run build来打包即可

# Webpack的依赖图

- ![1700484579332](D:\WX\WeChatFiles\WeChat Files\wxid_setv95mitnio22\FileStorage\Temp\1700484579332.png)

- 事实上webpack在处理应用程序时
  - 它会根据命令或者配置文件找到入口文件
- 从入口开始，会生成一个 依赖关系图
  - 这个依赖关系图会包含应用程序中所需的所有模块
  - 比如.js文件、css文件、图片、字体等
- 然后遍历图结构，打包一个个模块
  - 根据文件的不同使用不同的loader来解析

# webpack 的五个概念

- ### Entry

  - 入口指示 webpack 以哪个文件为入口起点开始打包，分析构建内部依赖图

- ### Output

  - 输出指示 webpack 打包后的资源 bundles输出到哪里去，以及如何命名

- ### Loader

  - Loader 让 webpack 能够处理那些非 javascript 文件（webpack 自身只理解 javascript）

- ### Plugins

  - 插件（Plugins）可以用于执行范围更广的任务，插件的范围包括：从打包优化和压缩，一直到重新定义环境中的变量等。

- ### Mode

  - mode 指示 webpack 使用相应的模式配置
    - 开发环境
    - 生产环境