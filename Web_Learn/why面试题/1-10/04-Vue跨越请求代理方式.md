1.配置Vue.config.js

- 在Vue项目中，可以通过修改 `vue.config.js` 文件来设置代理。例如，你可以添加如下配置

  ```js
  module.exports = {
    devServer: {
      proxy:{
        '/api': {
          // 设置代理的目标URL
          target: 'http//api.example.com',
          // 允许宽裕
          changeOrigin: true,
          pathRewrite: {
            // 将请求中的/api路径替换为空
            '^/api': ''
          }
        }
      }
    }
  }
  ```

  

2.使用http-proxy-middleware

- 然后在Vue-config-js中配置代理

  ```js
  const { createProxyMiddleware } = require('http-proxy-Middleware')
  
  module.exports = {
    devServer: {
      setup: function(app) {
        app.use(
        	'/api',
          createProxyMiddleware({
            target: 'http://api.example.com',
            changeOrigin: true,
            pathRewrite: { '^/api': '' }
          })
        )
      }
    }
  }
  ```

  





# 详情

在Vue项目中，跨域请求是一个常见的问题，因为浏览器的同源策略限制了从不同源（域名、协议、端口）的脚本对资源的访问。为了解决这个问题，可以使用代理（Proxy）的方式来进行接口请求。以下是一些常用的代理配置方法：

1. **配置 `vue.config.js`**： 在Vue项目中，可以通过修改 `vue.config.js` 文件来设置代理。例如，你可以添加如下配置：

   javascript

   ```javascript
   module.exports = {
     devServer: {
       proxy: {
         '/api': {
           target: 'http://api.example.com',  // 设置代理的目标URL
           changeOrigin: true,  // 允许跨域
           pathRewrite: {
             '^/api': ''  // 将请求中的/api路径替换为空
           }
         }
       }
     }
   }
   ```

   这样，当你在Vue组件中使用 `axios.get('/api/users')` 时，请求会被代理到 `http://api.example.com/users`。

2. **使用 `http-proxy-middleware`**： 如果你的项目中还没有 `http-proxy-middleware`，你可以通过npm安装它：

   bash

   ```bash
   npm install --save-dev http-proxy-middleware
   ```

   然后在 `vue.config.js` 中配置代理：

   javascript

   ```javascript
   const { createProxyMiddleware } = require('http-proxy-middleware');
   
   module.exports = {
     devServer: {
       setup: function (app) {
         app.use(
           '/api',
           createProxyMiddleware({
             target: 'http://api.example.com',
             changeOrigin: true,
             pathRewrite: { '^/api': '' },
           })
         );
       }
     }
   }
   ```

3. **Nginx 反向代理**： 在生产环境中，你也可以使用Nginx作为反向代理服务器来解决跨域问题。配置示例如下：

   nginx

   ```nginx
   server {
     listen 80;
     server_name yourdomain.com;
     location /api {
       proxy_pass http://api.example.com;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       proxy_set_header X-Forwarded-Proto $scheme;
     }
   }
   ```

4. **修改 Axios 请求**： 在使用代理后，你可能需要修改Axios的请求配置，以确保请求通过代理发送。例如：

   javascript

   ```javascript
   import axios from 'axios';
   const BASE_URL = "/api";
   axios.defaults.baseURL = BASE_URL;
   ```

这些方法可以帮助你在开发和生产环境中解决Vue项目的跨域请求问题。记得在配置代理后，需要重新启动Vue开发服务器以使配置生效。