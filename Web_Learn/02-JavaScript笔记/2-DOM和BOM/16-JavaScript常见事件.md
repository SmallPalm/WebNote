# 常见的鼠标事件

- **click**
  - 当用户点击某个对象时调用的事件句柄
- **contextmenu**
  - 在用户点击鼠标右键打开上下文菜单时触发
- dblclick
  - 当用户双击某个对象时调用的事件句柄
- mousedown
  - 鼠标按钮被按下
- mouseup
  - 鼠标按键被松下
- mouseover
  - 鼠标移到某个元素之上
    - 支持冒泡
- mouseout
  - 鼠标从某个元素移开
    - 支持冒泡
- mouseenter
  - 当鼠标指针移动到元素上时触发
    - 不支持冒泡
- mouseleave
  - 当鼠标指针移除元素时触发
    - 不支持冒泡
- mousemove
  - 鼠标被移动

# mouseover和mouseenter的区别

- mouseenter和mouseleave
  - 不支持冒泡
  - 不能做事件委托
  - 进入子元素依然属于在该元素内 , 没有任何反应
    - enter
      - 进入
    - leave
      - 离开
- mouseover和mouseout
  - 支持冒泡
  - 进入元素的子元素时
    - 先调用父元素的mouseout
    - 在调用子元素的mouseover
    - 因为支持冒泡 , 所以会将mouseover传递到父元素中
  - over
    - 从......向下
  - out
    - 向外



# 常见的键盘事件

- onkeydown
  - 某个键盘按键被按下
  - down事件先发生
- nokeypress
  - press发生在文本被输入
  - 某个键盘按键被按下
- nokeyup
  - 发生在文本输入完成
  - 某个键盘按键被松开
- 可以通过event.key和event.code来区分按下的是什么键
  - 对于非字符的按键 , 通常具有与code相同的值
  - code
    - 按键代码 ,  特定于键盘上按键的物理位置



# 常见的表单事件

- onchange
  - 该事件在表单元素的内容改变时触发
  - 事件是已经确定input失去焦点 确定内容时,事件触发 
- oninput
  - 元素获取用户输入时触发
- onfocus
  - 元素获取焦点时触发
- onblur
  - 元素失去焦点时触发
- onreset
  - 表单重置时触发
- onsubmit
  - 表单提交时触发



# 文档加载事件

- DOMContentLoaded
  - 浏览器已完成加载HTML，并构建了DOM树
  - 但像img 和 外部样式表等外部资源可能还没有加载完成
- load
  - 浏览器不仅仅加载完成HTML 还加载完成所有外部资源:图片样式等





# 视图事件

- onresize	
  - 当document尺寸发生改变的时候 ,  触发事件

- onscroll
  - 当浏览器时滚动时,  触发事件





# window中的定时器

- 一个函数, 而是等待一段时间之后再执行 , 我们称之为 “**计划调用**”

  - 计划调用 : scheduling a call

- setTimeout

  - 允许我们将函数推迟到一段时间间隔之后再执行

- setInterval

  - 允许我们重复运行一个函数
  - 从一段时间间隔之后开始运行
  - 之后以该时候间隔连续重发运行该函数

- clearTimeout

  - 取消setTimeout的定时器

- clearInterval

  - 取消setInterval的	定时器

- clear(清除)方法

  - set定时器在调用时, 会返回一个**定时器标识符** , 我们可以使用它来取消执行

    ```js
    var 变量 = setTimeout()
    clearTimeout(变量)
    ```

  

