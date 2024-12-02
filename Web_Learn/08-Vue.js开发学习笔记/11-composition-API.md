# Options API的弊端

- 在Vue2中 , 我们编写组件的方法是Options API

  - Options API的一大特点
    -  在对应的属性中编写对应的功能模块
  - Date定义数据
  - methods中定义方法
  - computed中定义计算属性
  - watch中侦听数据 属性的变化
  - 也包括生命周期钩子

- 弊端

  - 当我们**实现某一个功能**时
    - 这个功能**对应的代码逻辑**会被**拆分到各个属性**中
    - 当我们组件变得更大 , 更复杂时
    - **逻辑关注点的列表**就会增长
      - 那么**同一个功能的逻辑就会被拆分的很分散**

  - 会对阅读组件的其他人
    - 这个组件的代码是难以阅读和理解的

- 这种碎片化的代码使用理解和维护这个复杂的组件变得异常困难

  - 并且隐藏了潜在的逻辑问题

- 并且当我们处理单个逻辑关注点时

  - 需要不断的跳到相应的代码块中

- 我们能将**同一个逻辑关注点相关的代码收集在一起会更好**

  - 这就是Composition API想要做的事情
    - 以及可以帮助我们完成的事情

- Vue CompositionAPI简称为**VCA**



# 认识Composition-API

-  开始使用Composition API
  - 在Vue组件中，这个位置就是 setup 函数
- **setup其实就是组件的另外一个选项**
  - 只不过这个选项强大到我们可以用它来替代之前所编写的大部分其他选项
  - 如methods、computed、watch、data、生命周期等等



# setup函数的参数

- setup函数的参数，它主要有两个参数
  - 第一个参数
    - props
  - 第二个参数
    - content

**props**

- **父组件传递过来的属性**会被**放到props对象**中
- 在setup中如果需要使用
  - 那么就可以直接通过props参数获取
- 对于定义props的类型
  - 我们还是和之前的规则是一样的
    - 在props选项中定义
  -  并且在template中依然是可以正常去使用props中的属性
- 如果我们在setup函数中想要使用props传递过来的参数
  - 不可以通过this去获取
- props有直接作为参数传递到setup函数中
  - 所以我们可以直接通过参数来使用即可
  - 如 props.message

**context**

- 也称之为是一个**SetupContext**
  - 它里面**包含三个属性**
- attrs
  - 所有的非prop的attribute
- slots
  - 父组件传递过来的插槽
    - 在以渲染函数返回时会作用
- emit
  - 当我们组件内部需要发出事件时会用到emit
    - 因为我们不能访问this
      - 所以不能通过this.$emit发出事件

# setup的返回值

- setup的返回值
  - 可以在模板template中被使用
  - 可以通过setup的返回值来替代date选项
- 可以返回一个执行函数来代替在methods中定义的方法
- 这是因为对于一个定义的变量来说
  - 默认情况下
    - Vue并不会跟踪它的变化
      - 来引起界面的响应式操作

# Reactive

- 最主要定义复杂类型的数据 : 如对象 : 数据

- 如果想为在setup中定义的数据提供响应式的特性
  - 可以使用Reactive函数
- 在使用reactive函数处理我们的数据之后
  - 数据再次被使用时就会进行依赖收集
    - 就是被proxy代理
- 当**数据发生改变**时
  - 所用**收集到依赖**都是进行**对应的响应式操作**
- 在OptionsAPI中data选项
  - 在内部也是交给了reactive函数
    - 来将其变成响应式对象的
- reactive API对**传入的类型是有限制的**
  - 它要求我们必须传入的是**一个对象或者数组类型**
- 如果我们传入一个基本数据类型
  - String、Number、Boolean
    - 会报一个警告

# Ref

- Vue3提供了另外一个API的 ref API
  - ref会返回一个可变的响应式对象
    - 该对象作为一个**响应式的引用**
      - 维护着它内部的值
      - 这就是ref名称的来源
    - 它内部的值是在被ref的value属性中被维护
- 这里有两个注意事项
  - 在template模板中引入ref的值时
    - Vue会自动帮助我们进行解包操作
    - 所以我们并不需要在模板中通过 ref.value 的方式来使用
  - 但是在 setup 函数内部
    - 它依然是一个 ref引用，
    - 所以对其进行操作时
    - 我们依然需要使用 ref.value的方式

## Ref自动解包

