# 认识DOM和BOM

- DOM和BOM相关的API才能对网页,浏览器进行操作

- API: 应用程序编程接口



# DOM

- 文档对象模型
- 将页面所有的内容表示为可以修改的对象
- documet
- 浏览器将我们编写在html中的每一个元素(element)都抽象成对象
- document.documentElement
  - 对应的是html元素
- document.body
  - 对应的是body元素
- document.head
  - 对应的是head元素
- document.doctype
  - 对应文档声明


# 节点(Node)之间的导航(navigator)

- 获取一个节点后 ,可以根据这个节点去获取其他的节点 , 我们称之为节点之间的导航
- 节点之间存在的如下的导航关系
  - 父节点
    - parentNode
  - 前兄弟节点
    - previousSibling
  - 后兄弟节点
    - nextSibling
  - 子节点
    - childNodes
  - 第一个子节点
    - firstChild
  - 最后一个子节点
    - lastChild

# 元素(element)之间的导航(navigator)

元素之间存在的如下的导航关系

- 父元素
  - parentElement
- 前兄弟元素
  - previousElementSibling
- 后兄弟元素
  - nextElementSibling
- 子元素
  - children
- 第一个子元素
  - firstElementChild
- 最后一个子元素
  - lastElementChild

# 表单之间的导航

# from之间的导航

# 获取元素的方法

- 任意的获取到某个元素
- document.getElementById
  - 获取id
- getElementByClassName
  - 可以在元素上调用
  - 获取class
- **querySelector**
  - 通过选择器查询
  - 可以在元素上调用
- **querySelectorAll**
  - 查找所有的选择器
  - 可以在元素上调用

# 可迭代的

-  string
- 数组
- 元素的列表

# DOM对象模型

- 





# DOM Tree的理解

- 在html结构中,最终会形成一个树结构
  - 在抽象成DOM对象的时候 , 它们也会形成一个树结构
    - 称之为DOM Tree



# DOM的继承

- DOM相当于html,css和JavaScript的桥梁

# BOM

- 浏览器对象模型
- 浏览器提供的用于处理文档之外的所有内容的其他对象
- 比如navigator , location ,   history等对象

