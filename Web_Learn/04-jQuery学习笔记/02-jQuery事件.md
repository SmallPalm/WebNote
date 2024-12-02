# jQuery监听文档加载

- 监听文档加载
  - jQuery监听 document 的 DOM 加载完成事件 的四种方案
    - $(document).ready( handler)
    - $(“document”) . ready( handler)
    - $().ready( handler)
    - $(handler) : 推荐使用这种写法
- 监听window的load事件 ,即网页所有资源 ( 外部链接 ,图片等)加载完成
  - $(window).on(‘load’, handler)



# 认识事件(Event)

- Web页面经常需要和用户之间进行交互，而交互的过程中我们可能想要捕捉这个交互的过程：
  - 比如用户点击了某个按钮、用户在输入框里面输入了某个文本、用户鼠标经过了某个位置；
  - 浏览器需要搭建一条JavaScript代码和事件之间的桥梁；
  - 当某个事件发生时，让JavaScript可以相应（执行某个函数），所以我们需要针对事件编写处理程序（handler）；
- 原生事件监听方法：
  - 事件监听方式一：在script中直接监听（很少使用）。
  - 事件监听方式二：DOM属性，通过元素的on来监听事件。
  - 事件监听方式三：通过EventTarget中的addEventListener来监听。
- jQuery事件监听方法：
  - 事件监听方式一：直接调用jQuery对象中的事件处理函数来监听，例如：click，mouseenter....。
  - 事件监听方式二：调用jQuery对象中的on函数来监听，使用off函数来取消监听。

# click和on的区别

- click和on的区别：
  - click是on的简写。它们重复监听，不会出现覆盖情况，
    - 都支持事件委托，底层用的是addEventListener。
  - 如果 on 没有使用 selector 的话，
    - 那么和使用click是一样的。
  - on 函数可以接受一个 selector 参数，
    - 用于过滤触发事件的后代元素。
  - on 函数支持给事件添加命名空间。
- click和on的this指向
  - this都是指向原生的DOM Element

# jQuery的事件冒泡

- 默认情况下事件是从最内层的span向外依次传递的顺序
  - 这个顺序我们称之为事件冒泡（Event Bubble)
- 另外一种监听事件流的方式就是从外层到内层（body -> span)
  - 这种称之为事件捕获（Event Capture）
- 为什么会产生两种不同的处理流呢？
  - 这是因为早期浏览器开发时，不管是IE还是Netscape公司都发现了这个问题
    - 但是他们采用了完全相反的事件流来对事件进行了传递
  - IE<9仅采用了事件冒泡的方式
  - Netscape采用了事件捕获的方式
    - IE9+和现在所有主流浏览器都已支持这两种方式
- jQuery为了更好的兼容IE浏览器，底层并没有实现事件捕获。

# jQuery的事件对象

- jQuery事件系统的规范是根据W3C的标准来制定jQuery事件对象。
  - 原始事件对象的大多数属性
    - 都被复制到新的jQuery事件对象上。
- jQuery事件对象通用的属性
  - 以下属性已实现跨浏览器的兼容：
    - target、relatedTarget、pageX、pageY、which、metaKey
- jQuery事件对象常用的方法：
  - preventDefault() :  
    - 取消事件的默认行为（例如，a标签、表单事件等）。
  - stopPropagation() : 
    -  阻止事件的进一步传递（例如，事件冒泡）。
  - 要访问其它事件的属性，
    - 可以使用 event.originalEvent 
      - 获取原生对象。

# jQuery的事件委托

- 事件委托在某种情况下可以帮助我们实现强大的事件处理模式
  -  事件委托模式（也是一种设计模式）
- 那么这个模式是怎么样的呢？
  - 因为当子元素被点击时，
  - 父元素可以通过冒泡可以监听到子元素的点击；
    - 并且可以通过event.target获取到当前监听的元素；
- 案例
  - 一个ul中存放多个li，使用事件委托的模式来监听li中子元素的点击事件。

# jQuery常见的事件

- 鼠标事件（Mouse Events）

  - .click() 
    - 点击事件

  - .dblclick() 
    - 双击事件

  - .hover()
    - 鼠标悬浮事件

  - .mousedown() 
    - 鼠标按钮被按下

  - .mouseup()
    - 鼠标按钮被松开

  - .mouseenter()
    - 鼠标指针移动到元素上时触发

  - .mouseleave()
    - 鼠标指针移出元素时触发

  - .mousemove()
    - 鼠标被移动

  - .mouseover()
    - 鼠标移动到某元素上

  - .mouseout() 
    - 鼠标从某元素上移开

  - .contextmenu()
    - 点击鼠标右键打开上下文菜单时触发

  - .toggle()

- 键盘事件（Keyboard Events）
  - .keydown()
    - 事件先发生
  - .keypress()
    - 发生在文本被输入
  - .keyup()
    - 发生在文本输入完成 ( 抬起 , 松开)
- 文档事件（Document Loading Events）
  - load
  - ready()
  - unload
