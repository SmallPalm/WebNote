# computed

- 当我们的某些属性是依赖其他状态时，我们可以使用计算属性来处理
-  在Composition API中
  - 我们可以在 setup 函数中使用 computed 方法来编写一个计算属性

**使用computed**

- 方式一
  - 接收一个getter函数，并为 getter 函数返回的值，返回一个不变的 ref 对象
- 方式二
  - 接收一个具有 get 和 set 的对象，返回一个可变的（可读写）ref 对象



# setup中使用ref

- 在setup中如何使用ref获取元素或者组件
  - 我们只需要定义一个ref对象
  - 绑定到元素或者组件的ref属性上即可
  - ![image-20231219220718283](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231219220718283.png)



# 生命周期钩子

- setup 可以用来替代 data 、 methods 、 computed 等等这些选项
  - 也可以替代 生命周期钩子
- 使用直接导入的 onX 函数注册生命周期钩子；
  - ![image-20231219220811289](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231219220811289.png)



# Provide函数

-  provide可以传入两个参数
  - name：提供的属性名称
  - value：提供的属性值
- 通过 provide 方法来定义每个 Property

# Inject函数

- 通过 inject 来注入需要的属性和对应的值
- inject可以传入两个参数
  - inject 的 property 的 name
  - 默认值

# 数据的响应式

- 为了增加 provide 值和 inject 值之间的响应性
  - 我们可以在 provide 值时使用 ref 和 reactive
  - ![image-20231219221119737](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231219221119737.png)



# 侦听数据的变化

- Options API中
  - 我们可以通过watch选项来侦听data或者props的数据变化
    - 当数据变化时执行某一些操作
- Composition API中
  - 我们可以使用watchEffect和watch来完成响应式数据的侦听

- **watchEffect**：用于自动收集响应式数据的依赖
- **watch**：需要手动指定侦听的数据源



# Watch的使用

- watch的API完全等同于组件watch选项的Property
  - watch需要侦听特定的数据源，并且执行其回调函数
  - 默认情况下它是惰性的
    - 只有当被侦听的源发生变化时才会执行回调
- **设置 deep**
  - **深层的侦听**
- immediate
  - 第一次立即执行

## watchEffect

- 侦听到某些响应式数据变化时
  - 我们希望执行某些操作，这个时候可以使用 watchEffect
- watchEffect传入的函数会被立即执行一次
  - 并且在执行的过程中会收集依赖
  - 只有收集的依赖发生变化时
    - watchEffect传入的函数才会再次执行
- watchEffect的停止侦听
  - 获取watchEffect的返回值函数，调用该函数即可

# script setup语法

- 是在单文件组件 (SFC) 中使用组合式 API 的编译时语法糖

  - 当同时使用 SFC 与组合式 API 时则推荐该语法
    - 更少的样板内容，更简洁的代码
    - 能够使用纯 Typescript 声明 prop 和抛出事件
    - 更好的运行时性能
      - 将template和script setup 在同一个作用域下
    - 更好的 IDE 类型推断性能 

- script setup里面的代码会被编译成组件 setup() 函数的内容

  - 这意味着与普通的 <script> 只在组件被首次引入的时候执行一次不同

  - <script setup> 中的代码会在每次组件实例被创建的时候执行

## 顶层的绑定会被暴露给模板

- 当使用 <script setup> 的时候
- 任何在 <script setup> 声明的顶层的绑定 
  - (包括变量，函数声明，以及 import 引入的内容)
  - 都能在模板中直接使用

## 导入的组件

- 范围里的值也能被直接作为自定义组件的标签名使用





# defineProps() : defineEmits()

- 为了在声明 props 和 emits 选项时获得完整的类型推断支持
- 我们可以使用 defineProps 和 defineEmits API
  - 它们将自动地在 <script setup> 中可用

# defineExpose()

- 使用 <script setup> 的组件是默认关闭的
  - 通过模板 ref 或者 $parent 链获取到的组件的公开实例
  - 不会暴露任何在 <script setup> 中声明的绑定
- 通过 defineExpose 编译器宏来显式指定在 <script setup> 组件中要暴露出去的 property