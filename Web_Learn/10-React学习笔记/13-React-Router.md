# Router常用

### 1. **常用组件**

#### 1.1 `<BrowserRouter>`

用于启用基于 HTML5 `history` API 的路由管理，适合没有 `#` 符号的 URL（推荐用于现代浏览器）。

```jsx
import { BrowserRouter } from 'react-router-dom';

<BrowserRouter>
  <App />
</BrowserRouter>
```

#### 1.2 `<HashRouter>`

使用 URL 中的 `#` 符号（哈希符号）来表示路径，适合不支持 `history` API 的旧环境。

```jsx
import { HashRouter } from 'react-router-dom';

<HashRouter>
  {/* Your app here */}
</HashRouter>
```

#### 1.3 `<Routes>` 和 `<Route>`

- `<Routes>` 组件用于包装路由列表。

- `<Route>` 组件用于定义路径与组件的映射关系。

- ```jsx
  import { Routes, Route } from 'react-router-dom';
  import Home from './Home';
  import About from './About';
  
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
  ```

#### 1.4 `<Link>` 和 `<NavLink>`

- `<Link>`：用于创建导航链接，避免使用传统的 `<a>` 标签造成页面刷新。
- `<NavLink>`：继承自 `<Link>`，但可以基于当前路径为激活的链接添加样式（如 `active` 类）。

```jsx
import { Link, NavLink } from 'react-router-dom';

<Link to="/about">About</Link>
<NavLink to="/about" activeClassName="active">About</NavLink>
```

#### 1.5 `<Navigate>`

用于在应用内编程式地进行重定向。你可以通过 `<Navigate>` 来自动跳转到其他页面。

```jsx
import { Navigate } from 'react-router-dom';

<Navigate to="/login" />
```

### 2. **常用 Hook**

#### 2.1 useNavigate()

用于在代码中编程式地进行导航，类似于 `history.push` 或 `history.replace`。

```jsx
import { useNavigate } from 'react-router-dom';

function MyComponent() {
  const navigate = useNavigate();

  const goToAbout = () => {
    navigate('/about');
  };

  return <button onClick={goToAbout}>Go to About</button>;
}
```

#### 2.2 useLocation()

用于获取当前的路径和 URL 状态。

```jsx
import { useLocation } from 'react-router-dom';

function MyComponent() {
  const location = useLocation();

  console.log(location.pathname); // 当前的 URL 路径
  return <div>Current path: {location.pathname}</div>;
}
```

#### 2.3 useParams()

用于获取动态路由中的参数（如 `:id`）。

```jsx
import { useParams } from 'react-router-dom';

function Profile() {
  const { id } = useParams(); // 获取动态参数 id

  return <div>Profile ID: {id}</div>;
}
```

#### 2.4 `useMatch()`

用于匹配特定路径的信息。

```jsx
import { useMatch } from 'react-router-dom';

function MyComponent() {
  const match = useMatch('/about');

  return match ? <div>You're on the About page</div> : <div>Not on About page</div>;
}
```

### 3. **常用属性**

#### 3.1 element

`<Route>` 的 `element` 属性用于指定在匹配路径时渲染的组件。

```jsx
<Route path="/" element={<Home />} />
```

#### 3.2 path

`<Route>` 的 `path` 属性用于指定与当前路由对应的路径。

```jsx
<Route path="/about" element={<About />} />
```

#### 3.3 replace

`<Navigate>` 和 `useNavigate` 中的 `replace` 属性用于决定导航时是否替换浏览器历史记录。

```jsx
<Navigate to="/home" replace />
```

或者

```jsx
navigate('/home', { replace: true });
```

#### 3.4 state

用于传递一些状态信息（类似于 query 参数，但不显示在 URL 中）。

```jsx
import { useNavigate } from 'react-router-dom';

function MyComponent() {
  const navigate = useNavigate();

  const goToAbout = () => {
    navigate('/about', { state: { fromHome: true } });
  };

  return <button onClick={goToAbout}>Go to About</button>;
}
```

在目标组件中可以使用 `useLocation` 来读取状态：

```jsx
import { useLocation } from 'react-router-dom';

function About() {
  const location = useLocation();
  console.log(location.state?.fromHome); // true
}
```

### 其他方法

React Router 6+ 提供了更灵活的路由配置方式，通过 `createBrowserRouter` 或 `createHashRouter` 来创建更动态的路由。

```jsx
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
  },
  {
    path: "/about",
    element: <About />,
  },
]);

function App() {
  return <RouterProvider router={router} />;
}
```

#### 4.2 `Outlet`4.2 `出口`

`<Outlet>` 用于嵌套路由，可以在父路由中渲染子路由。

```jsx
<Route path="dashboard" element={<Dashboard />}>
  <Route path="stats" element={<Stats />} />
  <Route path="profile" element={<Profile />} />
</Route>

// 在 Dashboard 组件中使用 <Outlet>
function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>
      <Outlet /> {/* 渲染子路由的组件 */}
    </div>
  );
}
```

### 总结

- **常用组件**：`<BrowserRouter>`, `<HashRouter>`, `<Routes>`, `<Route>`, `<Link>`, `<NavLink>`, `<Navigate>`, `<Outlet>`.
- **常用 Hook**：`useNavigate()`, `useLocation()`, `useParams()`, `useMatch()`.
- **常用属性**：`path`, `element`, `replace`, `state`.
- **其他方法**：`createBrowserRouter`, `createHashRouter`, `useSearchParams`.