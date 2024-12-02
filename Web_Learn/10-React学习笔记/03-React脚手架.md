babel, webpack, gulp, 配置它们的转换规则,  打包依赖, 热更新等

# 前端脚手架

三大框架

- Vue :  @Vue/cli ; @vite
- Angular : @angular/cli
- React : creat-react-app



# PWA

- PWA 全称 Progressive Web App 
  -  称之为**渐进式Web应用**
- 一个PWA应用首先是一个网页
  - 通过Web技术编写出一个网页应用
- PWA更主要是应用在手机端的快应用
  - 生成软件图标
  - 其内在是一个Web页面组件的软件
- 并且拥有App Manifest 和 Service Worker来实现PWA的安装和离线功能
  - 离线存储缓存

 

# 脚手架中的WebPack

- React的脚手架是基于webpack来开发的
- 但创建出来的工程化项目并没有WebPack的身影
  - React脚手架将Webpack相关的配置隐藏起来了
    - (从Vue Cli3开始, Webpack也进行了隐藏)
- 如果我们希望看到webpack的配置信息
  - 可以执行一个package.json文件中的一个脚本
    - "eject": "react-scripts eject"
  - 这个操作是不可逆的

## 脚手架隐藏Webpack原因

- 主要原因是**简化开发流程**和**提高开发效率**

- Webpack是一个功能强大的工具
- 用于将各种前端资源（如JavaScript、CSS、图片等）打包成静态资源
  - 但是，Webpack的配置相对复杂
  - 包括各种loader、plugin配置等
  - 对于新手来说学习成本较高
    - 而且配置过程中可能出现各种错误。

- 为了让开发者专注于业务逻辑而不是配置Webpack
  - 前端社区逐渐倾向于使用脚手架工具来隐藏Webpack的配置
- 隐藏Webpack配置是为了降低前端开发的学习曲线和复杂度，使开发者可以更专注于业务逻辑的实现。

Vue CLI是在3.0版本开始隐藏Webpack配置的

Create React App则是从一开始就实现了Webpack配置的隐藏。