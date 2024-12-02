# React渲染流程

1. JSX

   ```react
   const element = <h2></h2>
   ```

   

2. 虚拟DOM

   ```react
    React.createElement("h2", null),
   ```

   

3. 真实DOM

   ```react
   <h2></h2>
   ```
   
   



# React更新流程

1. props / State 改变  
2. render 函数重新执行
3. 产生新的DOM数
4. 新旧DOM数进行Diff算法对比
5. 计算出差异, 进行DOM更新
6. 更新到真实DOM

理解

- React在Props和state发送改变时
  - 会调用React的Render方法
  - 会创建一颗不同的虚拟DOM树
- React需要基于这两颗不同的树之间的差别来判断如何有效的更新UI
  - 算法作用
    - 同层节点之间相互比较
      - 不会跨节点比较
    - 不同类型的节点
      - 产生不同的树结构
    - 开发中, 可以通过key来指定那些节点在不同的渲染下保持稳定

# key

- 当Foreach遍历列表时加入key属性
- 方式一 : 在列表最后位置插入数据
  - 这种情况, 有没有key意义不大
- 方式二: 在列表前面插入数据
  - 这种情况, 在没有key的情况下, 所有的列表都需要进行修改, 重新渲染
- 当列表拥有key时, React**使用key来匹配原有树上**的子元素以及**最新树上**的子元素 
  - 只会对需要改变的DOM做操作, 进行位移 , 插入即可

- key的注意事项
  - 每一个列表的key应该是唯一的
  - key不要使用随机数
  - 使用index作为key , 对性能是没有优化的

# render函数被调用

- 当一整个组件树中的其中一个组件的数据发生了改变时
  - 并不会所有的组件都需要重新render, 
    - 所有的进行diff算法 , 性能必然是很低的
-  事实上，很多的组件没有必须要重新render
  - 它们调用render应该有一个前提，
    - 就是依赖的数据（state、 props）发生改变时，再调用自己的render方法
- 生命周期中shouldComponentUpdate函数中返回的Boolean类型
  - 可以控制render方法是否被调用

# shouldComponentUpdate



简称 SUC优化

在render数据更新时 但componentDidUpdate函数还没有调用

- 该方法有两个参数
  1. nextProps : 修改之后, 最新的props属性
  2. nextState : 修改之后, 最新的state属性
- 该方法返回值是一个Boolean类型
  - 返回值为true, 就调用render方法
  - 返回值为false , 就不调用render方法
  - 默认返回true , 也就是state发生改变, 就会调用render方法
- 例子
  - 在state中增加一个message属性
  - JSX中并没有依赖这个message
    - 那么它的改变不应该引起重新渲染
  - 但是因为render监听到state的改变
    - 就会重新渲染
      - 所以最后render方法还是被重新调用了

# PureComponent

- 如果所有的类, 我们都需要手动来实现 shouldComponentUpdate
  - props或者state中的数据是否发生改变时
    - 决定shouldComponentUpdate来返回true或者false
- PureComponent默认帮我们实现好了shouldComponent方法



特点

- 浅比较 (Shallow Comparison)
  - `PureComponent`会自动实现`shouldComponentUpdate`方法
  - 进行比较当前Props和State 跟 下一个Props和State
    - 如果当前Props和下一个Props或当前State和下一个State是相同的
      - 组件就不会重新渲染
        - 从而提高渲染性能
  - Props主要是针对组件
- 性能优化
  - 在某些情况下，使用 `PureComponent` 可以减少不必要的渲染，
  - 特别是在父组件频繁更新但子组件 `props` 未变化的情况下。
  - 通过避免不必要的渲染，可以提高应用的性能。
- 限制
  - 由于 `PureComponent` 仅进行浅比较
  - 如果 `props` 或 `state` 是复杂的嵌套结构，对象或数组的深层次变化将不会被检测到。
  - 因此，使用 `PureComponent` 时需要确保 `props` 和 `state` 是不可变的（immutable）

## 与`Component` 的区别

**Component**

- 默认情况下不实现 `shouldComponentUpdate` 方法
  - 每次父组件重新渲染时，都会重新渲染子组件。
- 可以手动实现 `shouldComponentUpdate` 方法来控制组件是否需要更新

**PureComponent**

- 自动实现 `shouldComponentUpdate` 方法，使用浅比较来决定是否需要重新渲染
  - 不需要手动实现 `shouldComponentUpdate` 方法。

## shallowEqual方法

源码方法

- React 中用于浅比较两个对象的方法
- 通常用于实现像 `PureComponent` 这样的性能优化

# 高阶组件memo

- 针对类组件可以使用PureComponent继承, 控制那个组件重新渲染

- 针对函数组件可以使用memo

  - 事实上函数式组件在我们props没有改变时,
    - 也不希望其重新渲染其DOM树结构

