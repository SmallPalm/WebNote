# 对属性操作的控制

- 在前面我们的属性都是直接定义在对象内部的 
  - 或者直接添加到对象内部的
- 但是这样来做的时候我们就不能对这个属性进行要写限制
  - 比如这个属性是否是可以通过delete删除的
  - 这个属性是否在(for in)(for of) 遍历的时候被遍历出来的
- 如果我们想要对一个属性进行比较精准的操作控制
  - 可以使用属性描述符
  -  通过属性描述符可以精准的添加或修改对象的属性
  - 属性描述符需要使用Object.defineProperty来对属性进行添加或修改



# Object.defineProperty

- Object.defineProperty()方法
  - 会直接在一个对象上定义一个新属性
  - 或者修改一个对象的现有属性 , 并返回此对象

```js
Object.defineProperty(Object,property,descriptor)
```

- 可接受三个参数
  - Object : 定义属性的对象
  - Property : 定义或修改的属性的名称或标识(symbol)
  - descriptor : 要定义或修改的属性描述符
- 返回值
  - 被传递给函数的对象

# 属性描述符分类

1. 数据属性
2. 存取属性

# 数据属性描述符

​	四个特性

1. Configurable : 可配置
   - 告诉js引擎 , 对象的某个属性不可以被删除
   - 表示属性是否可以通过delete删除属性 , 是否可以修改它的特性
   - 在一个对象上定义某个属性时 , 这个属性的Configurable默认为true
   - 在属性描述符中定义某个属性时,  这个属性的Configurable默认为false
2. Enumerable : 可列举
   - 告诉js引擎 , 对象的某个属性不可以遍历
   - 表示属性是否可以通过for-in或者Object.keys()返回该属性
   - 在一个对象上定义某个属性时,  这个属性的Enumerable默认为true
   - 在属性描述符中定义某个属性时 , 这个属性是Enumerable默认为false
3. Writable : 可写的
   - 告诉js引擎, 对象的某个属性写入了,就不可以更改
   - 表示是否可以修改属性的值
   - 在一个对象上定义某个属性时 , 这个属性的writable默认为true
   - 在属性描述符中定义某个属性时,  这个属性的writable默认为false
4. value : 值
   - 默认情况修下这个值是undefined

# 存取属性描述符

- configurable : 和上面的一样
- Enumerable : 和上面的一样
- 当在对象中属性上, 进行再次赋值
  - 存取属性描述符就会监听对象中属性的变化 为set函数
- set函数
  - 监听对象中属性设置的过程
  - 默认undefined
- get函数
  - 监听对象中属性获取的过程
  - 默认undefined



# 额外补充对象方法

- 获取对象的属性描述符

  - 属性描述符的属性
  - getOwnPropertyDescriptor()

  - getOwnpropertyDescriptors()
    - 全部对象的属性

- 阻止对象的扩展

  - preventExtensions()
    - 给一个对象添加新的属性会失败

- 密封对象,  不允许配置和删除属性

  - seal
  - 实际上是调用preventExtensions()
  - 并且将现有属性的configurable的值为false

- 冻结对象 , 不允许修改现有属性

  - freeze
  - 实际上是调用seal
  - 并且将现有属性的writable的值为false


​	