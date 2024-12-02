# 跨平台开发

- 传统移动端开发方式
  - 移动端开发主要由 iOS 和 Android 这两大平台占据
  - 早期的移动端开发人员主要是针对 iOS 和 Android 这两个平台分别进行同步开发
  - 原生开发模式优点
    -  原生App在体验、性能、兼容性都非常好, 并可以非常方便使用硬件设备，比如：摄像头、罗盘
  - 原生开发模式缺点
    - 但是同时开发两个平台，无论是成本上，还是时间
      - 对于企业来说这个花费都是巨大，不可接受的。 
    - 纯原生 开发效率 和 上线周期 也严重影响了应用快速的迭代，也不利于多个平台版本控制等
- 跨平台开发的诞生
  - 因为原生App存在：时间长、成本高、迭代慢、部署慢、不利于推广等因素
  - 因此 “**一套代码，多端运行**” 的跨平台理念也应运而生

# 原生VS跨平台

- 原生开发的特点
  - 性能稳定，使用流畅，用户体验好、功能齐全，安全性有保证，兼容性好，可使用手机所有硬件功能等 
  -  但是开发周期长、维护成本高、迭代慢、部署慢、新版本必须重新下载应用 
  - 不支持跨平台，必须同时开发多端代码
- 跨平台开发的特点
  - 可以跨平台，一套代码搞定iOS、Android、微信小程序、H5应用等 
  - 开发成本较低，开发周期比原生短 
  -  **适用于跟系统交互少、页面不太复杂的场景**。 
  -  但是对开发者要求高，除了本身JS的了解，还必须熟悉一点原生开发
  - **不适合**做高性能、复杂用户体验，以及定制高的**应用程序**
    - 比如：抖音、微信、QQ等。 
  -  同时开发多端兼容和**适配比较麻烦**、调试起来不方便。

# 跨平台技术

- ReactNative（跨平台框架）
- Weex
- Flutter
  - Dart语言
- 微信小程序
- uni-app
- Taro

# main.js文件

- Uniapp的入口文件
  - 初始化Vue的实例
  - 定义全局组件
  - 定义全集属性
  - 安装插件: 如pinia, Vuex等

# App.Vue文件

- Uniapp 的入口组件

  - 所有页面都是在App.Vue下进行切换
  - App.Vue本身不是页面
    - 不能编写视图元素
    - 没有Template元素

- 作用

  - 应用(小程序)的生命周期
    - onLaunch
    - onShow
    - onHide
    - 应用生命的周期**仅可在App.vue中监听**，在页面监听无效
  - 编写全局样式
    - App.vue 中通过 @import 语句可以导入外联样式
      - 一样作用于每一个页面
  - 定义全局数据GlobalData

  #  uni.scss 文件

  - 用来编写全局公共样式，通常用来定义**全局样式变量**
  - 在uni.scss中定义的变量
    - 无需 @import 就可以在任意组件中直接使用
    - 使用uni.scss中的变量，需在 HBuilderX 里面安装 scss 插件
    - uni.scss定义的变量是全局可以直接使用
    - App.vue定义的变量只能在当前组件中使用
  
  # 页面调用
  
  - getApp()函数
  
    - 用于获取当前应用实例, 可用于获取globalData对象
  
      ```vue
      // App.Vue页面
      export default {
      	onLaunch: function(options) {}
      	onShow: function(options) {}
      	onHide: function() {},
      	globalData: {}
      }
      
      
      //子页面: 组件
      const app = getApp()
      console.log(app.globalData)
      ```
  
- getCurrentPages()

  - 用于获取当前页面栈的实例
    - 以数组的形式按栈的顺序给出
      - 栈是先进后出
      - 数组：第一个元素为首页，最后一个元素为当前页面。
  - 仅用于展示页面栈的情况, 不能改变页面栈,  会造成页面状态错误

- page.$getAppWebview()
  - 获取当前页面的webView对象实例
- page.route
  - 获取当前页面的路由

# page.json

- page.json全局页面配置
  - pages.json 文件用来对 uni-app 进行全局配置
    - 类似微信小程序中app.json。
  - 决定页面的路径、窗口样式、原生的导航栏、底部的原生tabbar 等

# 条件编译

- \#ifdef：if defined 仅在某平台存在
- #ifndef：if not defined 除了某平台均存在
-  %PLATFORM%：平台名称

- App平台下的代码
  - #ifdef APP-PLUS
  - #endif
- 除H5平台, 其他平台都会存在的代码
  - #ifndef H5
  - #endif
- 在H5平台或微信小程序平台存在的代码 ( 可以有||, 不能有&&, 因为没有交集)
  - #ifdef H5 || MP-WEIXIN
  - #endif