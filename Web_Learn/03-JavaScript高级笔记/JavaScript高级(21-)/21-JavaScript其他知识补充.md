# 错误处理方案

- 开发中我们会封装一些工具函数, 封装之后给别人使用
  - 对其他人使用的过程 , 可能会传递一些参数
  - 对于函数来说, 需要对这些参数进行验证 , 
    - 否则可能得到的是我们不想要的结果
- 很多时候我们可能验证到不是希望得到的参数时, 就会直接return
  - 但是return存在很大的弊端
    - 调用者不知道是因为函数内部没有正常执行
      - 还是执行结果就是一个undefined
  - 事实上, 正确的做法应该是 ,
    - 如果没有通过某些验证 ,那么应该让外界知道函数内部报错了
- 让函数告知外界自己内部出现了错误
  - 通过throw关键字, 抛出一个异常



# throw关键字

- throw语句用于抛出一个用户自定义的异常
  - 当遇到throw语句时 , 当前的函数执行会被停止 ( throw后面的语言不会执行)
- throw表示式就是throw后面可以跟一个表示式
  - 来表示具体的异常信息
- throw关键字可以跟上那些类型
  - 基本数据类型: Number string  Boolean
  - 对象类型: 

# Error类

- 事实上 , JavaScript已经给我们提供了一个Error类 , 我们可以直接创建这个类的对象
- Error包含三个属性
  - message : 创建Error对象时传入的message
  - name : Error的名称, 通常和类的名称一致
  - stack : 整个Error的错误信息, 包括函数的调用栈
    - 当我们直接打印Error对象时
      - 打印的就是stack
- Error有一些自己的子类 :  浏览器默认实现的一些子类 , 浏览器使用
  - RangeError :  下标值越界时 ,使用的错误类型
  - SyntaxError : 解析语法错误时, 使用的错误类型
  - TypeError : 出现的类型错误时, 使用的错误类型



# 异常的捕获

- 很多情况下当出现异常时 , 我们并不希望程序直接退出 , 

  - 而是希望可以正确的处理异常

- 使用try catch

- ```js
  try{
  	console.log("没有产生异常执行")
  }catch(error){
  	console.log("产生了异常执行", error)
  }finally{
  	console.log("有没有异常我都会执行")
  }
  ```

- 如果try和finally中都有返回值 , 那么会使用finally当中的返回值





# 认识Storage

- WebStorage 主要提供了一种机制 , 可以让浏览器提供一种比cookie更直观的key , value存储方式
  - localStorage 
    - 本地存储 , 提供的是一种永久性的存储方法
      - 在关闭掉网页重新打开时
        - 存储的内容依然被保留
        - localStorage.setItme : 设置
        - localStorage.getItem : 获取
  - sessionStorage
    - 会话存储 ,提供的是本次会话的存储, 临时存储
      - 在关闭掉会话时 , 存储的内容会被清除
      - sessionStorage.setItme : 设置
      - sessionStorage.getItme : 获取



### localStorage和sessionStorage的区别

1. 关闭网页后重新打开 , localStorage会保留 , 而 sessionStorage会被删除
2. 在页面内实现跳转 , localStorage会保留, sessionStorage也会保留
3. 在页面外实现跳转, localStorage会保留, sessionStorage不会被保留



# Storage常见的方法和属性

local (本地)  和session (会话)  都可以使用的方法和属性

- 属性
  - Storage.length : 只读属性
    - 返回一个整数 , 表示存储在Storage对象中的数据项数量
- 方法
  - Storage.key(index)
    - 该方法接受一个数值n作为参数 , 返回存储中的第n个key名称
  - Storage.getItem() 
    - 该方法接受一个key为参数, 并且返回key对应的value
  - Storage.setItme()
    - 该方法接受一个key和value, 并且将会把key和value添加到存储中
      - 如果key存储 , 则更新其对应的值
  - Storage.removeItem()
    - 该方法接受一个key作为参数 ,并把该key 从存储中删除
  - Storage.clear()
    - 该方法的作用是清空存储中的所有的key