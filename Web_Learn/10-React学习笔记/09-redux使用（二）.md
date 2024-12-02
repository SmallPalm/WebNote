## Redux 中如何进行异步操作，与同步操作有什么区别

#### 同步操作：

在 Redux 中，**同步操作**是指直接通过 `dispatch` 发起一个 action 来更新 `state`。当你调用 `dispatch` 时，`action` 被立即发送到 `reducer`，然后 `reducer` 计算并返回新的 `state`。

```js
// 同步 action
const incrementAction = { type: 'INCREMENT', action: "xxx"};
store.dispatch(incrementAction);
```

****

#### 异步操作：

**异步操作**（如 API 请求）在 Redux 中不能直接通过 `dispatch` 来处理，因为 `dispatch` 需要一个简单的对象作为 `action`，而异步代码是通过回调或 `Promise` 完成的。为了解决这个问题，通常使用 **中间件（middleware）**，例如 `redux-thunk` 或 `redux-saga`。

**`redux-thunk`** 是 Redux 中处理异步操作最常见的中间件，它允许 `dispatch` 一个函数，该函数可以进行异步操作并在异步操作完成后再次 `dispatch`。

```js
// 异步 action
const fetchData = () => {
  return (dispatch) => {
    // 异步操作，假设从 API 获取数据
    fetch('http://123.207.32.32:8000/home/multidata')
      .then(response => response.json())
      .then(data => {
        // 当数据获取成功后 dispatch 一个同步 action 来更新 state
        dispatch({ type: 'FETCH_DATA_SUCCESS', payload: data });
      });
  };
};
store.dispatch(fetchData());
```

### 区别：

- **同步操作**立即执行 `dispatch`，触发 `reducer` 更新 `state`。
- **异步操作**需要通过中间件（如 `redux-thunk`），让 `dispatch` 可以执行函数进行处理异步逻辑，并在异步完成通过传入dispatch再触发 `dispatch`。





## Redux 中如何进行 `reducer` 的拆分，拆分的原理和本质是什么

随着应用变得复杂，一个单一的 `reducer` 可能会变得非常臃肿。因此 Redux 提供了 `reducer` 的拆分机制，将不同的 `reducer` 按照功能模块化。

#### `combineReducers`：

Redux 提供了 `combineReducers` 函数，用于将多个小的 `reducer` 合并成一个主 `reducer`。每个子 `reducer` 管理 `state` 的一部分，而 `combineReducers` 会将所有子 `reducer` 的结果合并为一个总的 `state`。

```js
import { combineReducers } from 'redux';

// 定义多个小的 reducer
const userReducer = (state = {}, action) => {
  switch (action.type) {
    case 'SET_USER':
      return { ...state, user: action.payload };
    default:
      return state;
  }
};

const productReducer = (state = [], action) => {
  switch (action.type) {
    case 'ADD_PRODUCT':
      return [...state, action.payload];
    default:
      return state;
  }
};

// 使用 combineReducers 将小的 reducer 组合成一个大的 reducer
const rootReducer = combineReducers({
  user: userReducer,
  products: productReducer,
});

export default rootReducer;
```

#### 原理和本质：

- 每个子 `reducer` 只处理 `state` 的一部分，当 `combineReducers` 被调用时，它会为每个子 `reducer` 分发 `action`，并将每个子 `reducer` 返回的 `state` 合并成一个大的 `state`。
- 这种方式可以让 `reducer` 更加模块化、易于维护和扩展。

## 什么是 Redux Toolkit，核心 API 有哪些，说出它们的作用

Redux Toolkit：用于简化 Redux 的使用，它提供了一套简单易用的 API 来减少 Redux 的样板代码，并集成了常见的中间件和开发工具（如 `redux-thunk` 和开发者工具扩展）。

#### 核心 API：

