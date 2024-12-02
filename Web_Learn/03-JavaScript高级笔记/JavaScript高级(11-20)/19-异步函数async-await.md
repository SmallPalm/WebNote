# 异步函数 async function

- async关键字用于声明一个异步函数
  - async是 asynchronous 单词的缩写 : 异步 , 非同步的
  - sync是 synchronous 单词的缩写 : 同步, 同时



# 异步函数的执行流程

- 异步函数的内部代码执行过程和普通的函数是一致的
  - 默认情况下也是会被同步执行的
  - 不会阻塞后面代码
- 异步函数的返回值 , 和普通函数会有区别
  - 情况一 : 异步函数也可以有返回值 , 
    - 但是异步函数的返回值相当于被包裹到 Promise.resolve 中
  - 情况二 : 如果我们的异步函数的返回值是Promise
    - 状态由会Promise决定
  - 情况三 : 如果我们的异步函数的返回值是一个对象并且实现了 thenable
    - 那么会由对象的then方法来决定
- 如果我们在async中抛出了异常 , 那么程序它并不会像普通函数一样报错
  - 而是会作为Promise中的reject来传递

# await关键字

- async函数另外一个特殊之处 ,  就是可以在它的内部使用await关键字
  - 而普通函数是不可以使用
- await关键字有什么特点
  - 通常使用await是后面会跟上一个表达式
    - 这个表达式会返回一个Promise
      - 返回的Promise, 那么会等待Promise后续有了结果  结果的fulfilled状态
        - 才会继续执行后续
  - 那么await会等到Promise的状态变成fulfilled状态
    - 之后继续执行异步函数
- 如果await后面是一个普通的值
  - 那么会直接返回这个值
- 如果await后面是一个thenable对象
  - 那么会根据对象的then方法调用来决定后续的值
- 如果await后果的表示式
  - 返回的是promise是reject的状态
    - 那么会将这个reject 结果直接作为函数的Promise的reject值

异步函数await-asyns天然返回一个promise