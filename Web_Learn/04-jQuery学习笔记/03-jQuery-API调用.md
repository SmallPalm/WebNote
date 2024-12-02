# jQuery过滤器

- jQuery原型上的方法
- 1.eq(index)
  - 从匹配元素的集合中，取索引处的元素， eq全称(equal 等于)，返回jQuery对象。
- 2.first()
  - 从匹配元素的集合中，取第一个元素，返回jQuery对象。
- 3.last()
  - 从匹配元素的集合中，取最后一个元素，返回jQuery对象。
- 4.not(selector)
  - 从匹配元素的集合中，删除匹配的元素，返回jQuery对象。
- 5.filter(selector)
  - 从匹配元素的集合中，过滤出匹配的元素，返回jQuery对象。
- 6.find(selector)
  - 从匹配元素集合中，找到匹配的后代元素，返回jQuery对象。
- 7.is(selector | element |  . )
  - 根据选择器、元素等检查当前匹配到元素的集合。集合中至少有一个与给定参数匹配则返回true。
- 8.odd() 
  - 将匹配到元素的集合减少为集合中的奇数，从零开始编号，返回jQuery对象。
- 9.even()
  - 将匹配到元素的集合减少到集合中的偶数，从零开始编号，返回jQuery对象。
- 10.支持链式调用



# jQuery对文本的操作

- .text()、.text(text)
  - 获取匹配到元素集合中每个元素组合的文本内容，包括它们的后代，或设置匹配到元素的文本内容。相当与原生元素的textContent属性。
- .html()、html(htmlString)
  - 获取匹配到元素集合中第一个元素的HTML内容，
    - 包括它们的后代，
    - 或设置每个匹配元素的 HTML 内容。
      - 相当与原生元素的innerHTML属性。
- .val()、.val(value)
  - 获取匹配到元素集合中第一个元素的当前值 
    - 或设置每个匹配到元素的值。
  - 该.val()方法主要用于获取input,select和等表单元素的值。
    - 相当与获取原生元素的value属性。

# jQuery对CSS的操作

- .width()、.width(value)
  - 获取匹配到元素集合中第一个元素的宽度
    - 或设置每个匹配到元素的宽度。
- .height()、height(value)
  - 获取匹配到元素集合中第一个元素的高度
    - 或设置每个匹配到元素的高度。
- .css(propertyName)、.css(propertyNames)
  - 获取匹配到元素集中第一个元素样式属性的值，
    - 底层是调用getComputedStyle函数获取。
- **.css( "width" )和.width()之间的区别:**
  - width() 返回一个无单位的像素值（例如，400)
  - css() 返回一个具有完整单位的值（例如，400px）
- .css(propertyName, value)、.css(properties)
  - 为每个匹配到元素设置一个 或 多个 CSS 属性。
  - 调用css方法添加样式会直接把样式添加到元素的style属性上。



# jQuery对属性的操作

- .addClass(className)、.addClass(classNames)、.addClass(funcntion)
  - 将指定的类添加到匹配元素集合中的每个元素，每次都是追加class。
  - 底层调用的是setAttribute( "class", finalValue )方法添加class。
- .hasClass(className)
  - 是否给任意匹配到的元素分配了该类。
  - 底层是通过getAttribute( "class" ).indexOf()来判断是否存在。
- .removeClass()、.removeClass(className)、.removeClass(classNames)、.removeClass(function)
  - 给匹配元素集中的每个元素删除单个类、多个类或所有类。
  - 底层调用的是setAttribute( "class", finalValue )方法。
- .toggleClass()、.toggleClass(className[,state])、.toggleClass(classNames[,state])
  - 根据类的存在或状态参数的值，在匹配到元素的集合中，给每个元素添加或删除一个或多个类。

## jQuery对自定义data属性的操作

- .data()、.data(key)
  - 获取匹配元素集中第一个元素的自定义属性的值
- .data(key, value) 、.data(obj)
  - 为每个匹配元素设置一个或多个自定义属性
- .removeData([name]) 
  - 会删除data()函数给匹配元素属性添加的数据 
    - data()函数绑定的自定义属性。
  - data函数添加的属性会被移除，
    - 但是如果属性同时在签上定义了就不会被移除。
  - 因为在data中定义的数据, 会存储中缓存中, 
    - 当删除时, 会直接从缓存中清除, 
      - 就不会移除标签中data自定义的属性了 

# jQuery对DOM的操作

## 插入内容

- .**append**(content [, content] ) 、append( function )
  - 将参数的内容插入到匹配元素集中**每个元素的末尾**。
    - content 所包含的类型: 
      - DOM element, elements 
      - text node,  text nodes
      - array
      - HTML string
      - jQuery object
- .**prepend**(content [, content] ) 、prepend( function )
  - 将参数的内容插入到匹配元素集中**每个元素的开头**。
- .**after**(content [, content] ) 、after( function )
  - 在匹配元素集中的**每个元素之后**，插入由参数指定的内容。
- .**before**(content [, content])、before( function )
  - 在匹配元素集中的**每个元素之前**，插入由参数指定的内容。
- .**appendTo**(target)
  - 将匹配元素集中的每个元素插入到**目标元素的末尾**。
    - target的类型：
      - selector, 
      - HTML string
      - array 
      - elements, element
      - jQuery object
- .**prependTo**(target)
  - 将匹配元素集中的每个元素插入到**目标元素的开头**。
- .**insertAfter**(target)
  - 在**目标元素之后**，插入匹配元素集中的每个元素。
- .**insertBefore**(target) 
  - 在**目标元素之前**，插入匹配元素集中的每个元素。

## 移除

- .empty():  
  - 删除匹配元素集的所有子节点，自身不会删除。
- .remove( ) 、.remove( [selector] )
  - 删除匹配的元素集，自身也会删除。
  - selector参数
    - 字符串类型选择器
      - 筛选匹配元素集的元素来删除

## 替换

- .replaceAll(target): 
  - 用匹配到的元素集替换每个目标元素。
- .replaceWidth(newContent)、.replaceWidth( function )
  - 用新内容替换匹配元素集中的每个元素，并返回被移除的元素集。
  - newConten参数的类型： 
    - HTML string,
    - DOM element
    - array 
    - DOM elements
    - jQuery object

## 克隆

- .clone()、.clone( withDataAndEvents )
  - 对匹配的元素集执行深度复制，
  - 底层是调用了elem.cloneNode( true )来复制元素。
    - withDataAndEvents参数 : 
      - 布尔值 ,  默认值为false。
        - 是否复制该元素的事件处理程序和数据，

