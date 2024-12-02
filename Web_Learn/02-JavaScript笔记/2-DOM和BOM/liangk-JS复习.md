# JS复习

## 1.对象

- dom对象
  - 找对象
    1. id : getElementById
    2. 标签 : getElementsByTagName
    3. class : getElementsByClassName
    4. name : getElementsByName
  - 操作对象
    - 创建对象
      1. 创建文本节点 : createTextNode
      2. 创建元素节点 : createElement
    - 添加节点
      1. 添加到内部后边 : appendChild
      2. 添加到指定元素的前边 : insertBefore
    - 子节点 :  父节点 : 兄弟节点 
      1. children : 子节点
      2. parentNode : 父节点
      3. firstElementChild : 第一个子节点
      4. lastElementSibling : 最后一个子节点
      5. previousElementSibling : 上一个兄弟
      6. nextElementSibling : 下一个兄弟
    - 添加样式
      1. class : className
      2. 行内样式 : style.属性名
    - 找对象中的内容
      1. innerHTML : 可以操作文本也可以操作子节点
      2. innerText : 找或者设置的是文本
    - 事件
      - 绑定方式
        1. PC :
           - 行内绑定 : on + 事件名
           - 对象 :  on+ 事件名 = 事件处理函数
        2. 移动的  : 对象addEventListener(事件名 , 事件处理函数 , false)
      - 常用事件
        1. 鼠标事件 : click
        2. 键盘事件 : keyup
        3. 触摸事件 : touch 
           1. touchstart  :  触摸开始
           2. touchmove :  触摸时
           3. touchend :  触摸结束



## js高级

1. ​	canvas对象
   1. 添加绘画功能 : getContext
   2. 设置起点 : moveTo
   3. 绘制直线 : lineTo
   4. 矩形 : rect ( x , y ,widht ,height )
   5. 圆 : arc(x , y  , r , 开始弧度 , 结束弧度 , true / false)