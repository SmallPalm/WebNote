# 为什么要搭建本地服务器

- **目前我们开发的代码，为了运行需要有两个操作：**

  - 操作一

    - npm run build，编译相关的代码

    - 操作二
      - 通过live server或者直接通过浏览器
        - 打开index.html代码，查看效果；

- 这个过程经常操作会影响我们的开发效率
  - 我们希望可以做到，当文件发生变化时
    - 可以自动的完成编译和展示

- **为了完成自动编译，webpack提供了几种可选的方式：**
  - webpack watch mode；
  - **webpack-dev-server**（常用）；
  - webpack-dev-middleware；

# webpack-dev-server

- 安装
  - npm install webpack-dev-server -D
- webpack-dev-server
  - 在编译之后不会写入到任何输出文件
  - 而是将 bundle 文件保留在内存中
-  事实上底层webpack-dev-server使用了一个库叫memfs
  - （memory-fs webpack自己写的）
  - 

# 认识模块热替换

- **什么是HMR呢**
  - HMR的全称是Hot Module Replacement
    - 翻译为模块热替换
  -  模块热替换是指在
    - 应用程序运行过程中，替换、添加、删除模块
      - **只是运行修改的内容**
      - 而无需重新刷新整个页面
- **HMR通过如下几种方式，来提高开发的速度**
  - 不重新加载整个页面
    - 这样可以保留某些应用程序的状态不丢失
  -  只更新需要变化的内容
    - 节省开发的时间
  - 修改了css、js源代码
    - 会立即在浏览器更新
      - 相当于直接在浏览器的（控制台）中直接修改样式
- 使用HMR
  - 默认情况下，webpack-dev-server已经支持HMR
    - 我们只需要开启即可（默认已经开启）
  -  在不开启HMR的情况下
    - 当我们修改了源代码之后
    - 整个页面会自动刷新，使用的是live reloading

## **开启HMR**

- 修改webpack的配置

![image-20231127102403349](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127102403349.png)

- 浏览器效果
  - ![image-20231127102729526](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127102729526.png)
- 当我们修改了某一个模块的代码时，依然是刷新的整个页面
  - 这是因为我们需要去指定哪些模块发生更新时，进行HMR
- ![image-20231127102819575](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127102819575.png)



# 框架中HMR

- 在开发其他项目时
  - 我们是否需要经常手动去写入
    - module.hot.accpet相关的API呢
- 开发Vue、React项目
  - 我们修改了组件
    - 希望进行热更新替换
- vue开发中
  - 我们使用vue-loader，此loader支持vue组件的HMR
  - 提供开箱即用的体验
- react开发中
  - 有React Hot Loader
  - 实时调整react组件
    - 目前React官方已经弃用了，改成使用react-refresh

# host配置

- **host设置主机地址：**

  - 默认值是localhost；

  - 如果希望**其他地方也可以访问**，可以设置为 0.0.0.0；

**localhost 和 0.0.0.0 的区别：**

localhost

- 本质上是一个域名
  - 通常情况下会被解析成127.0.0.1;

127.0.0.1

- 回环地址(Loop Back Address)
  - 表达的意思其实是我们主机自己发出去的包
    - 直接被自己接收

- 正常的数据库包经常
  - 应用层 - 传输层 - 网络层 - 数据链路层 - 物理层 ;

- 而回环地址
  - 是在网络层直接就被获取到了
  - 是不会经常数据链路层和物理层的

- 比如我们监听 127.0.0.1时
  - 在同一个网段下的主机中
  - 通过ip地址是不能访问的;

0.0.0.0

- ：监听IPV4上所有的地址
  - 再根据端口找到不同的应用程序;

- 比如我们监听 0.0.0.0时
  - 在同一个网段下的主机中
  - 通过ip地址是可以访问的;

# port、open、compress

- port设置监听的端口，默认情况下是8080

- open是否打开浏览器
  - 默认值是false，设置为true会打开浏览器
  - 也可以设置为类似于 Google Chrome等值
- compress是否为静态文件开启gzip compression
  - 默认值是false，可以设置为true
  - ![image-20231127103953449](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127103953449.png)



# 如何区分开发环境

- 目前我们所有的webpack配置信息都是放到一个配置文件中的：webpack.config.js
  - 当配置越来越多时
    - 这个文件会变得越来越不容易维护
- 并且某些配置是在开发环境需要使用的
- 某些配置是在生成环境需要使用的
  - 当然某些配置是在开发和生成环境都会使用的
    -  所以我们最好对配置进行划分
      - 方便我们维护和管理；

- **在启动时如何可以区分不同的配置呢？**
  - 方案一
    - 编写两个不同的配置文件，开发和生成时，分别加载不同的配置文件即可；
  - 方式二
    - 使用相同的一个入口配置文件，通过设置参数来区分它们

![image-20231127104442676](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127104442676.png)

# 入口文件解析

- 我们之前编写入口文件的规则是这样的：**./src/index.js**
  - 但是如果我们的配置文件所在的位置变成了 config 目录
  - 我们是否应该变成 **../src/index.js**呢
- 如果我们这样编写，**会发现是报错的**
  - 依然要写成 ./src/index.js
- 这是因为入口文件其实是和另一个属性时有关的 **context**
- **context的作用是用于解析入口（entry point）和加载器（loader）：**
  - 官方说法：默认是当前路径
    - 默认应该是webpack的启动目录
  - 另外推荐在配置中传入一个值
  - ![image-20231127104720034](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127104720034.png)

![image-20231127104736821](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127104736821.png)

# 区分开发和生成环境配置

- **这里我们创建三个文件：**
  - webpack.comm.conf.js
  - webpack.dev.conf.js 
  - webpack.prod.conf.j

# webpack-merge

- development(开发环境) 和 production(生产环境) 这两个环境下的构建目标存在着巨大差异 
  - 所以webpack的配置写的差距会非常的大`
- 在**开发环境中**
  - 我们需要强大的 **source map** 和一个有着 **live reloading(实时重新加载)** 
  -  **hot module replacement(热模块替换)** 能力的 localhost server。
- 生产环境目标则转移至其他方面
  - 关注点在于**压缩 bundle、更轻量的 source map、资源优化等**
  - 通过这些优化方式改善加载时间
    - 由于要遵循逻辑分离，我们通常建议为**每个环境编写彼此独立的 webpack 配置**。
- 虽然以上我们将 生产环境 和 开发环境 做了细微区分
  - 但是，请注意，我们还是会遵循**不重复写配置的原则**
  - 保留一个 `"common( 公共 )" 配置`。为了将这些配置合并在一起
- 我们将使用一个名为webpack-merge的工具。此工具会引用 "common" 配置
  - 因此我们不必再在环境特定`env`的配置中编写重复代码。
- 插件使用
- ![image-20231127105330681](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231127105330681.png)