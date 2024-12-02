# grid布局

#### 认识

- flex是一个一维的布局

- grid是一个二维的布局
- grid对浏览器的兼容性对比 flex较差
- grid暂时了解即可

​	

#### 重要概念

- grid container
  - 元素设置display为grid的盒子
- grid item :  grid cell
  - grid container的直接子项
- grid line
  - 构成网格结构的分割线
  - 它们可以是垂直的(“列网格线”) 或水平的(“行网格线”)
- grid track
  - 两条相邻网格线之间的空间
  - 可以看成网格的行或者列
- grid  Area
  - 由四条网格线包围的总空间
  - 一个网格区域可以由任意数量的网格单元组成
- grid container常见属性
  1. display
  2. grid-template
     1. grid-template-columns
     2. grid-template-rows
     3. grid-template-areas
  3. grid-gap
     1. grid-columns-gap
     2. grid-row-gap
  4. place-items
     1. justify-items
     2. align-items
  5. place-content
     1. justify-content
     2. align-content
  6. grid-auto-flow
     1. grid-auto-columns
     2. grid-auto-rows
  7. grid
- grid item常见属性
  1. grid-columns-start
  2. grid-columns-end
  3. grid-row-start
  4. grid-row-end
  5. grid-column
  6. grid-row
  7. grid-area
  8. justify-self
  9. align-self
  10. place-self