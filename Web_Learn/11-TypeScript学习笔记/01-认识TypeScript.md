# JavaScript的痛点

- JS在类型检测上依然是毫无进展

## 类型带来的问题

- 编程开发中**错误出现的越早越好**

### 类型错误

- JavaScript的函数对我们传入的参数没有进行任何的限制
  - 如果有错误, 会到运行期间才会保错
- TS就是给JS加上很多限制的

### 类型思维的缺失

- 前端开发人员对类型思维的缺失
  - 通常不需要关心变量或者参数是什么类型

# 认识TypeScript

- TypeScript是拥有类型的JavaScript超集
  - 可以编译成普通, 干净, 完整的Javascript代码
- TypeScript是加强版JavaScript
- JavaScript所拥有的特性, TS全部支持
  - 并且TS紧随**ECMAscript**标准
- 没有兼容性问题
- 编译时可以不借助Babel这用的工具



## TypeScript的编译环境

- 安装TypeScript
  - 可以通过TypeScript的Compiler将代码编译为JavaScript

```npm
# 安装命令
npm install typescript -g
# 查看版本
tsc --version
```

### TypeScript运行

- 第一步：通过tsc编译TypeScript到JavaScript代码
- 第二步：在浏览器或者Node环境下运行JavaScript代码
- 简化步骤

直接运行浏览器

- 通过webpack, 配置本地的TypeScript编译环境和开启一个本地服务, 可以直接运行在浏览器上
  - https://mp.weixin.qq.com/s/wnL1l-ERjTDykWM76l4Ajw

直接通过node的命令来执行

- 通过ts-node库

  - 为TypeScript的运行提供执行环境

- ```npm
  #安装ts-node
  npm install ts-node -g
  #ts-node需要依赖tslib和@type/node两个包
  npm install tslib @type/node -g
  ```

- 这样即可在node中运行TS代码

  - ts-node 文件名

