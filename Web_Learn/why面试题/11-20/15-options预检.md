### 什么是 OPTIONS 预检请求（Preflight Request）

在跨域资源共享（CORS, Cross-Origin Resource Sharing）中，当浏览器发起某些类型的跨域请求时，浏览器会先发送一个 **OPTIONS 预检请求（Preflight Request）**。预检请求是为了检测目标服务器是否允许实际请求执行的一种安全机制。

### 预检请求的触发条件

浏览器会在以下情况触发 OPTIONS 预检请求：

1. **使用非简单请求的 HTTP 方法**：请求使用了 `GET`、`POST`、`HEAD` 以外的方法，例如 `PUT`、`DELETE`、`PATCH` 等。
2. **自定义请求头**：请求中包含非标准的请求头（即非简单请求头），如 `Authorization`、`X-Custom-Header` 等。
3. **非简单的 `Content-Type`**：
   - 简单的 `Content-Type` 包括 `text/plain`、`application/x-www-form-urlencoded` 和 `multipart/form-data`。
   - 其他 `Content-Type`（如 `application/json`）会触发预检。

### 预检请求的工作细节

1. **发送 OPTIONS 请求**：

   - 浏览器向目标服务器发送一个 OPTIONS 请求，询问服务器是否允许当前的跨域请求。
   - OPTIONS 请求包含请求方法、请求头等信息，而不会携带实际的数据。

2. **服务器响应**：

   - 服务器收到 OPTIONS 请求后，会返回响应，说明允许的 HTTP 方法、允许的请求头和允许的源（Origin）。

   - 主要响应头包括：
     - **`Access-Control-Allow-Origin`**：允许的请求源（Origin）。
       - **`Access-Control-Allow-Methods`**：允许的请求方法（如 `GET`, `POST`, `PUT`）。
       - **`Access-Control-Allow-Headers`**：允许的自定义请求头。
       - **`Access-Control-Max-Age`**：预检请求的缓存时间，在此期间无需再次发送预检请求。

3. **决定是否执行实际请求**：

   - 如果服务器允许该跨域请求，浏览器会继续发送实际请求。

   - 如果服务器拒绝（没有正确返回 CORS 响应头），浏览器将拦截实际请求，阻止其执行。

### 预检请求的优化建议

1. **减少预检请求频率**：通过设置 `Access-Control-Max-Age` 响应头，浏览器会缓存预检请求的结果，减少频繁的预检请求。
2. **控制跨域请求**：尽量使用简单请求方式，避免使用复杂请求方法和头，减少预检请求的触发。
3. **服务器优化**：确保服务器快速响应预检请求，减少响应时间，以提高整体性能。

OPTIONS 预检请求是浏览器的一种保护机制，确保跨域请求符合服务器安全策略。理解并正确处理预检请求，可以有效减少跨域通信中的安全问题和性能开销。