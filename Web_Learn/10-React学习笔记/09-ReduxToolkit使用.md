# 认识Redux Toolkit

Redux Toolkit 是官方推荐的编写 Redux 逻辑的方法

- redux的编写逻辑过于的繁琐和麻烦
- 并且代码通常分拆在多个文件中（虽然也可以放到一个文件管理，但是代码量过多，不利于管理）
- Redux Toolkit包旨在成为编写Redux逻辑的标准方式，从而解决上面提到的问题；
- 在很多地方为了称呼方便，也将之称为“RTK”

```bash
// RTK只是优化redux代码，并不能全局应用store，还是需要react-redux
npm install @reduxjs/toolkit react-redux
```





# Redux Toolkit的核心API

- configureStore：包装createStore以提供简化的配置选项和良好的默认值。
  - 它可以自动组合你的 slice reducer，添加你提供 的任何 Redux 中间件
  - redux-thunk默认包含，并启用 Redux DevTools Extension。
- createSlice：接受reducer函数的对象、切片名称和初始状态值，并自动生成切片reducer，并带有相应的actions。
- createAsyncThunk: 接受一个动作类型字符串和一个返回承诺的函数
  - 并生成一个pending/fulfilled/rejected基于该承诺分派动作类型的 thunk
  - 主要用于异步操作，网络请求等

# createSlice

createSlice主要包含如下几个参数：

- name：用户标记slice的名词
  - 在之后的redux-devtool中会显示对应的名词； 
- initialState：初始化值
  - 第一次初始化时的值； 
- reducers：相当于之前的reducer函数 
  - 对象类型，并且可以添加很多的函数；
  - 对象中的函数类似于redux原来reducer中的一个case语句；
    -  函数的参数： ✓ 参数一：state ✓ 参数二：调用这个action时，传递的action参数；

 createSlice返回值是一个对象，包含所有的actions；

```jsx
const counterSlice = createSlice({
  // 在redux-devtools中区别其他module的name
  name: "counter",
  initialState: {
    counter: 666
  },
  //相当于之前的reducer函数
  reducers:{
    // actionCreator方法
    addCounterAction(state, action) {
      console.log(action)
      // 在toolkit中可以直接修改state值, 因为toolkit中使用了一个immerJs库, 可以将数据持为可变数据
      // 当数据被修改时，会返回一个对象，但是新的对象会尽可能的利用之前的数据结构而不会对内存造成浪费
      state.counter += action.payload
    },
    subCounterAction(state, { payload }) {
      state.counter -= payload
    }
  }
})
```





# Redux Toolkit异步操作

- Redux Toolkit默认已经给我们继承了Thunk相关的功能：createAsyncThunk

```jsx
export const getMultiDataAction = createAsyncThunk(
  'multiData', 
  async (extraInfo, store) => {
    console.log(extraInfo, store)

    const res = await axios.get('http://123.207.32.32:8000/home/multidata')

    return res.data
  }
)
```

当createAsyncThunk创建出来的action被dispatch时，会存在三种状态

pending：action被发出，但是还没有最终的结果； 

fulfilled：获取到最终的结果（有返回值的结果）； 

rejected：执行过程中有错误或者抛出了异常；

```jsx
extraReducers: (builder) => {
  console.log("builder", builder)
  // 第二种写法
  builder.addCase(getMultiDataAction.pending, (state, action) => {
    console.log("getMultiDataAction.pending")
  }).addCase(getMultiDataAction.fulfilled, (state, action) => {
    console.log("getMultiDataAction.fulfilled")
    state.banners = action.payload.data.banner.list
    state.recommends = action.payload.data.recommend.list
  }).addCase(getMultiDataAction.rejected, (state, action)=> {
    console.log("getMultiDataAction.rejected")
  })
}
```



# Redux Toolkit的数据不可变性

在React开发中，我们总是会强调数据的不可变性

- 无论是类组件中的state，还是redux中管理的state；
- 事实上在整个JavaScript编码过程中，数据的不可变性都是非常重要的；

在redux中我们经常会进行浅拷贝来完成某些操作，但是浅拷贝事实上也是存在问题的

- 比如过大的对象，进行浅拷贝也会造成性能的浪费；
- 比如浅拷贝后的对象，在深层改变时，依然会对之前的对象产生影响；

Redux 强调不可直接修改 `state`，因为这样可以保证应用状态的可追溯性和可预测性。

但是在 Redux Toolkit 中，reducers 看起来可以直接修改 `state`

- 这是因为**Redux Toolkit底层使用了immerjs的一个库来保证数据的不可变性**

## Immer.js 是如何工作的？

`Immer.js` 通过代理 (Proxy) 实现了不可变数据的管理。

它允许你在 reducer 中像普通对象一样“修改”状态，但实际上并没有直接改变原始的 `state`。`Immer.js` 在幕后进行以下工作：

1. **代理拦截**：当你“修改” `state` 时，`Immer.js` 使用代理对象捕捉这些修改，并记录下所有的变化。
2. **创建副本**：当你完成修改后，`Immer.js` 会根据记录的变更，生成一个新的不可变的 `state` 副本，而原始 `state` 保持不变。
3. **优化性能**：如果 `state` 中某些部分没有被修改，`Immer.js` 会直接引用未修改的部分，避免不必要的深拷贝，提升性能。
   - Persistent Data Structure（持久化数据结构或一致性 数据结构）；
   - 当数据被修改时，会返回一个对象，但是新的对象会尽可能的利用之前的数据结构而不会 对内存造成浪费；