- 使用高阶组件memo

  - 对函数式组件使用memo函数进行一层包裹, 即可

    ```react
    // 通过memo 包裹的组件，只有当组件的props发生变化时，才会重新渲染
    // 其他组件发送变化时, 当前组件不会发送渲染, 提高性能
    const Profile = memo(
      function Profile() {
      console.log("Profile组件渲染")
      return (
          <div>Profile</div>
        )
      }
    )
    ```

    

    

    

# 数据不可变的力量

- 不要直接去修改原state中的数据, 如果真的需要修改,
  - 把整个的数据全部指向的内存全部修改掉,
- PureComponent的特性: 做浅层比较时, 会比较当前内存地址
  - 所以需要将原数据引用的一份副本, 在副本中做修改, 再将副本赋值给state





# 如何使用ref

- 在React的开发模式中, 通常情况下不需要, 也不建议直接操作原生DOM
  - 但在某些特殊情况下, 确实需要获取到DOM的某些操作
    - 如 :
      - 管理焦点, 文本选择, 或媒体播放
      - 触发强制动画
      - 集成第三方DOM库
-  可以通过refs来获取原生DOM : 三种方式
  1. **传入字符串**
     - 使用时通过this.refs传入的字符串格式获取对应的元素
  2. **传入一个对象**
     - 对象是通过React.createRef()方式创建出来的
     - 使用时获取到创建的对象其中有一个current属性就是对应的元素
  3. **传入一个函数**
     - 该函数会在DOM被挂载时进行回调
       - 这个函数会传入一个元素对象
         - 我们可以进行保存
       - 使用时, 直接拿到进行操作即可

# ref的类型

- ref的值 , 根据节点的类型而有所不同
  - 当ref属性用于 HTML 元素时
    - 构造函数中使用React.createRef()  创建的ref接收底层DOM元素作为current属性
- 当ref属性用于自定义class组件时
  - ref对象接收组件的挂载实例作为其current属性
- **不能在函数组件上使用ref属性**,  因为函数组件没有实例

  - 1.ref无法获取函数式组件, 但可以获取函数式组件中的DOM元素

  - 2.因为函数式组件没有实例, 所以不能获取到对应的组件对象

  - 3.使用forwardRef()进行将函数包裹

  - 但是某些时候, 我们可能想要获取函数式组件中的某个DOM元素
    - 可以使用React.forwardRef

    ```react
    // forwardRef()中的回调函数中会传入两个参数props, ref
    const HelloWorld = forwardRef(function(props, ref) {
      return (
        <div ref={ref}>
          HelloWorld
        </div>
      )
    })
    ```




# ref的转发

- ref不能应用于函数式组件

- 因为函数式组件没有实例 , 所以不能获取到对应的组件对象

- 但是, 在开发中我们可能想要获取函数式组件中某个元素的DOM

  - 方式一: 直接传入ref属性 (错误的做法)

  - 方式二: 通过forward高阶函数

    ```react
    const Home = forwardRef(function (props, ref) {
      return (
      	<div>
        	<h2 ref={ref}>Home</h2>
        </div>
      )
    })
    ```



# Form

## 认识受控组件

- 在React中, 对Form表单元素和其他DOM元素不同
  - 因为表单元素通常会保存一些内部的state


如HTML表单元素

- DOM**默认**处理HTML表单的行为
  - 在用户点击提交时会提交到某个服务器中，并且刷新页面
- 在React中，并没有禁止这个行为，它依然是有效的
  - 通常情况下会使用JavaScript函数来方便的处理表单提交
  - 同时还可以访问用户填写的表单数据
- 这种效果的标准方式是使用**受控组件**

## 理解

- 非受控组件: 普通DOM中的表单元素
  - 在React中, 获取的state是做不了操作的
    - 因为表单元素内部会保存state
      - 所以在React中的state并不会跟随表单元素中内部value所更改
- 受控组件 : 表单元素
  - 表单元素绑定了React中的state
    - 并且绑定了事件
    - 在事件中获取表单元素中event
      - 将event中的value和React中state做绑定
  - 表单元素才会成功根据React的state做更改, 并渲染render



# 受控组件基本演练

- 表单元素通常自己维护state, 并根据用户输入进行更新

​	`跟React没有关系: 自己维护state: 称之为非受控组件`

- 而在React中, 可变状态 ( mutable state ) 通常保存在组件的state属性中
  - 并且只能通过使用setState() 来更新	
    - 我们将两者结合起来, 使React中state成为唯一数据源
    - 渲染表单的React组件还控制这用户输入过程中表单发生的操作
    - 被**React以这种方式控制取值的表单输入元素**就叫做受控组件
- 由于在表单元素上设置了 value 属性，因此显示的值将始终为 this.state.value，这使得 React 的 state 成为唯一数据源



# 非受控组件

