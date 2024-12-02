# 节点node常见的属性

- **nodeType**
  - 获取节点的类型
  - 数值类型
  - 1
    - 一个元素节点
  - 3
    - text文本
  - 8
    - 一个注释节点
  - 9
    - 一个document节点
  - 10
    - 文档声明
- **nodename**
  - 获取节点的名称
  - 是为任意的节点定义
- **tagname**
  - 获取元素的标签名词
  - 只适用于元素节点
- 元素可以是节点，但是节点不一定是元素

- data
  - 针对非元素的节点获取数据
- **innerHTML**
  - 对应的HTML元素也会获取
  - 设置元素中的内容
- outerHTML
  - 包含了元素的完整HTML
  - innerHTML加上元素本身
- **textContent**
  - 只会获取文本内容
- innerHTML和textContent区别
  - innerHTML作为HTML插入,带所有的HTML标签
  - textContent作为文本插入,所有符号均按字面意义
- **nodeValue**
  - 和data作用一样

节点的其他属性

- hidden属性 : 全局属性可以用于设置元素隐藏
- value
- href
- id





- 在元素中的属性称之为attribute
- 在对象中的属性称之为property

# attribute的分类

- 标准attribute
- 非标准attribute
- ![image-20230725144500934](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230725144500934.png)





# property属性

- 在标准的attribute在对应的对象模型中都有对应的property
- 大多数情况下, property和attribute是相互的作用的
- 大多数情况下,设置获取attribute ,  推荐使用property的方式





# 动态修改样式

- ```js
  btnel.className =  "class"
  ```

- 在开发中，大多数情况下 ,  可以动态修改class完成某个功能 ,   更推荐使用动态class



# classlist

- 和**className**配合使用

- ```js
  btnel.onclick = function () {
      boxel.classList.toggle("active")
    }
  ```

- ![image-20230725154151373](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230725154151373.png)



- 在js中单独修改一个css属性 , 对于多词属性,使用驼峰式
- 如果将一个属性的值 设置为空的字符串 ,  那么使用的默认值





## 元素style的读取

- 使用getComputedStyle的全局函数来实现

  - ```js
    console.log(getComputedStyle(元素).全局样式)
    ```

    

