# transform属性

CSS transform属性允许对某一个元素进行某些形变，包括旋转，缩放，倾斜或平移

transform是形变的意思

不是所有的盒子都可以进行transform的转换 （通知行内级元素不能进行形变）对行内级非替换元素是无效的

### transform的用法

transform属性的语法如下：

transform-list = transform-function+

transform-function  :  常见函数

1. ##### 平移，位移  ：translate(x,y)

   - 这个css函数用于移动元素在平面上的位置
   - translate本身可以表示翻译 的意思 ，在物理上也可以表示平移
     - 值个数
     - transform：translate（100px）一个值的时候代表x轴的 位移，二个值的时候代表x轴和y轴上 的 位移
     - transform：translate（100%）百分比
     - 百分比相对于自身宽度高度，100%就是自身宽度，参照物元素本身

2. ##### 缩放：scale（x，y）

   - scale（）CSS函数可改变元素的大小
   - 设置0~1是缩小 ， 设置大于1是放大
   - 一个值的时候代表x轴的缩放
   - 二个值的时候代表x轴和y轴上 的 缩放
     - 数值类型
     - 1：保持不变
     - 2：放大一倍
     - 0.5：缩小一半
     - 百分比不常用

3. ##### 旋转：rotate（deg）

   - 一个值表示旋转角度
   - 正数为顺时针
   - 负数为逆时针
   - 支持单位  度（deg）百分度（grad）（gradians）弧度（rad）（radians）圈数（turn）（turns）；

4. ##### 倾斜 ：skew（deg ， deg） 

   - 定义一个元素在二维平面上的倾斜转换

5. ##### transform-origin:;

   1. 修改当前元素的形变的原点位置
      1. 属性
         1. left right top bottom center
         2. 也可以给px 给具体单位,设置原点
         3. 还可以设置百分比,对应的是宽高
         4. 一个值是x轴 两个值是x轴和y轴


还有好多单词 需要用到查文档

### transfrom设置多个值

- 设置多个值 的 时候,应该 用什么来分割
  1. 属性后面跟+  
     - 一个或者 多个用空格 分割
  2. 属性后面跟#
     - 一个或者多个用逗号来分割， 
- 给transform 设置多个 形变的值



## 认识transition动画

- css提供了一种在更改css属性时控制动画速度的方法 
- 给css属性变化成为一个持续一段时间的过程,不是立刻 生效的
- 通过css transition,让这个过程加上一定的动画效果,包括一定的曲线速率变化

### 过渡动画 - transition属性

- transition-property  :  指定应用过渡属性的名称
  - all  :    所有属性都执行动画
  - none :   所有属性都不执行动画
  - css属性名称 :  要执行动画的css属性名称
- transition-duration :   指定过渡动画所需的时间
  - 单位可以是秒(s) 或者毫秒(ms)
- transiton-timing-function:  指定动画的变化曲线
- transition-delay  :  指定过渡动画执行之前的等待时间(就是延迟

### animation属性

- animation-name：指定执行那个关键帧动画

  - 使用@keyframes来定义多个变化状态，使用animation-name来声明匹配

  - ```html
    @keyframes jaek {
      0%{
        transform: translate(0px,0px);
      }
      20% {
        transform: translate(0px, 0px);
      }
      50% {
        transform: translate(0px, 0px);
      }
      100% {
        transform: translate(0px, 0px);
      }
    }
    ```

    

- animation-duration：指定动画的持续时间

- animation-timing-function：指定动画的曲线变化

- animation-delay：指定动画延迟执行时间

- animation-iteration-count：指定动画执行的次数

  - infinite：表示无限执行动画

- animation-direction：指定方向，常用值normal和reverse

- animation-fill-mode：执行动画最后保留到那一个位置

  - none：回到没用执行动画的位置
  - forwards：动画最后一帧的位置
  - backwards：动画第一帧的位置

- animation-play-state：指定动画运行或者暂停（在JavaScript中使用，用于暂停动画）

## vertical-align

- 一个行盒中的行内级元素的对齐方式	
- vertical-align会影响行内级元素在一个行盒中垂直方向的位置
- div没有高度，会被内容撑起高度。内容有了行高在会撑起div的高度
- vertical-align取值
  - baseline（默认值）：基线对齐
  - top：把行内级盒子的顶部跟line boxes顶部对齐
  - middle：行内级盒子的中心点与父盒基线加上x  - height（高度）一半的线对齐
    - 
  - bottom：把行内级盒子的底部跟line box底部对齐

######  大部分字体都会进行文本下沉的
