# 异步任务的处理

- 调用一个函数, 这个函数中发送网络请求 
  - 如果发送网络请求成功了 , 
    - 那么告知调用者发生成功 , 并且将相关数据返回过去
  - 如果发送网络请求失败了 , 
    - 那么告知调用者发生失败  , 并且告知错误信息
- 我们需要自己来设计回调函数, 回调函数的名称 , 回调函数的使用 
- 对于不同的人 , 不同的框架设计出来的方案是不同的 , 
  - 那么我们必须去耐心的看别人的源码或者文档, 以便可以理解它的这个函数到底怎么用

# Promise

- Promise是一个类, ( :  承诺, 许诺 , 期约)
- 当我们需要的时候 , 给予调用者一个承诺
  - 待会儿我会给你回调数据时 ,  就可以创建一个Promise的对象
- 在通过new 创建 Promise对象时 , 我们 需要传入一个回调函数, 
  - 称之为executor : 执行者
- 这个回调函数会被立即执行 , 并且给传入另外两个回调函数 resolve ,  reject
- 当我们调用resolve回调函数时,
  - 会执行Promise对象的then方法传入的 回调函数
- 当我们调用reject回调函数时, 
  - 会执行Promise对象的catch方法传入的回调函数



# Promise代码结构

- ```js
  const promise = new promise( (resolve, reject)=>{
    //代码执行体
  
    //resolve()
    
    //reject()  
  })
  
  promise.then( () =>{
    "成功"
  })
  promise.carch( ()=>{
    "失败"
  })
  ```

- Promise使用过程, 划分为三个状态

  - 待定 ( pending) : 初始状态 ,  既没有被兑现 , 也没有被拒绝
    - 当执行executor中的代码时, 处于该状态
      - 代码执行体
  - 已兑现 ( fulfilled ) : 意味着操作成功完成
    - 执行了resolve时, 处于该状态 , Promise已经被兑现
      - 调用resolve时, 那么then的回调就会被执行
  - 已拒绝 ( rejected) : 意味着操作失败
    - 执行了reject时, 处于该状态, Promise已经被拒绝
      - 调用resolve时, 那么catch的回调就会被执行



# Executor

- Executor是在创建Promise时需要传入的一个回调函数
  - 这个回调函数就会被立即执行, 并且传入两个参数
- 通常我们会在Executor中确定我们的Promise状态
  - 通过resolve , 可以兑现 (fulfilled) Promise的状态 
    - 我们也可以称之为已决议 (resolve)
  - 通过reject , 可以拒绝 (rejected) Promise的状态
- 注意: 一旦状态被确定下来, Promise的状态会被锁死 ,
  - 该Promise的状态是不可更改的
- 在我们调用resolve的时候 , 如果resolve传入的值本身不是一个Promise
  - 那么会将该Promise的状态变为兑现
- 在之后我们去调用reject时, 已经不会有任何的响应了
  - 并不是代码不能执行 , 而是无法改变Promise状态了



# resolve不同值的区别

- 情况一
  - 如果resolve传入一个普通的值或对象, 
    - 那么这个值会作为then回调的参数
- 情况二
  - 如果resolve中传入的是另外一个Promise
    - 那么这个新Promise 会决定 原Promise的状态
- 情况三
  - 如果resolve中传入的是一个对象 , 并且这个对象有实现then方法
    - 那么会执行该then方法 , 并且根据then方法的结果来决定Promise的状态



# then方法

- then方法是Promise对象上的一个方法 ( 实例方法 )
  - 它其实是放在Promise的原型上的 Promise.prototype.then
- then方法接受两个参数
  - fulfilled的回调函数
    - 当状态变成fulfilled时会回调的函数
  - reject的回调函数
    - 当状态变成reject时会回调的函数

**返回值**

-  then方法本身是有返回值的 , 它的返回值是一个Promise, 所以我们可以链式调用

# catch方法

- catch方法也是Promise对象上的一个实例方法
  - 它其实是放在Promise的原型上的 Promise.prototype.catch
- 一个Promise的catch方法是可以被多次调用的
  - 每次调用我们都可以传入对应的reject回调
  - 当Promise的状态变成reject的时候 , 这些回调函数都会被执行

**返回值**

- catch方法也是会返回一个Promise对象的. 
  - 所以catch方法后面我们可以继续调用then方法或者catch方法  
- 执行完catch方法
  - 返回一个promise
    - 可以继续执行then方法
  - 希望继续执行catch方法, 需要抛出一个异常



# finally方法

- finally是在ES9中新增的一个特性
  - 表示无论Promise对象无论变成fulfilled还是rejected状态
    - 最终都会被执行的代码
- finally方法是不接受参数的 
  - 因为无论前面是fulfilled状态, rejected状态 , 它都会执行



# resolve方法

- 前面我们学习的then, catch , finally 方法, 都是属于Promise的实例方法
  - 都是存放在Promise的prototype上的
- 当我们已经 有一个现成的内容
  - 希望将其转成Promise来使用 , 这个时候我们可以使用**Promise.resolve**方法来完成
- Promise.resolve的用法相当于一个new Promise 并且执行resolve操作
- resolve参数
  - 参数是一个普通的值或对象
  - 参数本身是Promise
  - 参数是一个thenable

# reject方法

- reject方法类似于resolve方法
  - 只是会将Promise对象的状态设置为reject状态
- Promise.resolve的用法相当于一个new Promise 并且执行reject操作



# all的方法

- Promise.all
- 它的作用是将多个Promise包裹在一起形成一个新的Promise
- 新的Promise状态由包裹的所有Promise共同决定的
  - 当所有的Promise状态变成fulfilled状态时
    - 新的promise状态为fulfilled
      - 并且会将所有的Promise的返回值组成一个数组
  - 当有一个Promise的状态为reject时, 新的Promise状态为reject
    - 并且会将第一个reject的返回值作为参数

# allSettled方法

- all方法缺陷
  - 当有其中一个Promise变成reject状态时, 新Promise就会立即变成对应的reject状态
    - 那么对于resolve的 , 以及依然处于pending状态的Promise, 我们是获取不到对应的结果的
- 在ES11中添加了新的API
  - **Promise.allSettled**
- 该方法会在所有的Promise都有结果
  - 无论是fulfilled, 还是rejected时 , 都会有最终的状态
    - 并且这个返回的all的Promise的结果一定是一个fulfilled的
- allSettled的结果是一个数组, 数组中存放这着每一个Promise的结果
  - 并且每一个Promise对应一个对象
    - 这个对象中包含status状态 , 以及对应的value值

# race方法

- 如果有一个Promise有了结果 , 我们就希望决定最终新的Promise的状态, 那么可以使用race方法
  - race是竞技, 竞赛的意思 , 表示多个Promise相互竞争, 谁先有结果, 那么就使用谁的结果

# any方法

- any方法是ES12中新增的方法, 和race方法类似
  - any方法会等到一个fulfilled状态
    - 才会决定新Promise的状态, 只会返回fulfilled状态
  - 如果所有的Promise的reject的
    - 那么也会等到所有的Promise都变成rejected状态
      - 会报一个AggregateError的错误