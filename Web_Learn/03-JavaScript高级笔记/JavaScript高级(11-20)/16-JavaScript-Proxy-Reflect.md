# 监听对象的操作

- 需求: 有一个对象, 我们希望监听这个对象中的属性被设置或获取的过程
  - 可以使用属性描述符 Object.defineProperty 的存储属性描述符来做到
    - 对对象的属性的监听, 发生改变
- 缺点
  - 首先 Object.defineProperty 设计的初衷 , 
    - 不是为了去监听截止一个对象中所有的属性
      - 我们定义某些属性的时候 , 初衷其实是定义普通的属性, 
        - 但是后面我们强行将它变成了数据属性描述符
  - 其次 , 如果我们**想监听更加丰富的操作** 
    - 比如新增属性 , 删除属性 
      - **Object.defineProperty是无能为力**的
- **存储数据描述符**设计的初衷并不是为了去监听一个完整的对象



# Proxy基本使用

- 在ES6中, 新增一个Proxy类 (构造函数)
  - 是用于帮助我们创建一个代理的对象
- 监听一个对象的相关操作时 
  - 先new 一个代理对象 (Proxy对象)
  - 之后对该对象的所有操作 , 都通过代理对象来完成 , 
    - 代码对象可以监听我们想要对原来对象的做的那些操作



1. new Proxy对象
2. 传入需要侦听的对象以及一个处理对象 可以称之为handler( 处理)
3. 之后的操作都是直接对Proxy的操作 , 而不是原有的对象,
4. 需要再handler里面进行监听



# Proxy的捕获器

handler: 捕获器

- 监听某些具体的操作 , 在handler中添加对应的捕捉器 (Trap)
- Set 和 Get 对应的是函数类型
- Set函数参数 : 当代理对象被设置时
  - target : 目标对象 ( 侦听的对象 )
  - property : 将被设置的属性的key
  - value : 新属性值
  - receiver : 调用的代理对象
- Get函数参数 : 当代理对象被获取时
  - target : 目标对象( 侦听的对象 )
  - property : 被获取的属性key
  - receiver : 调用的代理对象
- handler.getPropertyOf()
  -  监听获取对象原型
- handler.setPropertyOf()
  - 监听设置对象的原型
- handler.isExtensible()
  - 监听对象判断是否可以新增属性 , 扩展属性的
- handler.preventExtensions()
  - 监听对象是否阻止扩展	
- handler.defineProperty
  - 监听对象使用属性描述符
- handler.ownKeys()
  - 监听Object.getOwnPropertyNames方法
  - 监听Object.getOwnPropertySymbol方法
- **handler.has()**
  - 监听 in操作符
- **handler.get()**
  - 监听获取操作
- **handler.set()**
  - 监听设置操作
- **handler.deleteProperty()**
  - 监听delete操作符

用于函数的对象

- **handler.apply()**
  - 监听函数调用操作
- **handler.construct()**
  - 监听new 操作符



- Proxy可以监听函数
  - 在捕获器中使用apply和constructor
    - 应用于函数对象的



# Reflect的作用

- 和proxy一起来使用

- Reflect是ES6中新增的一个API , 它是一个对象 ,  字面意思就是反射
- 直接使用
- 用处
  - 提供了很多操作 JavaScript对象的方法 ,
    - 有点像Object原型中操作对象的方法
- Reflect的来源
  - 这是因为在早期的ECMA规范中 没有考虑到这种**对 对象本身 的操作** 
    - 如何设计会更加的规范 , 所以将**这些API放到了Object上面**
  - 但是**Object作为一个构造函数**, 这些操作实际上**放到Object身上并不合适**
    - 另外还包含一些**类似于 in Delete 操作符 ,**
      - 让JS看起来是会有一些奇怪的
  - 所以在**ES6中新增了Reflect** , 让我们**这些操作都集中到了Reflect对象上**
- 使用Proxy时, 可以做到完全**不操作原对象**

# Reflect的常见方法

**Reflect方法和Proxy方法是对应的**

- Reflect.getPrototype(target)
  - **类似于Object.getPropertyOf()**
- Reflect.setPrototyp(target, prototype)
  - **设置对象原型的函数的, 返回一个boolean**
    - **如果更新成功 , 则返回true**
- Reflect.isExtensible()
  - **类似于Object.isExtensible()**

- Reflect.preventExtensions ()
  - **类似于Object.preventExtensions ()**
    - **返回一个boolean类型**
- Reflect.getOwnPropertyDescriptor( target , propertyKey)
  - **如果对象中存在该属性, 则返回对应的属性描述符** 
    - **否则返回undefined**
- Reflect. defineProperty( target, propertyKey)
  - **类似于object.defineProperty**
    - **也返回一个boolean类型**
- Reflect.ownKeys(target)
  - **返回一个包含所有自身属性 (不包含继承属性 ) 的数组**
    - **类似于Object.keys()**
      - **但不会受 属性描述符中的 Enumerable影响**



- **Reflect. has(target , propertyKey)**
  - 判断一个对象是否存在某个属性 ,
    - 和in 运算符 的功能完全相同
- **Reflect. get(target , propertyKey, Receiver)**
  - 获取对象身上某个属性的值, 类似于 target [name]
- **Reflect.set (target , propertyKey , value, [receiver])**
  - 将值分配给属性的函数, 返回boolean 
    - 如果更新成功, 则返回true
- **Reflect.deletePropert(target, propertyKey )**
  - 作为函数的delete操作符 
    - 相当于执行delete target[key]



- Reflect.apply(target, thisArgument , argumentsList)
  - **对一个函数进行调用操作, 同时可以传入一个数组作为调用参数**
    - **和function. prototype .apply() , 功能类似**
- Reflect. construct(target , argumentsList , [new target])
  - **对构造函数进行new 操作, 相当于执行 new target (...args)**