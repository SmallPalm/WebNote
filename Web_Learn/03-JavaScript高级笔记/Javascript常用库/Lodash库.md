# underscore库 VS Lodash库  

- Lodash 和 Underscore 都是非常实用JavaScript工具库
  - 它们都提供了非常多的函数来对数字、字符串、数组、对象等操作
  - 这些函数不但可以简化JavaScript编写
  - 而且可以极大的提高我们的开发效率
- 这些库非常适合如下操作：
  - 迭代数组
  - 对象和字符串
  - 操作和测试值
  - 创建复合函数
- Lodash是Underscore的一个分支
  - 仍然遵循Underscore的API
  - 但在底层已完全重写过。
  - 对于字符串、数组、对象等Lodash提供了**跨环境迭代**的支持。
- Lodash还添加了许多Underscore没有提供的特性和功能，
  - 例如：
    - 提供 AMD 支持、
    - 深度克隆
    - 深度合并
    - 更好的性能
    - 大型数组和对象迭代的优化等
  - 如今的Lodash足以成为Underscore替代品。
  - Lodash从第4个版本开始放弃对IE9以下的支持。

# Lodash库字符串

- 字符串（String）
- .camelCase(string)
  - 转换字符串为驼峰写法。
- .capitalize(string)
  - 转换字符串首字母为大写，剩下为小写。
- .endsWith(string, target) 
  - 检查字符串是否以给定的target字符串结尾。
- padStart(str, length,char)
  - 如字符串长度小于 length 则在左侧填充字符
    -  如果超出length长度则截断超出的部分。
- .trim(string, chars)
  - 从字符串中移除前面和后面的 空格 或 指定的字符。  

# Lodash库数组

- 数组（Array）
- .first(arr, level)
  - 获取array中的第一个元素
- .last(arr, [n=1]) 
  - 获取array中的最后一个元素
- .uniq(arr) 
  - 创建一个去重后的array数组副本。返回新的去重后的数组
- .compact(arr) 
  - 创建一个新数组，包含原数组中所有的非假值元素。返回过滤掉假值的新数组
- .flatten(arr) 
  - 减少一级array嵌套深度。返回新数组

# Lodash库对象

- 对象
- .pick(object, [props])
  - 从object中选中的属性来创建一个对象。返回新对象。
- .omit(object, [props])
  - 反向版_.pick ;  删除object对象的属性。返回新对象。_
- .clone( value)
  - 支持拷贝 arrays、 booleans、 date 、map、 numbers， Object 对象,  sets, strings, symbols等等。 
  - ​	arguments对象的可枚举属性会拷贝为普通对象。（注：也叫浅拷贝） 返回拷贝后的值。
- .cloneDeep(value)
  - 这个方法类似_.clone，担它会递归拷贝 value。（注：也叫深拷贝）。返回拷贝后的值。

# Lodash库集合

- 集合（Array | Object）

- .sample()
  - 从collection（集合）中获得一个随机元素。返回随机元素。
- .orderBy
  - 给数组排序，默认是升序asc。
- .each()
- .forEach()
  - 遍历(集合) 中的每个元素
- .filter( )
  - 返回一个新的过滤后的数组。

# Lodash库函数

- 函数
- .curry() - 返回新的柯里化（curry）函数
- .debounce() - 返回新的 debounced（防抖动）函数
- .throttle() - 返回节流的函数。

