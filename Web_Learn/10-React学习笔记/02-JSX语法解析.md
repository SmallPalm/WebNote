# 认识JSX

- ```jsx
  const element = <div>Hello JSX</div>
  ```

- 变量声明的标签语法是一段JSX语法

## JSX是什么

- JSX是一种JavaScript的语法扩展
  - 很多地方也称之为JavaScript XML
    - 因为看起来很像一段XML语法
- 它用于描述我们的UI界面
  -  可以完全和JavaScript融合在一起使用
  - 不同于Vue的模板语法

## 为什么React使用JSX

- React认为渲染逻辑的本质上与其他UI逻辑存在 - 内在耦合
  - 内在耦合 : 很难分割, 关联性太强了, 息息相关
  - 如 UI需要绑定事件
  - 如 UI中需要展示数据状态
  - 如 在某些状态发送改变时, 又需要改变UI
  
- UI和JavaScript是密不可分的
  - React**没有将标记分离到不同的文件中**
    - 而是将**他们组合到一起**称之为组件

- JSX其实就是嵌入在JavaScript中的一种语法结构

- JavaScript的state和Html是分不开的
  - 所以才设计了JSX
  - 这是React设计之初的理念


Jsx的书写规范

- JSX的顶层只能有一个根元素，所以我们很多时候会在外层包裹一个div元素
- JSX中的标签可以是单标签，也可以是双标签



# JSX的使用

- JSX嵌入变量作为子元素
  - 情况一：当变量是Number、String、Array类型时，可以直接显示
  - 情况二：当变量是null、undefined、Boolean类型时，内容为空
    - 如果希望可以显示null、undefined、Boolean，那么需要转成字符串
    - 转换的方式有很多，比如toString方法、和空字符串拼接，String(变量)等方式
  - 情况三：Object对象类型不能作为子元素（not valid as a React child）

- JSX嵌入表达式
  - 运算表达式
  - 三元运算符
  - 执行一个函数



# React事件绑定

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写
- 我们需要通过{}传入一个事件处理函数，这个函数会在事件发生时被执行





# this的绑定问题

- 在事件执行后，我们可能需要获取当前Class类的对象中相关的属性
  - 这个时候需要用到this
  - 如果我们这里直接打印this，也会发现它是一个undefined

- 为什么是undefined
  - 原因是**点击函数**并不是我们主动调用的
    - 而且当button发生改变时，React内部调用了**点击函数**

- 如何解决this的问题呢
  - 方案一：bind给btnClick显示绑定this
  - 方案二：使用 ES6 class fields 语法
  - 方案三：事件监听时传入箭头函数



# 事件参数传递

- 在执行事件函数时, 有可能我们需要获取一些参数信息
  - 比如event对象, 其他参数
- 情况一 : 获取event对象
  - 默认情况下，event对象有被直接传入
  - 函数就可以获取到event对象
- 情况二：获取更多参数
  - 有更多参数时，我们最好的方式就是传入一个箭头函数
    - 主动执行的事件函数，并且传入相关的其他参数



# 条件渲染

在React中，所有的条件判断都和普通的JavaScript代码一致

1. 条件判断语句
2. 三元运算符
3. 逻辑与运算符
4. display: none



# 列表渲染

在React中需要使用JavaScript代码的方式来组织数据, 转为JSX

- 在React中

  - 展示列表最多的方式就是使用数组的map高阶函数

- 使用连接的方法可以做很多条件

- ```React
  renter(){
      return (
      	{
              array.filter(item => {item > 200}).slice(0, 2).map(item =>{
                item
            })
          }
      )
  }
  ```

## diff算法Key

- 我们需要在列表展示的jsx中添加一个key。
- key主要的作用是为了提高diff算法时的效率





# JSX的本质

实际上JSX仅仅只是, React.createElement(component, props, ... chlidren) 函数的语法糖

- createElement三个参数
  - type
    - 当前ReactElement的类型
    - 如果是标签元素，那么就使用字符串表示 “div”
    - 如果是组件元素，那么就直接使用组件的名称；
  - config 
    - 所有jsx中的属性都在config中以对象的属性和值的形式存储
    - 比如传入className作为元素的class
  - children
    - 存放在标签中的内容，以children数组的方式进行存储
    - 当然，如果是多个元素呢？React内部有对它们进行处理，处理的源码在下方



# 虚拟DOM的创建过程

- React.createElement函数最终创建出来一个ReactElement对象



这个ReactElement对象的作用

- React利用ReactElement对象组成了一个JavaScript的对象树
- JavaScript的对象树就是虚拟DOM (Virtual DOM)



ReactElement最终形成的树结构就是Virtual DOM；

# 虚拟DOM

最主要的两个作用

第一个重要的作用

- 虚拟DOM可以在更新数据时
  - 没有必要将整个结构全部重新渲染
- 当数据发送改变
  - render函数就是重新发送调用
    - DOM结构就会重新执行, 形成一个新的结构
  - 这是新的虚拟DOM就会和旧的虚拟DOM
    - 两者之间就会进行diff算法
      - 比较两者之间的不同
- 虚拟DOM可以在我们JS对象中快速进行diff算法
  - 来决定那些元素更新 , 那些元素不更新

第二个重要的作用

- 虚拟DOM可以转为真实DOM渲染到浏览器中
- 但是虚拟DOM作为对象
  - React可以将虚拟DOM
    - 转为Android端和IOS端的控件
    - React的虚拟DOM可以做到跨平台的



React开发原生Android端IOS端

使用ReactNative

Vue开发原生Android端IOS端

使用Weex





# 声明式编程

- 虚拟DOM帮助我们从命令式编程转到了声明式编程的模式
- React官方的说法
  - Virtual DOM 是一种编程理念
  - 在这个理念中
    - UI以一种理想化或者说虚拟化的方式**保存在内存中**
      - 并且它是一个相对简单的JavaScript对象
  - 可以通过ReactDOM.render让 虚拟DOM 和 真实DOM同步起来
    - 这个过程中叫做协调（Reconciliation）