- 表单事件（Form Events）
  - .blur() 
    - 元素失去焦点时触发
  - .focus()
    - 元素获取焦点时触发
  - .change()
    - 该事件在表单元素的内容改变时触发
  - .submit()
    - 表单提交时触发
  - .select()
- 浏览器事件（Browser Events）
  - .resize()
    - 屏幕尺寸发生变化
  - scroll()

## mouseover和mouseenter的区别

- mouseenter 和 mouseleave
  - 不支持冒泡
    - 进入子元素依然属于在该元素内
      - 没有反应
- mouseover 和 mouseout
  - 支持冒泡
  - 进入事件监听的元素的子元素时
    - 先调用父元素 的 mouseout
    - 再调用子元素 的 mouseover
    - 因为支持冒泡 , 所以会将mouseover传递到父元素中

## jQuery的键盘事件

- 事件的执行顺序是 keydown()、keypress()、keyup()
  - keydown事件先发生
  - keypress发生在文本被输入
  - keyup发生在文本输入完成（抬起、松开)
- 我们可以通过key和code来区分按下的键
- code
  - “按键代码”（"KeyA"，"ArrowLeft" 等）
    - 特定于键盘上按键的物理位置
- key
  - 字符（"A"，"a" 等）
    - 对于非字符（non-character）的按键
    - 通常具有与 code 相同的值。

## jQuery的表单事件

- 表单事件（Form Events）
- .blur()
  - 元素失去焦点时触发
- .focus()
  - 元素获取焦点时触发
- change() 
  -  该事件在表单元素的内容改变时
  - 触发( <input>, <keygen>, <select>, 和 <textarea>)
- .submit() 
  -  表单提交时触发



# jQuery动画操作-animate

- .animate()
  - 执行一组 CSS属性的自定义动画
    - 允许支持数字的CSS属性上创建动画。
- .animate( properties [, duration ] [, easing ] [, complete ] ) 
  - animate传入的属性
  - easing : 缓动动画
- .animate( properties, options )
  - propertys参数的支持
    - 数值：number 、string
    - 关键字：'show'、'hide'和'toggle'
    - 相对值：+= 、 -= 
    - 支持  em 、% 单位（可能会进行单位转换
- 自定义修改宽高度动画
  - height ：100% -> 0
  - width： 100% -> 0
  - opacity: 1 - > 0
- 两种缓动动画
  - linear
  - swing

- 只能给数字属性的做动画, color属性就不能做动画, 
  - jQuery中动画效果是通过数字做修改

# jQuery常见动画函数

- .显示和隐藏匹配的元素
  - .hide() 、.hide( [duration ] [, complete ] )、.hide( options )  -  
    - 隐藏元素
  - .show() 、.show( [duration ] [, complete ] )、.show( options ) - 
    - 显示元素
  - .toggle() 、.toggle( [duration ] [, complete ] )、.toggle( options ) 
    - 显示或者隐藏元素
- 淡入淡出
  - .fadeIn()、.fadeIn( [duration ] [, complete ] )、.fadeIn( options )  
    - 淡入动画
  - .fadeOut()、.fadeOut( [duration ] [, complete ] )、.fadeOut( options )  
    - 淡出动画
  - .fadeToggle()、.fadeToggle( [duration ] [, complete ] )、.fadeToggle( options ) 
    -  淡入淡出的切换
  - .fadeTo( duration, opacity [, complete ] )   
    -   渐变到

# jQuery元素中的动画队列

- jQuery匹配元素中的animate和delay动画是通过一个动画队列(queue)来维护的
  - 例如执行下面的动画都会添加到动画队列中
    - .hide() 
    -  .show()
    - .fadeIn() 
    - .fadeOut()
    - .animate()
    - delay()
- queue()
  - 查看当前选中元素中的动画队列
- .stop( [clearQueue ] [, jumpToEnd ] )
  - 停止匹配元素上当前正在运行的动画
  - clearQueue 
    - 一个布尔值，指示是否也删除排队中的动画。默认为false
  - jumpToEnd 
    - 一个布尔值，指示是否立即完成当前动画。默认为false



# jQuery中的遍历

- each( function )
  - 遍历一个 jQuery 对象
  - 为每个匹配的元素执行一个回调函数。
    - function 参数: 
      - Function( Integer index, Element element )， 
        - 函数中返回false会终止循环。
- jQuery.each( array | object , callback )
  - 一个通用的迭代器函数，可以用来无缝地迭代对象和数组
    - array参数：
      - 支持数组（array）或者类数组（array-like)
    - object参数: 
      - 支持普通的对象 object 和 JSON对象等
    - function 参数: 
      - Function( Integer index, Element element )，
        - 函数中返回false会终止循环
- .each() 和 jQuery.each(）函数的区别
  - .each()是jQuery对象上的方法
    - 在js中这个就是类方法
    - **用于遍历 jQuery对象**
  - jQuery.each( ) 是jQuery函数上的方法 
    - 在js中这个就是实例方法
    - **可以遍历对象、数组、类数组等**，它是一个通用的工具函数

 