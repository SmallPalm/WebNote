# 创建元素

- document.createElement(tag)
  - create :  创建
  - tag : 标签



# 插入元素

- node.append——在节点（node）末尾，插入节点或者字符串
- node.prepend——在node开头，插入节点或者字符串

- node.before——在node前面
- node.after——在node后面
- node.replaceWith——将node替换为给定的节点或者字符串



# 移除元素

- remove()

​	

# 克隆元素

- cloneNode()





# 获取html元素的大小位置

- clientWidth : 获取宽度 : contentwidth+padding : 不包含滚动条
- clientHeight : 获取高度 : contentheight+padding :不包含滚动条
- clientTop : border
- clientLeft : border
- offsetWidth : 元素完整的宽度
- offsetHeight : 元素完整的高度
- offsetTop :  距离父元素的x 
- offsetLeft : 距离父元素的y
- scrollTop : 滚动部分的高度
- scrollHeight : 整个可滚动的区域的高度

# window的大小位置

- inner : 获取可视视口
- outer : 获取视口
- documentElement : 获取html
- scrollX : 获取window的滚动位置 : x轴
- scrollY : 获取window的滚动位置 : y轴
- **scrollBy(x , y)** : 将页面滚动到 ,相对于当前位置的(x , y)位置
  - 在原来的位置每次增加
- **scrollTo(pageX , pageY)** : 将页面滚动到 绝对坐标
  - 滚到绝对的位置 , 就不在变化



# 补充string方法

- padStart

  - 在字符串的前面添加

  - ```js
    var num = "4"
    console.log(num.padStart(6, "0")
    ```

- padEnd

  - 在字符串的后面添加