1. **`configureStore`**：

   - 作用：简化创建 `store` 的过程，并且默认包含了 `redux-thunk` 中间件，支持时间旅行调试。

   - 示例：

     ```js
     import { configureStore } from '@reduxjs/toolkit';
     const store = configureStore({
       reducer: rootReducer, // 合并的 reducer
     });
     ```

2. **`createSlice`**：

   - 作用：简化 `reducer` 和 `action` 的创建。`createSlice` 可以在reducers中同时生成 `action creators` 和 `reducer`。

   - 示例：

     ```js
     import { createSlice } from '@reduxjs/toolkit';
     const userSlice = createSlice({
       name: 'user',
       initialState: { name: '', age: 0 },
       reducers: {
         setUser: (state, action) => {
           state.name = action.payload.name;
           state.age = action.payload.age;
         },
       },
     });
     export const { setUser } = userSlice.actions;
     export default userSlice.reducer;
     ```

3. **`createAsyncThunk`**：

   - 作用：简化处理异步逻辑的方式，自动生成 `pending`、`fulfilled` 和 `rejected` 三种状态的 `action`。

   - 示例：

     ```js
     import { createAsyncThunk } from '@reduxjs/toolkit';
     const fetchUserData = createAsyncThunk(
       'user/fetchUserData',
       async (userId) => {
         const response = await fetch(`/api/user/${userId}`);
         return response.json();
       }
     );
     ```

4. **`createReducer`**：

   - 作用：简化 `reducer` 的创建，允许直接修改 `state`（通过 immer 库），不需要手动返回新的 `state`。

   - 示例：

     ```js
     import { createReducer } from '@reduxjs/toolkit';
     const userReducer = createReducer({ name: '', age: 0 }, {
       setUser: (state, action) => {
         state.name = action.payload.name;
         state.age = action.payload.age;
       },
     });
     ```

5. **`createEntityAdapter`**：

   - 作用：用于处理标准化的 CRUD 操作和实体集合的管理。

   - 示例：

     ```js
     import { createEntityAdapter } from '@reduxjs/toolkit';
     const usersAdapter = createEntityAdapter();
     ```

# 总结 Redux 的使用步骤

#### 原始 Redux 用法

1. **创建 `store`**：使用 `createStore` 创建 `store`。

   ```js
   import { createStore } from 'redux';
   const store = createStore(reducer);
   ```

2. **定义 `reducer`**：编写 `reducer` 处理 `action`。

   ```js
   const reducer = (state = {}, action) => {
     switch (action.type) {
       case 'SET_USER':
         return { ...state, user: action.payload };
       default:
         return state;
     }
   };
   ```

3. **发起 `action`**：使用 `dispatch` 发起 `action`。

   ```js
   store.dispatch({ type: 'SET_USER', payload: { name: 'John' } });
   ```

4. **订阅 `store` 变化**：通过 `store.subscribe` 监听 `state` 的变化。

   ```js
   store.subscribe(() => {
     console.log(store.getState());
   });
   ```

#### Redux Toolkit (RTK) 用法：

1. **创建 `slice` 和 `reducer`**：使用 `createSlice` 创建 `reducer` 和 `action`。

   ```js
   const userSlice = createSlice({
     name: 'user',
     initialState: { name: '', age: 0 },
     reducers: {
       setUser: (state, action) => {
         state.name = action.payload.name;
         state.age = action.payload.age;
       },
     },
   });
   ```

2. **配置 `store`**：使用 `configureStore` 创建 `store`。

   ```js
   const store = configureStore({
     reducer: userSlice.reducer,
   });
   ```

3. **发起 `action`**：使用 `dispatch` 发起 `action`。

   ```js
   store.dispatch(userSlice.actions.setUser({ name: 'John', age: 30 }));
   ```

4. **异步操作**：使用 `createAsyncThunk` 创建异步操作。

   ```js
   const fetchUserData = createAsyncThunk('user/fetchUserData', async (userId) => {
     const response = await fetch(`/api/user/${userId}`);
     return response.json();
   });
   ```