- React推荐大多数情况下使用 受控组件 来处理表单数据
  - 一个受控组件中, 表单数据是由React组件来管理的
  - 另一种替代方案是使用非受控组件
    - 这时表单数据将交给DOM节点来处理
  - 在非受控组件中通常使用defaultValue来设置默认值
  - <input type='checkbox'> 和 <input type='radio'> 
    - 支持defaultCheckbox
  - \<select\> 和 \<textarea\> 
    - 支持 defaultValue

# 认识高阶组件

- 什么是就高阶函数
  - 接受一个或者多个函数作为输入(参数)
  - 输出(返回) 一个函数
- 高阶组件
  - 高阶组件的英文 Higher - Order Components
  - 官方的定义 : 高阶组件是参数为组件, 返回值为新组件的函数
- 高阶组件本身不是一个组件 , 而是一个函数
  - 这个函数的参数是一个组件, 返回值也是一个组件

> 高阶组件本身不是一个组件, 而是一个函数

# 高阶组件的定义

- 高阶函数的调用过程

  ```react
  const EchancedComponent = higherOrderComponent(WrappedComponent)
  ```

- 高阶函数的编写过程

  ```react
  // 传入函数组件
  function higherOrderComponent(WrapperComponent) {
    class NewComponent extendes PureComponent {
      render() {
        return <WrapperComponent></WrapperComponent>
      }
    }
    
    NewComponent.displayName = 'CoderLi'
    // 返回函数组件
    return NewComponent
  }
  ```



- 组件的名称
  - 在ES6中, 类表达式中类名是可以省略的
  - 组件的名称都可以通过displayName来修改



- 高阶组件并不是React API 的一部分
  - 它是基于React的组合特性而形成的设计模式
- 高阶组件在一些React第三方库中非常常见
  - 如: redux中的connect
  - 如: react-router 中的 withRouter



# 高阶函数的意义

- 利用高阶组件可以针对某些React代码进行更优雅的处理
- 其实早期的React有提供组件之间的一种复用方式的mixin
  - Mixin可能会相互依赖, 相互耦合, 不利于代码维护
  - 不同的Mixin中的方法可能会相互冲突
  - Mixin非常多时, 组件处理起来会比较麻烦
    - 甚至还要为其做相关处理
    - 这样会给代码造成滚雪球式的复杂性

高阶组件 HOC : 缺陷

- HOC需要在原组件上进行包裹或者嵌套
  - 如果大量使用HOC , 将会产生非常多的嵌套
  - 这让调试变得非常困难
- HOC可以劫持props, 在不遵守约定的情况下也可能造成冲突



# 高阶组件与Ref

- 因为高阶组件是由一个函数组成
- 那么在函数中会丢失类组件的实例
- Ref就会绑定不到
  - ref不能应用于函数式组件
  - 因为函数式组件没有实例，所以不能获取到对应的组件对象
  - 在高阶组件中的类组件也会丢失实例
- 这时就需要通过forwardRef高阶函数
  - 进行包裹

# Portals的使用

- 某些情况下，我们希望渲染的内容独立于父组件
  - 甚至是独立于当前挂载到的DOM元素中
  - 默认都是挂载到id为root的DOM 元素上的

Portal 提供了一种将子节点渲染到存在于父组件以外的 DOM 节点的

- ReactDOM.createPortal(child, container); 

从组件的 render 方法返回一个元素时，

该元素将被挂载到 DOM 节点中离其最近的父节点

child: 元素或组件

container : 需要挂载到那个容器中或那个DIV中



# fragment

- 一个组件中返回内容时包裹一个div元素
  - 希望可以不渲染这样一个div
    - 使用Fragment
- Fragment 允许你将子列表分组，而无需向 DOM 添加额外节点
- fragment的语法糖<></> 
  - 如果我们需要在Fragment中添加key，那么就不能使用短语法



# StrictMode

严格模式

严格模式检查仅在开发模式下运行；它们不会影响生产构建；

- StrictMode是一个用来突出显示应用程序中潜在问题的工具
- 与 Fragment标签 一样，StrictMode标签 不会渲染任何可见的 UI；

## 严格模式检查

1. 识别不安全的生命周期
   - 对React的中一些过期或不在维护的生命周期弹出警告
2. 使用过时的ref API
   - 过时API
3. 检查意外的副作用
   - 副作用（side effects）是指在组件渲染过程中发生的操作，可能会影响到组件外部的状态或是引发副作用
   - 这个组件的constructor会被调用两次
     - 这是严格模式下故意进行的操作
       - 让你来查看在这里写的一些逻辑代码被调用多次时，是否会产生一些副作用； 
     - 当然在生产环境中，是不会被调用两次的；
4. 使用废弃的findDOMNode方法
   - 在之前的React API中，可以通过findDOMNode来获取DOM
5. 检测过时的Context API
   - 
