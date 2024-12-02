# Margin 塌陷问题如何额解决？

margin塌陷

如 两个div 应该margin距离为200px, 但margin发生重叠, 距离就会根据那个margin大

如果不希望margin重叠, 就需要给元素触发**BFC** : 独立块级格式化

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box1,
    .box2 {
      width: 100px;
      height: 100px;
      background-color: #445443;
    }

    .box1 {
      margin-bottom: 100px;
    }

    .box2 {
      margin-top: 100px;
    }
  </style>
</head>

<body>
  <div class="box1"></div>
  <div class="box2"></div>
</body>

</html>
```



# BFC是什么

块级格式化上下文 : Block  Formatting Context

一个独立的渲染区域, 有自己的渲染规则 , 与外部元素不会相互影响

# 怎么触发

触发BFC方式

- 设置了 float 属性  ( 值不为none )
- 设置了 position  属性 为 absolute 或 fixed
- 设置了 display 属性为 inline-block
- 设置了 overflow 属性 ( 值不为visible )

