# 什么是响应式

- 目前大部分都是对象的响应式
- 对象中的Value是一个值
  - 在定义对象后使用对象 , 调用了这个对象
    - 当这个对象的中的value发生变化时
    - 之前使用并调用对象的函数
      - 会再次重新执行
- 这种自动响应数据变量的代码机制，我们就称之为是响应式的
  - 就是当 数据发生变化时
    - 依赖数据的代码重新执行



# 响应式函数

- 封装一个新的函数WatchFn
  - 传入watchFn函数, 就是需要响应式的
  - 其他默认定义的函数都是不需要响应式的
  - 在定义一个数组, 进行保存



## 响应式依赖的收集

- 正常是将一个对象中所有的key属性放入一个reactiveFn中
  - 但是这导致不管对象中那个属性发生变化
    - 其他的函数都会执行
  - ![image-20240127100232049](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240127100232049.png)



- 应该让对象每一个属性存放在自己的reactiveFn中
  - ![image-20240127100556588](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240127100556588.png)
  - ![image-20240127101218708](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240127101218708.png)



- 