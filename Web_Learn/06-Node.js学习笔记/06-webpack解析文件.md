# CSS转义

## css-loader的使用

### loader

- loader 可以用于对模块的源代码进行转换
- 我们可以将css文件也看成是一个模块
  - 我们是通过import来加载这个模块的
- 在加载这个模块时
  - webpack其实并不知道如何对其进行加载
  - 我们必须制定对应的loader来完成这个功能

### CSS-loader

- 对于加载css文件来说，我们需要一个可以读取css文件的loader
  - 这个loader最常用的是css-loader

### css-loader的安装

- npm install css-loader -D

### 使用方案

- loader来加载css文件有三种方式

  - 内联方式

    - 内联方式使用较少，因为不方便管理

    - 在引入的样式前加上使用的loader，并且使用!分割

    - ```js
      import "css-loader!../css/style.css"
      ```

      

  - CLI方式（webpack5中不再使用)

    - 在webpack5的文档中已经没有了--module-bind
    - 实际应用中也比较少使用，因为不方便管理

  - 配置方式

## loader配置方式

配置方式表示的意思是在我们的webpack.config.js文件中写明配置信息

- module.rules中允许我们**配置多个loader**
  - （因为我们也会**继续使用其他的loader，来完成其他文件的加载**）
- 这种方式可以更好的表示loader的配置
  - 也方便后期的维护
  - 同时也让你对各个Loader有一个全局的概览

### module.rules的配置如下

- rules属性对应的值是一个数组：[Rule]
- 数组中存放的是一个个的Rule
  - **Rule是一个对象**，对象中可以**设置多个属性**

- test属性
  - 用于对 resource（资源）进行匹配的
  - 通常会设置成正则表达式
- use属性
  - 对应的值时一个数组：[UseEntry]
- [UseEntry]
  - UseEntry是一个对象
  - 可以通过对象的属性来设置一些其他属性
- loader
  - 必须有一个 loader属性
    - 对应的值是一个字符串
- options
  - 可选的属性
  - 值是一个字符串或者对象
  - 值会被传入到loader中
- 传递字符串
  - 如：use: [ 'style-loader' ]
    - 是 loader 属性的简写方式
      - use: [ { loader: 'style-loader'} ]

## 认识style-loader

- css-loader只是负责将.css文件进行解析
  - 并不会将解析之后的css插入到页面中
- 如果我们希望再完成插入style的操作
  - 那么我们还需要另外一个loader，就是style-loader

### 安装style-loader

- npm install style-loader -D

## 配置style-loader

- 在配置文件中，添加style-loader
- 因为**loader的执行顺序是从右向左**
  - 或者说从下到上，或者说从后到前的
- 所以我们需要将**style-loader写到css-loader的前面；**

## less文件

- 我们可能会使用less、sass、stylus的预处理器来编写css样式，效率会更高
  - less、sass等编写的css需要通过工具转换成普通的css
- 安装less
  - npm install less -D
- less工具来完成它的编译转换
  - npx lessc ./src/css/title.less title.css

当我们使用less编写大量css时

- 这个时候我们就可以使用less-loader，来自动使用less工具转换less到css

安装less-loader 并配置webpack.config.js

- npm install less-loader -D

打包时less就可以自动转换成css，并且页面也会生效了





## 认识PostCSS工具

PostCSS是一个通过JavaScript来转换样式的工具

- 这个工具可以帮助我们**进行一些CSS的转换和适配**
  - 比如**自动添加浏览器前缀**
  - **css样式的重置**
- 但是实现这些功能，我们需要**借助于PostCSS对应的插件**

如何使用PostCSS呢？主要就是两个步骤

第一步：查找PostCSS在构建工具中的扩展

- 比如webpack中的postcss-loader

第二步：选择可以添加你需要的PostCSS相关的插件

## postcss-loader

- 在webpack中使用postcss
  - **就是使用postcss-loader来处理的**

安装postcss-loader

- npm install postcss-loader -D

- 注意：
  - 因为postcss需要有对应的插件才会起效果，所以我们**需要配置它的plugins**
- ![image-20231121171224610](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231121171224610.png)

## 单独的postcss配置文件

- 因为我们**需要添加前缀**，所以要**安装autoprefixer**
  - npm install autoprefixer -D

