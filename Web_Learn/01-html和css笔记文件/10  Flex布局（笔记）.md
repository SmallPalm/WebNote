# css Flex布局

## 认识flexbox

- flexbox翻译为弹性盒子
  1. 弹性盒子是一种用于按行或按列布局元素的一维布局方法。（grid布局是二维布局比flex布局强大，但是grid布局有兼容性问题，所以90%都是还在使用flex布局）
  1. 元素可以膨胀以填充额外的内容，收缩以适应更小的空间。（所以称之为弹性盒子）
  1. 通常我们使用Flexbox来进行布局的方案 **称之为flex布局**
- flex布局是目前web开发中使用最多的布局方案 :
  1. flex布局 目前特别在移动端可以说已经完全普及
  2. 在pc端也几乎已经完全普及和使用,只有非常少数的网站还在使用浮动来布局
- 为什么需要flex布局
  1. css布局中唯一可靠并跨**浏览器兼容**的布局工具只有floats和positioning
  2. 但是这两种方法本身存在很大的局限性,并且他们用于布局实在是无奈之举

## flex布局的重要概念

- 两个概念
  - 开启了flex布局的元素叫 flex container(容器)
  - flex container 里面的直接子元素叫做flex item
- 当flex container 中的子元素变成了flex item时,具备一下特点
  1. flex item的布局将受flex container属性的设置来进行控制和布局
  2. flex iten不在严格区分块级元素和行内级元素
  3. flex item默认情况下是包裹内容的，但是可以设置宽度和高度
- 设置display属性为flex或者inline-flex 可以成为flex container
  - 设置的两个属相
    1. flex：flex container 以 block-level形式存在（**多用**）（设置成flex  就成为了块级弹性盒子  ，主要是为了添加后面的属性）
    2. inline-flex：flex container 以inline-level形式存在（了解）（设置在inline-flex 就变成了行内级弹性盒子）
- （ 我的理解）主要是为了开启flex布局  

### flex布局的模型

- flex布局模型 分为了主轴（main axis）和交叉轴（cross axis）
  - 主轴代表了元素布局的方向，主轴和交叉轴是可以调整和改变的
  - 父元素主轴的子元素宽高占满后不会自动换行，而是会被压缩。
- 还有四个个是主轴的大小（main size），开始（main start）和结束（main end），交叉轴的大小（cross size），开始（cross start）和结束（cross end）

### flex相关的属性

- #### 应用在flex container上的css属性
  
  - **flex-flow**
    
    - flex-flow属性是flex-direction和flex-wrap的简写
      - 顺序任意，并且都可以省略
    
  - **flex-direction**（flex的方向）
    
    - flex items 默认都是沿着 main axis（主轴）从main start 开始往 main end 方向排布
      1. flex-direction决定了main axis的方向 有四个取值	
      2. row（默认值）
      3. row-reverse（row的反转）
      4. column（列变成主轴的方向）
      5. column-reverse（列主轴进行反转）
    
  - **flex-wrap**
    
    -  flex-wrap决定了flex container是单行还是多行
      1. nowrap（默认）：单行	
      2. wrap：多行
      3. wrap-reverse：多行反转（忘记了，就写一下看看）
    
  - **justify-content **   （设置主轴）
    
    - justify-content决定了flex items在main axis（主轴）上的对齐方式
      1. **flex-start**（默认值）：与main start对齐。
      2. **flex-end**：让元素和main end对齐
      3. **center**：给元素居中对齐
      4. **space-between**： 
         1. flex items之间的距离相等
         2. main start，main end两端对齐
      5. **space-around**：
         1. flex items之间的距离相等
         2. flex items与main start ，main end 之间的距离是flex items 之间距离的一半
      6. **space-evenly**：
         1. flex items之间的距离相等
         2. flex items与main start，main end之间的距离  等于flex items之间的距离
    
  - **align-items**    （设置交叉轴）
  
    - align-items决定了flex items 在cross axis（交叉轴）上的对齐方式
      1. **normal**：在弹性布局中，效果和stretch一样
      2. **stretch**：当flex items在cross axis方向的size 为auto时，会自动拉伸至填充flex container
      3. **flex-start**：与cross start对齐
      4. **flex-end**：与cross end对齐
      5. **center**：居中对齐
      6. **baseline**：与基准线对齐
  
  - **align-content **    （设置交叉轴）
  
    （因为一般在实际开发中，不用写高度，所以一般是不会用到的， 这些是在基于高度中所做的效果）
  
    
    
    - align-content决定对了多行flex items在 cross axis 上的对齐方式，**用法与justify-content类似**
      1. **stretch**（默认值）：与align-items的stretch类似
      2. **flex-start**：与cross start 对齐
      3. **flex-end**：与cross end 对齐
      4. **center**：居中对齐
      5. **space-between**：
         1. flex items之间的距离相等
         2. 与cross start，cross end两端给对齐
      6. **space-around**：
         1. flex items之间的距离相等
         2. 与cross start，cross end之间的距离是flex items 之间距离的一半
      7. **space-evenly**：
         1. flex items之间的距离相等
         2. flex items与cross start，cross end 之间的距离 等于flex，items之间的距离
  
