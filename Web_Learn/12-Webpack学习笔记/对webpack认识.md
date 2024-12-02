# Loader和Plugin的不同

主要是功能和作用上存在不同

**Loader用于转换某些类型的模板**

- Loader的主要任务
  - Babel-loader
    - 可以将ES2015(ES6)+的JavaScript语法转换为向后兼容的ES5语法
  - Ts-loader
    - 可以将TypeScript文件转换为JavaScript文件
  - Css-loader
    - 处理CSS文件, 使其可以作为模块导入JavaScript中
    - 配合postCss-loader用于添加自定义Css扩展
  - Style-loader
    - 将打包好的CSS代码以<style>标签的形式插入到HTML文件中
    - style-loader是和css-loader成对出现
- **Loader主要用于转换文件内容, 更好的能够被webpack理解和打包**

**Plugin是Webpack的插件机制**

- Plugin主要在Webpack构建时执行一些自定义的操作: 如: 
  - 压缩代码
  - 处理文件
  - 生成HTML
- Plugin是基于webpack整个构建过程
  - 能够访问到Compilation和Compiler对象
  - 从而执行特定的任务
- **Plugin的目的是为了解决Loader无法实现的其他功能**: 如: 
  - 打包优化
  - 资源管理
  - 环境变量注入
- 在Webpack的不同阶段(生命周期)
  - Plugin会贯穿整个编译周期, 提供特定的功能

Loader : 负责转换文件内容

Plugin : 负责执行webpack构建过程中的自定义操作和优化等任务

****



# Webpack到底是什么

- webpack是一个静态的模块化打包工具, 为现代的JavaScript应用程序

- 我们来对上面的解释进行拆解

  - 打包 : bundler : webpack可以帮助我们进行打包, 所以它是一个打包工具
  - 静态的 : static : 这样表述的原因是我们最终可以将代码打包成最终的静态资源(部署到静态服务器中)
  - 模块化: module : webpack默认支持各种模块化开发 , ES Module , CommonJS , AMD等
  - 现代的 : modern : 我们前端说过, 正是因为现代前端开发面临各种各样的问题
    - 才催生了WebPack的出现和发展

  

  

# Mode配置

Mode配置 : 可以告知webpack使用相对应模式的内置优化

- 默认值 : production :  生成环境
- 可选值 : none | development : 开发环境 | production 