- 我们可以将这些配置信息放到一个单独的文件中进行管理
  - 在根目录下创建postcss.config.js

![image-20231121173203419](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231121173203419.png)



## postcss-preset-env

preset : 预设

- 事实上，在配置postcss-loader时
  - 我们配置插件并**不需要使用autoprefixer**
- 我们可以使用另外一个插件：**postcss-preset-env**
- postcss-preset-env也是一个postcss的插件
  - 它可以帮助我们**将一些现代的CSS特性** ， **转成大多数浏览器认识的CSS**
  - 并且会**根据目标浏览器或者运行时环境添加所需的polyfill**；
- 也包括会自动帮助我们添加autoprefixer
  - 所以相当于已经**内置了autoprefixer**

- 安装postcss-preset-env
  - npm install postcss-preset-env -D
- 我们在**使用某些postcss插件时，也可以直接传入字符串**

# 认识asset module type

- 我们当前使用的webpack版本是webpack5

- 在webpack5之前，
  - 加载**这些资源**我们需要使用一些loader
  - 比如raw-loader 、url-loader、file-loader
  - **这些资源 : 图片img 图标font 等**
- 在webpack5开始
  - 我们可以直接使用资源模块类型
    - asset module type
  - 来替代上面的这些loader

## 资源模块类型(asset module type)

通过添加 4 种新的模块类型，来替换所有这些 loader

- asset/resource 发送一个单独的文件并导出 URL
  - 之前通过使用 file-loader 实现
- asset/inline 导出一个资源的 data URI
  - 之前通过使用 url-loader 实现
- asset/source 导出资源的源代码
  - 之前通过使用 raw-loader 实现
- asset 在导出一个 data URI 和发送一个单独的文件之间自动选择
  - 之前通过使用 url-loader，并且配置资源体积限制实现

# asset module type的使用

![image-20231121211423820](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231121211423820.png)

- **开发中我们往往是小的图片需要转换**
  - **但是大的图片直接使用图片即可**
- **这是因为小的图片转换base64**
  - **之后可以和页面一起被请求**	
  - **减少不必要的请求过程**
- **而大的图片也进行转换**
  - **反而会影响页面的请求速度；**

**我们需要两个步骤来实现**

- **步骤一：将type修改为asset**
- **步骤二：添加一个parser属性**
  - **并且制定dataUrlCondition的条件**
    - **添加maxSize属性；**

- ![image-20231121211620655](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231121211620655.png)



## 自定义文件的输出路径和文件名

- 方式一
  - 修改output，添加assetModuleFilename属性
  - ![image-20231121211744108](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231121211744108.png)
- 方式二
  - 在Rule中，添加一个generator属性
    - 并且设置filename
    - ![image-20231121211813472](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231121211813472.png)

最常用的placeholder(占位符)

- [ext]： 处理文件的扩展名
- [name]：处理文件的名称
- [hash] : 哈希值：文件的内容
  - webpack生成的hash(哈希值)(唯一的)
  - 使用MD4的散列函数处理
  - 生成的一个128位的hash值
  - 32个十六进制





# 转换JS

# babel

- 事实上 , 在开发中我们很少直接去接触babel
  - 但是babel对于前端开发来说 ,目前是不可缺少的一部分
- 开发中 ,我们想要使用ES6+的语法
  - 想要使用typescript 开发react项目, 都是离不开babel的
- 所以学习babel 对于我们理解代码从编写到上线的转变过程至关重要
  - 将ES6的语法转化成ES5的语法

**babel是什么**

- Babel是一个工具链
  - 主要用于旧浏览器或者环境中
    - 将ECMA script 2015以上的代码
      - 转换为向后兼容版本的JavaScript
  - 包括: 语法转换 , 源代码转换等 

# babel命令行

- 环babel本身可以作为一个独立的工具
  - 跟postCSS一样
  - 不和webpack等构建工具配置来单独使用
- 在命令行使用babel 需要安装
  - @babel/core :babel 的核心代码 必须安装
  - @babel/cli : 可以让我们在命令行使用babel
    - pnpm add @babel/cli @babel/core -D
