# CSS常见单位

整体可以分为两类：

- 绝对长度单位 （absolute length unit）
- 相对长度单位 （relative length unit）
  - em：
    - 相对是自己的font-size，如果自己没有设置，那就会继承父级的font-size
    - 在其他属性中使用是相对于自身的字体（font-size）大小
  - rem：
    - 相对是html的font-size
  - vw / wh：
    - 相对于视口（屏幕，视窗）的宽度和高度
    - 跟随视口变化而变化

# Pixel

- 像素是影响显示的基本单位
- 像素单位常见三种像素名称
  - 设备像素 :  物理像素
  - 设备独立像素 : 逻辑像素
  - CSS像素
- 设备像素 :  物理像素
  - 显示器的真实像素，这个是屏幕固有的属性
- 设备独立像素 ：逻辑像素
  - 在开发中通常面向的1980x1080，无论显示器是都好的，在开发中都是1980x1080

# DPR，PPI

- DPR：设备像素比
- PPI：每英寸像素



# CSS编写的痛点

- #### css预处理器

- 常见预处理器

  - Sass / Scss
    - 最早也是最成熟的CSS预处理器
  - Less
    - 容易上手，可编程功能不够
  - Stylus
    - 主要用来Node项目进行CSS预处理
    - 语法偏向Python



## Less

- 就是编写css的一种过渡的代码

- Less的编写方法

  - 变量

    - @自己定义的变量名：变量值；

  - 嵌套

    - &：表示当前选择器的父级

  - 运算

  - 混入

    - 将一组属性从一个规则集到另一个规则集的方法

    - ```html
      .border{
      border:3px solid #f00
      }
      .container{
      height:200px;
      .border();
      }
      ```

    - ```html
      .border(@变量，@变量){
      border:3px solid #f00
      }
      .container{
      height:200px;
      .border(10px , #0f0);
      }
      ```

    - ```html
      .box{
      w100px
      h300px
      }
      .cont ainer{
      widht:.box()[w];
      height:200px;
      .border(10px , #0f0);
      }
      ```

  - extend继承

  - less内置函数

  - 作用域

  - 注释

  - 导入

