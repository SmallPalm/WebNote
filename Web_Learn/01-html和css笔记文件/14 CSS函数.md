# css函数

1. rgb
2. rgba
3. translate
4. rotate
5. scale
6. var：使用CSS定义的变量
7. calc：计算CSS值，通常用于计算元素的大小或位置
8. blur：毛玻璃(高斯模糊)效果
   1. blur（radius）
   2. filter：blur（数值）
   3. backdrop-filter：blur（数值）
      1. 需要添加 background-color的背景颜色rgba
9. bgradient：颜色渐变函数
   1. 是一种**bakcground-image**CSS数据类型的子类型，用于表现两种或者多种颜色的过渡转变
   2. 颜色渐变用的是一张图像，并不是用上真正的颜色

## FC-Formatting Context

任何元素只要在标准流里面都是属于一个FC

块级元素的布局属于Block Formatting context (**BFC**)

行内级元素的布局属于lnline Formatting context (**IFC**)

### Block Formatting Context BFC

- 在BFC里面，两个相邻的两个盒子的margin才会折叠
- 在BFC中，box会在垂直方向上一个挨着一个的排布
- 垂直方向的间距由margin属性决定
- 在BFC中，每个元素的左边缘是紧挨着包含块的左边缘
- BFC解决两个块级盒子margin的重叠问题
  - 给第一个盒子的父级盒子在设置一个BFC,让他脱离html的BFC
- BFC解决浮动高度塌陷
  - 浮动元素的父元素触发BFC，形成独立的块级格式化上下文
  - 浮动元素的父元素的高度是auto的
- BFC的高度是auto的情况下，是如何计算高度的
  - 如果只是inline-level，是行高的顶部和底部的距离
  - 如果有block-level，是由最底层的块上边缘和最低层块盒子的下边缘之间的距离
  - 如果有绝对定位元素，将被忽略
  - 如果有浮动元素，那么会增加高度以包括这些浮动元素的下边缘

#### 设置overflow：auto；才会脱离html的BFC