- 使用babel来处理我们的源代码
  -  src :是源文件的目录
  - --out-dir : 指定要输出的文件件dist
    - npx babel src --out-dir dist

## 插件的使用

- **转换箭头函数变成普通函数**
  - 那么我们就可以使用箭头函数转换相关的插件
  - 安装插件
  - npm install @babel/plugin-transform-arrow-functions -D
  - 运行插件
  - npx babel src --out-dir dist --plugins=@babel/plugin-transform-arrow-functions
- 将ES6的Const let 转换为var 定义的变量
  - 使用 plugin-transform-block-scoping 来完成这样的功能
  - 安装插件
  - npm install @babel/plugin-transform-block-scoping -D
  - 运行插件
  - npx babel src --out-dir dist --plugins=@babel/plugin-transform-block-scoping

# babel的预设preset

- 如果要转换的内容过多 , 在命令行输入的太过麻烦 
- 一个个去安装使用的插件
  - 需要手动来管理大量的babel插件
  - 可以使用预设 : preset
- 常见的预设有三个
  - env
  - react
  - TypeScript
- 安装预设
  - npm install @babel/preset-env -D
- 执行命令
  - npx babel src --out-dir dist --presets=@babel/preset-env

# babel-loader

- 实际开发 , 我们通常会再**构建工具中通过配置babel**来对其进行使用的
  - 安装loader
  - npm install babel-loader -D
- 我们可以设置一个规则，在加载js文件时，使用我们的babel





# 转换Vue

- 对Vue代码打包会报错：我们需要合适的Loader来处理文件
  - 需要使用Vue-loader
  - npm install vue-loader -D
- 在webpack的模块规则中进行配置
  - ![image-20231124110003202](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231124110003202.png)
- 打包依然会报错
  - 这是因为我们必须添加
    - @vue/compiler-sfc来对Vue代码中template进行解析
  - npm install @vue-compiler-sfc -D
- 另外我们需要配置对应的Vue插件
- ![image-20231124110331275](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231124110331275.png)

![image-20231124110346234](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231124110346234.png)

- **重新打包即可支持vue代码的写法**



# resolve模块解析

- **resolve用于设置模块如何被解析**
  - 在开发中我们会有各种各样的模块依赖
  - 这些模块可能来自于自己编写的代码
    - 也可能是来自第三方库
- resolve可以帮助webpack从每个require / import 语句中
  - 找到需要引入的合适的模块代码
  - webpack底层就是使用enhanced-resolve来解析文件路径

**webpack能解析三种文件路径**

- 绝对路径
  - 由于已经获得文件的绝对路径
    - 因此不需要在做进一步解析
- 相对路径
  - 在这种情况下 , **使用import 或 require 的资源文件所处的目录被认为是上下文目录**
  - **在import / require中给定的相对路径**
    - **会拼接此上下文路径**
      - **来生成模块的绝对路径**
- 模块路径
  - 在resolve.modules中指定的所有的目录检索模块
    - 默认值是 [ “ node_modules ”]
      - 所以**默认会从node_modules中查找文件**
  - 我们可以通过设置别名的方式来替换初识模块路径
    - 使用**alias配置**

**在resolve中判断文件还是文件夹**

![image-20231124111955130](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231124111955130.png)

- 如果是一个文件
  - 如果文件具有扩展名 , 将直接打包文件
  - 否则,  将使用resolve .extensions选项作为**文件扩展名解析**
- **extensions : 扩展**
  - extensions是解析到文件时自动添加扩展名
  - 默认值是['.js', '.json', '.wasm']
    - 加载 .vue 或者 jsx 或者 ts 等文件时，可以自己写上扩展名
- **alias : 配置别名**
  - 当我们项目的目录结构比较深的时候
    - 或者一个文件的路径可能需要 ../../../这种路径片段
  - 可以给某些常见的路径起一个别名
    - 使用别名可以直接链接绝对路径
- 如果是一个文件夹
  - 会在文件夹中根据resolve.mainFiles配置选项中指定的文件顺序查找
    - resolve . mainFiles的默认值是 index文件
    - 在根据resolve.extensions来解析文件扩展名
  - resolve.mainFiles默认在文件夹后面的拼接index.文件
    - 拼接index的文件 在使用resolve.extensions来拼接文件后面的扩展名