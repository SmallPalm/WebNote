# 认识事件(Event)

- 当某个事件发生时，让JavaScript可以响应(执行某个函数)，所以我们需要针对事件编写处理程序， (handler : 处理)。



# 事件处理方案

- 带on的，添加事件

- addEventListener
  - 添加监听事件
  - 注册某个事件类型以及事件处理函数



# 常见的事件列表 

- 鼠标事件
  - click —— 当鼠标点击一个元素时
  - mouseover / mouseout——当鼠标指针移入 / 离开一个元素时
  - mousedown / mouseup——当在元素上按下 / 释放鼠标按钮时
  - mousemove —— 当鼠标移动时
- 键盘事件
  - keydown / keyup——当按下和松开一个按键时
- 表单事件
  - submit —— 当访问者提交了一个form时
  - focus —— 当访问者聚焦于一个元素时， 例如聚焦于一个<input>

- document事件
  - DOMContentLoaded —— 当HTML的加载和处理均完成，DOM被完成构建完成时
- css事件
  - transitionend —— 当一个css动画完成时



# 事件流

- 因为HTML中元素是具备层叠性的
- 默认情况下事件是从**最内层往外层依次传递**的顺序，这个顺序我们称之为**事件冒泡**（Event bubbling）
- 还有另一种监听事件流就是**从外层到内层**，这种称之为**事件捕获**（Event capture）
  - 在addEventListener添加第三个属性true
- ![image-20230726153620642](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230726153620642.png)
- 一般使用默认的事件冒泡比较多



# 事件对象

- 当事件发生时，就会有和这个事件相关的很多信息
- 这些信息会被封装到一个**event对象**中
  - 这个对象是由浏览器创建
    - 称之为**event对象**呢
- **event对象**会在传入的事件处理 ，函数回调时，会被系统传入
- 我们可以在回调函数中拿到这个**event对象**



# event对象

- **常见的属性和方法**
  - **target** : 当前事件发生的元素
  - **currentTarget** : 当前处理事件的元素
  - type : 事件的类型 
  - eventPhase : 事件所处的阶段

### target和currentTarget区别

- 当拥有事件流时
  - 拥有冒泡和捕获的时候,会拥有区别
  - currentTarget
    - 第一个进入的事件
  - target
    - 发生的事件

## event方法

- event自己的方法
  - **event.preventDefault()**
    - 阻止元素的默认行为
      - 就像a元素自动专跳页面，在函数中阻止默认行为
  - **event.stopPropagation**
    - 阻止事件的进一步传递
      - 冒泡或者捕获都可以阻止



# 事件处理中this

- 在事件处理函数中，我们也可以通过this来获取当前的发生元素
  - this === event.currentTarget



# EventTarget类

- 所用的节点 ，元素都继承自EventTarget
  - 事实上window也继承自EventTarget
- EventTarget是一个DOM接口
  - 主要用于添加，删除，派发event事件
- EventTarget常用的方法
  - addEventListener()
  - removeEventListener()
    - 移除某个事件类型以及事件处理函数
  - dispatchEvent()
    - 派发某个事件类型到EventTarget上
    
    - ```JS
      window.dispatchEvent(new Event("limingyu"))
      ```

# 事件委托(event delegation)

- 事件冒泡在某种情况下可以帮助我们实现强大的事件处理默认
  - 事件委托模式(也是一种设计模式)
- 当子元素被点击时 , 父元素可以通过冒泡可以监听到子元素的点击
- 可以通过event . target 获取到当前监听的元素

