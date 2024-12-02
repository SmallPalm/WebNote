# 认识Plugin

- webpack的另一个核心是Plugin , 官方有这样一段对Plugin的描述
  - Loader是用于**特定的模块类型进行转换**
    - 当我们去打包其他文件时 , loader所进行的转换
  - Plugin可以用于执行**更加广泛的任务**
    - 比如打包优化 , 资源管理, 环境变量注入等

# Clean

- 每次修改了一些配置 ,重新打包时 , 都需要手动删除dist文件夹
  - 如果想每一次打包之前自动删除上一次打包的文件夹
- 在output出口中
  - 设置Clean为true即可

# HtmlWebpackPlugin

- Plugin插件
- 我们的HTML文件是编写在根目录下的
  - 而最终打包的dist文件夹中是没有index.html文件的
- 在进行**静态服务器部署项目**时
  - 必然也是需要有对应的入口文件index.html
- 所以我们也需要对index.html进行打包处理
- 需要使用在plugin中使用HtmlWebpackPlugin插件
  - npm install html-webpack-plugin -D

## 生产index.html分析

- 我们会发现，使用html插件 , 
  - 现在自动在dist文件夹中
    - 生成了一个index.html的文件
  - 该文件中也自动添加了我们打包的bundle.js文件
- 这个文件是如何生成的呢
  - 默认情况下是根据ejs的一个模板来生成
  - 在html-webpack-plugin的源码中
    - 有一个default_index.ejs模块

## 自定义html模板

- 如果我们想在自己的模块中加入一些比较特别的内容
- 比如在开发vue或者react项目时，
  - 我们需要一个可以挂载后续组件的根标签 <div id="app"></div>
-  在配置HtmlWebpackPlugin时，我们可以添加如下配置
  - **template：**指定我们要使用的模块所在的路径
  - **title：**在进行htmlWebpackPlugin.options.title
    - 读取时，**就会读到该信息**

# DefinePlugin

- **DefinePlugin允许在编译时创建配置的全局常量**
  - **是一个webpack内置的插件（不需要单独安装）**
  -  这个时候，
    - 编译template就可以正确的编译了会读取到BASE_URL的值
- **在插件中可以配置项目的全局变量**
- DefinePlugin有一个默认属性
  - proces.env.NODE_ENV
    - 值为开发环境或生产环境

# Mode配置

- 主要告知webpack使用相应模式的内置优化
  - 默认值是Production
  - 可选值
    - none
    - development
      - 会将proces.env.NODE_ENV的值设置为development
    - production
      - 会将proces.env.NODE_ENV的值设置为production