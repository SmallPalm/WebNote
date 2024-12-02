# 屏幕尺寸的分割点

- Bootstrap的一大核心就是响应式
  - 即开发一套系统便可以适配不同尺寸的屏幕
- 它底层原理是使用媒体查询来为我们的布局和页面创建合理的断点
  - 断点(Breakpoints)
- Bootstrap 4设了5个断点来构建响应式系统
  - 5个断点分别为 
    - Extra-Small
      - 特小尺寸的
    - Small
      - 小尺寸的
    - Medium
      - 中尺寸的
    - Large
      - 大尺寸的
    - Extra large
      - 特大尺寸的
- 媒体查询是CSS的一项功能
  - 它允许你根据浏览器的分辨率来应用不同的CSS样式
  - 如 @media (min-width: 576px){}

# 响应式容器

- Containers容器是 Bootstrap中最基本的布局元素
  - 并且该布局支持响应式
  - 在使用默认网格系统时是必需的
- Containers容器用于包含、填充，有时也会作为内容居中使用
  - 容器也是可以嵌套，但大多数布局不需要嵌套容器
- Bootstrap 带有三个不同的Containers容器
  - .container: 它在每个断点处会设置不同的max-width
    - container-sm
    - container-md
    - container-lg
    - container-xl
  - .container-fluid：在所有断点处都是 width: 100%
  - .container-{breakpoint}, 默认是width: 100%
    - 直到指定断点才会修改为响应的值

![image-20231110135356990](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231110135356990.png)

# 认识网格系统

- 在我们在开发一个页面时，经常会遇到一些列表（例如，商品列表）
  - 这些列表通常都是通过行和列来排版。
- 为了方便我们对这种常见列表的布局
  - Bootstrap框架对它进行了封装，封装为一个网格系统

网格系统

- Bootstrap网格系统是用于构建移动设备优先的强大布局系统
  - 可支持12列网格、5 个断点和数十个预定义类。
- 提供了一种简单而强大的方法来创建各种形状和大小的响应式布局
- 底层使用了强大的flexbox来构建弹性布局，并支持12列的网格布局
- 网格系统是使用container、row和col类来布局
  - 并且布局是支持响应的