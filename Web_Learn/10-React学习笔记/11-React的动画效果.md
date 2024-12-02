# react-transition-group插件

添加过渡动画

React社区提供的react-transition-group用来完成过渡动画



主要包含四个组件

1. Transition : 不常用 : 通常直接使用CSS的Transition
2. CSSTransition
   - 在前端开发中，通常使用CSSTransition来完成过渡动画效果
3. SwitchTransition
   - 两个组件显示和隐藏切换时，使用该组件
4. TransitionGroup
   - 将多个动画组件包裹在其中，一般用于列表中元素的动画；



# CSSTransition

- CSSTransition是基于Transition组件构建的
- CSSTransition执行过程中, 有三个状态: appear, enter , exit

appear : 刷新页面时动画: 第一次展示时动画

enter : 隐藏后展示动画

exit : 隐藏动画

- 它们有三种状态, 需要定义对应的CSS样式

第一类，开始状态：对于的类是 -appear、 -enter、-exit； 

第二类：执行动画：对应的类是 -appear-active、-enter-active、-exit-active； 

第三类：执行结束：对应的类是 -appear-done、 -enter-done、-exit-done；

- CSSTransition常见对应的属性
- in : 触发进入或退出的状态 : boolean类型
  -  当in为true时
  - 触发进入状态，会添加-enter、-enter-acitve的class开始执行动画当动画执行结束后，会移除两个class， 并且添加-enter-done的class；
  - 当in为false时
  - 触发退出状态，会添加-exit、-exit-active的class开始执行动画，当动画执行结束后，会移除两个class，并 且添加-enter-done的class；
- unmountOnExit : 该属性会在执行退出动画结束后移除掉该组件
- classNames : 动画class的名称
  - 决定了在编写css时，对应的class名称：如card-enter、card-enter-active、card-enter-done
- timeout : 过渡动画的时间
- appear : 是否在初次进入添加动画 (需要和in同时为true)

CSSTransition对应的钩子函数

主要为了检测动画的执行过程，来完成一些JavaScript的操作

- onEnter：在进入动画之前被触发； 
- onEntering：在应用进入动画时被触发； 
- onEntered：在应用进入动画结束后被触发；



# SwitchTransition

- SwitchTransition可以完成两个组件之间切换的炫酷动画

属性

- mode
  - in-out : 表示新组件先进入，旧组件再移除
  - out-in : 表示就组件先移除，新组建再进入

使用SwitchTransition

- SwitchTransition组件里面要有CSSTransition或者Transition组件
  - 不能直接包裹想要切换的组件
- SwitchTransition里面的CSSTransition或Transition组件不再像以前那样接受in属性来判断元素是何种状态
  - 取而代之的是key属性

# TransitionGroup

CSSTransition放入到一个TransitionGroup中来完成动画

```react
render() {
  return (
    <TransitionGroup>
    {
    	this.state.friends.map((item, index) => {
        return (
        	<CSSTransition key={index} timeout={2000} classNames={friend}>
          	<div>{item}</div>
          </CSSTransition>
        )
      })    
    }
    </TransitionGroup>
  )
}
```