- **模板中的解包是浅层的解包**
  - **将ref放到一个reactive的属性**当中
  - 那么**在模板中使用时**
  - **它会自动解包**：

# 单向数据流

- 这是一种默认的代码规范
- 在showinfo子组件中修改了app传递的对象
- 可行但不允许的
  - 是不规范的
  - 这是单向数据流(这是一种规范)
- 子组件拿到数据后只能使用, 不能修改
- 如果确定到修改
  - 那么需要将事件传递给父组件
  - 由父组件来修改数据
- 因为父组件中可以传递给很多个子组件数据
  - 如果随便子组件都可以修改数据
  - 不好查询在那个组件中修改了数据
  - 其他组件修改了数据
    - 只要使用的所用组件以及父组件都会被改变
- 代码没有错误
  - 但是违背了规范(单项数据流)

# readonly

- 我们通过reactive或者ref可以获取到一个响应式的对象
  - 但是某些情况下
  - 我们传入给其他地方或组件的这个响应式对象
    - 希望在另一个地方组件被使用
    - 但是不能被修改
      - 单项数据流
    - 这个时候然后防止这个情况
- vue3为我们提供了readonly的方法
- readonly会返回原始对象的只读代理
  - 也就是它依然是一个Proxy
  - 这是一个proxy的set方法被劫持
  - 并且不能对其进行修改
- 在开发中常见的readonly方法会传入三个类型的参数
  - 类型一：普通对象
  - 类型二：reactive返回的对象
  - 类型三：ref的对象

## readonly的使用

- readonly返回的对象都是不允许修改的
- 但是经过readonly处理的原来的对象是允许被修改的
  - 比如 const info = readonly(obj)，info对象是不允许被修改的
  - 当obj被修改时，readonly返回的info对象也会被修改
  - 但是我们不能去修改readonly返回的对象info
- 本质上就是readonly返回的对象的setter方法被劫持了而已
-  在我们传递给其他组件数据时
  - 往往希望其他组件使用我们传递的内容
  - 但是不允许它们修改时，就可以使用readonly了



# Reactive判断的API

- **isProxy**
  - 检查对象是否是由 reactive 或 readonly创建的 proxy

- **isReactive**
  - 检查对象是否是由 reactive创建的响应式代理
  - 如果该代理是 readonly 建的
    - 但包裹了由 reactive 创建的另一个代理
      - 它也会返回 true；

- **isReadonly**
  - 检查对象是否是由 readonly 创建的只读代理

- toRaw
  - 返回 reactive 或 readonly 代理的原始对象
  - 不建议保留对原始对象的持久引用。请谨慎使用

- shallowReactive : 浅层的响应式
  - 创建一个响应式代理
  - 它跟踪其自身 property 的响应性
  - 但不执行嵌套对象的深层响应式转换 
    - 深层还是原生对象

- shallowReadonly : 浅层的自读
  - 创建一个 proxy
  - 使其自身的 property 为只读
  - 但不执行嵌套对象的深度只读转换
    - 深层还是可读、可写的




# toRefs

- 如果我们使用ES6的解构语法
- 对reactive返回的对象进行解构获取值
  - 那么之后无论是修改结构后的变量
- 还是修改reactive返回的state对象
  - 数据都不再是响应式的

让我们解构出来的属性是响应式

- Vue为我们提供了一个toRefs的函数
  - 可以将reactive返回的对象中的属性都转成ref
- 我们再次进行结构出来的 name 和 age 本身都是 ref 的
- 相当于已经在state.name和ref.value之间建立了 链接
  - 任何一个修改都会引起另外一个变化

# toRef

- 只希望转换一个**reactive对象中的属性为ref**,
  - 那么可以**使用toRef的方法**

# Ref其他的API

- unref
  - 如果我们想要**获取一个ref引用中的value**
    - 那么也可以**通过unref方法**

  - 如果参数是一个 ref，则返回内部值
    - 否则返回参数本身

  - 这是 val = isRef(val) ? val.value : val  本质就是这个代码

- isRef
  - 判断值是否是一个ref对象

- shallowRef
  - 创建一个浅层的ref对象

- triggerRef
  - 手动触发和 shallowRef 相关联的副作用


# setup不可以使用this

- 官方关于this有这样一段描述
  - 表达的含义是this并没有指向当前组件实例
  -  并且在setup被调用之前
    - data、computed、methods等都没有被解析
      - 调用时, 被创建了 ,但是没有被解析
    - 所以无法在setup中获取this



