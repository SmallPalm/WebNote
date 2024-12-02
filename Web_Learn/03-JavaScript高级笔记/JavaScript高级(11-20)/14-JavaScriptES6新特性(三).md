# Set的基本使用

- 在ES6之前 , 我们存储数据的结构主要有两种: 数组  和 对象
  - ES6中新增了另外两种数据结构,  **Set** **Map** 
    - 以及 它们的另外形式 **Weak Set** , **Weak Map**
- Set是一个新增的数据结构
  - 可以用来保存数据 , 类似于数组 , 但是和数组的区别是**元素不能重复**
  - 保存的是一个可迭代对象就可以
    - 创建Set , 我们需要通过 Set 构造函数 
      - (暂时没有字面量创建的方式)
- 我们可以发生Set 中存放的元素是不会重复的 ,
  -  那么Set有一个非常常用的功能就是**给数组去重**

Set的常见方法

- Set的常见属性 : 
  - size : 返回 Set 中元素的个数
- Set 常用的方法 :
  - add (Value) : 添加某个元素 , 返回Set对象本身
  - delete (value) : 从Set 中删除和这个值相等的元素, 返回Set对象本身
  - has (Value) : 判断set中是否存在某个元素 , 返回boolean类型
  - clear() : 清空set中所有的元素 , 没有返回值 ,
  - forEach ( callback , [thisArg]) : 通过forEach遍历Set
- Set支持 for of 的遍历的



# WeakSet使用

- 和Set类似的另外一个数据结构称之为WeakSet 
  - 也是内部元素不能重复的数据结构
- 和Set的区别
  1. WeakSet 中只能存放对象类型 , 不能存放基本数据类型
  2. WeakSet 对元素的引用是弱引用 
     - 如果没有其他引用对某个对象进行引用
       - 那么GC(内存垃圾回收器) , 可以对该对象进行回收
       - GC当弱引用当做不存在
- 常见的方法
  - add()
  - delete()
  - has()
- WeakSet 不能遍历
  - 因为WeakSet 只能对对象的弱引用 , 
    - 如果我们遍历获取到其中的元素
    - 那么可能造成对象不能正常的销毁

  - 所有存储到WeakSet中的对象是没办法获取的




# Map的基本使用

- 新增的数据结构是Map  用于**存储映射关系**
- 使用对象来存储映射关系 ,他们有什么区别
  - 对象存储映射关系只能用字符串 和 Symbol 作为属性名(key)
  - 某些情况下我们可能希望通过其他类型作为 key
    - 比如对象, 这个时候 会自动 将对象转成字符串来作为key

- 常见的方法
  - set (key , Value) : 添加Key Value , 返回Map对象本身
  - get( key) :  根据Key获取Map中的Value
  - delete (value) : 根据Key删除一个键值对 , 返回map对象本身
  - has (Value) : 判断Map中是否存在key , 返回boolean类型
  - clear() : 清空set中所有的元素 , 没有返回值 ,
  - forEach ( callback , [thisArg]) : 通过forEach遍历Map



# WeakMap的使用

- 数据结构WeakMap
  - 以键值对的形式存在的
- 和Map的区别
  - WeakMap的key只能使用对象 , 不接受其他的类型作为key
  - WeakMap的key对对象想的引用是弱引用, 
    - 如果没有其他引用引用这个对象 , 那么GC就会回收该对象
- 常见方法
  - Set(key , valuw) : 在Map中添加key value 并且返回整个Map对象
  - get (key) : 根据key 获取Map中value
  - has(key) :判断是否包括某个key 返回boolean类型
  - delete(key) :根据key删除一个键值对
