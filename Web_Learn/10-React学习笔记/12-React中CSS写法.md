# 组件化天下的CSS

组件化使用CSS条件

1. 局部CSS
   - css具备自己的具备作用域，不会随意污染其他组件内的元素
2. 动态的CSS
   - 可以获取当前组件的一些状态，根据状态的变化生成不同的css样式
3. 支持所有的CSS特性
   - 伪类、动画、媒体查询等





# React中的CSS

css一直是React的痛点，也是被很多开发者吐槽、诟病的一个点

React官方并没有给出在React中统一的样式风格

从普通的css，到css modules，再到css in js，有几十种不同的解决方案，上百个不同的库





# 内联样式

内联样式是官方推荐的一种css样式的写法

- style 接受一个采用小驼峰命名属性的 JavaScript 对象，，而不是 CSS 字符串
- 并且可以引用state中的状态来设置相关的样式

内联样式的优点

- 1.内联样式, 样式之间不会有冲突
- 2.可以动态获取当前state中的状态

内联样式的缺点

- 1.写法上都需要使用驼峰标识
- 2.某些样式没有提示 
- 3.大量的样式, 代码混乱 
- 4.某些样式无法编写(比如伪类/伪元素)



# 普通的CSS

- 编写到一个单独的文件，之后再进行引入到JSX文件中
  - 最大的问题是样式之间会相互层叠掉



# css modules

- cs
- s modules并不是React特有的解决方案
  - 而是所有使用了类似于webpack配置的环境下都可以使用的。

React的脚手架已经内置了css modules的配置

- .css/.less/.scss 等样式文件都需要修改成 .module.css/.module.less/.module.scss 等
- css modules确实解决了局部作用域的问题

**css modules缺陷**

- 引用的类名，不能使用连接符(.home-title)，在JavaScript中是不识别的
- 所有的className都必须使用{style.className} 的形式来编写
- 不方便动态来修改某些样式，依然需要使用内联样式的方式



# 认识CSS in JS 模式

- CSS in JS 是指一种模式, 其中CSS 由 JavaScript生成而不是在外部文件定义
  - 此功能并不是 React 的一部分，而是由第三方库提供

在传统的前端开发中，我们通常会将结构（HTML）、样式（CSS）、逻辑（JavaScript）进行分离。

- React的思想中认为逻辑本身和UI是无法分离的，所以才会有了JSX的语法
  - **样式也是属于UI的一部分**
- 事实上CSS-in-JS的模式就是一种将样式（CSS）也写入到JavaScript中的方式
  - 并且可以方便的使用JavaScript的状态

CSS-in-JS通过JavaScript来为CSS赋予一些能力

- 类似于CSS预处理器一样的样式嵌套、函数定义、逻辑复用、动态修改状态等等



# CSS in JS库

## styled-components

# ES6标签模板字符串

模板字符串还有另外一种用法：标签模板字符串（Tagged Template Literals）。

正常情况下，我们都是通过 函数名() 方式来进行调用的，其实函数还有另外一种 调用方式：

```js
// 标签模板字符串
const name = 'limgbnyu'
const age = 12

// 基本使用
const str = `my name is ${name}, age is ${age}`
console.log(str)

function foo(...args) {
  console.log(...args)
}

// foo(): 小括号方式调用: 常用
// foo``: 模板字符串方式调用

// ``中传入参数，进行调用
foo`my name is ${name} and age is ${age} 111`

```



如果我们在调用的时候插入其他的变量

- 模板字符串被拆分了； 
- 第一个元素是数组，是被模块字符串拆分的字符串组合； 
- 后面的元素是一个个模块字符串传入的内容； 

在styled component中，就是通过这种方式来解析模块字符串，最终生成我们想要 的样式的







# styled的基本使用

styled-components的本质是通过函数的调用

最终 创建出一个组件：

 这个组件会被自动添加上一个不重复的class

styled-components会给该class添加相关的样式

它支持类似于CSS预处理器一样的样式嵌套： 

- 支持直接子代选择器或后代选择器，并且直接编写 样式； 
- 可以通过&符号获取当前元素； 
- 直接伪类选择器、伪元素等；

```js
// 4.可以通过attrs给标签模板字符串中提供的属性 
// 4.1:需要在attrs中传入函数定义默认值
export const AppWrapper = styled.div.attrs((props) => {
  console.log("attrs", props)
  return {
    acolor: props.color ?? '#aaa',
    asize: props.size || 18,
  };
})`
  /* 获取props需要使用箭头函数获取 */
  font-size: ${(props) => {
    console.log("props", props);
    return props.asize;
  }}px;
  // 如何是空值, 需要有默认值,或进行判断
  color: ${(props) => props.acolor};

  .app {
    color: #f00;
    border: 1px dashed #f00;

    &:hover {
      color: #0f0;
      background-color: #f00;
    }
  }
`;
```







# classNames库

```jsx
export class App extends PureComponent {
  render() {
    return (
      <Fragment>
        <AppWrapper>
          {/* classNames('take', 'easy') => 'take easy' */}
          <h2 className={classNames('take', 'easy')}> Take is easy - 放轻松 </h2>
          <h2 className={classNames('hard', {problem: true})}> No problem </h2>
          <button className={classNames({'btn-active': true}, {'btn': false})}>按钮</button>
          <p className={classNames([null, false, 'p', undefined, {'p-active': 0}, {"kkkk": undefined, 'kkkk-active': null, 'kkkk-a': '', key: '1222', ooo: true}])}>Hang in there - 坚持下去</p>
          <p className={classNames(null, false, 'p', undefined, {'p-active': 0}, {"kkkk": undefined, 'kkkk-active': null, 'kkkk-a': '', key: '1222', ooo: true})}>Hang in there - 坚持下去</p>
        </AppWrapper>
      </Fragment>
    )
  }
}
```