- #### 应用在flex items 上的css属性
  
  - **flex-grow**
    - flex-grow决定了 flex items  如何扩展(拉伸/成长)
      1. 可以设置任意非负数字(正小数,正整数,0),默认值是0
      2. 当flex container在main axis 方向上有剩余size 时,flex-grow属性才会有效(就是当父元素(flex container)上面还有剩余空间的时候,flex-grow设置才会生效)
    - flex items设置flex grow时,扩展后最终size不能超过max-width\max-height   (height是设置到交叉轴上的时候)
  - **flex-basis**
    - flex-basis用来设置flex items 在main axis(主轴) 方向上base size(基础大小)
      1. auto(默认值), 具体的宽度数值
    - 绝对flex items 最终的base size(基础大小)的因素,从优先级高到低
      1. max-width \ max-height \ min-width  \ min-height
      2. flex-basis
      3. width \ height
      4. 内容本身的size(大小)
  - **flex-shrink**
    - flex-shrink决定了flex items如何收缩(缩小)
      1. 可以设置任意非负数字(正小数,正整数 ,0),默认值是1(默认值是 要压缩的)
      2. 当flex items 在 main axis 方向上超过了 flex container 的size ,flex-shrink 属性才会生效
  - **order**
    - order决定了flex items的排布顺序
      - 可以设置任意整数（正整数，负整数，0），值越小就越排在后面
      - 默认值是0
  - **align-self**
    - 通过align-self属性可以覆盖align-items给flex container效果
      - 就是align-self属性是给单个item设置
      - align-items是给整体设置
        1. auto（默认值）：遵从flex container设置的align-items
        2. stretch，flex-start，flex-end，center，bastline效果跟align-items一样
  - flex
    - flex是flex-grow || flex-shrink ||flex-basis的 简写 ,flex属性可以指定1个 ,2个,3个
    - flex设置auto是   flex: 1  1   auto
    - flex设置 none 是 : flex:0  0   auto

### flex布局常见的问题

1. 一般flex布局不会设置高度, 都是让内容把父级弹性盒子撑起来。
2. 弹性盒子设置了布局，但是最后一行如果缺少flex item，就会布局乱。而flex布局里面的属性还不能调整，
   1. 方法一：通过计算宽度 设置margin，就可以将flex item在flex container中铺满（但是没有扩展性，如果flex container是固定的，计算一下设置flex item也可以。）
   2. 方法二：在flex items 中设置空的**i元素**（什么元素都可以，div，span）然后把设置i元素设置与flex items一样的宽度，就可以把flex items做成规整布局（一般加上两个就可以了）
   3. 方法二加了两个没有什么问题，**但是可以有扩展性**
