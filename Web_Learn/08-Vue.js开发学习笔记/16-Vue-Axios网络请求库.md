# 为什么不使用原生的网络请求

- 需要自己来使用原生封装一些功能
  - 原生某些功能是不具备
    - 需要自己封装后才能使用
    - 如
      - 请求拦截
      - 响应拦截
- JS代码是在浏览器中运行
  - 也可以在Node中运行
  - 使用fetch在浏览器可以正常请求
    - 但在Node中运行就不能正常运行
      - 需要修改API
        - 使用Http模块



# 认识Axios

优势

- 在浏览器中发生XMLHttpRequests请求
- **在Node.js中发送Http请求**
- 支持promise API
- 拦截请求和拦截响应
- 转换请求 和 响应数据



# Axios请求方式

- axios请求
  - axios(config)
    - config : 对象

- request请求
  - axios.request(config)
- get请求
  - axios.get(url, { config })
- delete请求
  - axios.delete(url , { config })
- head请求
  - axios.head(url , { config })
- post请求
  - axios.post(url, {data , config })
    - data  : 对象
- put请求
  - axios.put(url , {data , config})
- patch请求
  - axios.patch(url ,{data,  config })

同时发生两个请求, 多个请求

- 使用axios.all
  - 可以放入多个请求的数组 
- axios.all([]) 返回 的结果是一个 数组
  - 使用axios. spread 可将数组  [res1, res2] 展开为 res1, res2



# 常见的config配置选项

- 请求地址
  - url :  “/user”
- 请求类型
  - method : “ get ”
- 请求根路径
  - baseURL : “http://www.xxx.com/api”
- 请求前的数据处理
  - transformRequest : [ function(data){} ],
- 请求后的数据处理
  - transformResponse : [ function(data){} ],
- 自定义的请求头
  -  headers : { 'x-Requested-With' : 'XMLHttpRequest' },
- URL查询对象
  - params:{ id: 12 },
- 查询对象序列化函数
  - paramsSerializer : function(params){ }
-  request body
  - data : { key: 'aa'}
- 超时设置
  - timeout: 1000,



# Axios的创建实例

- 为什么要创建axios的实例
  - 当我们从axios模块中导入对象时
    - 使用的实例就是**默认的实例**
  - 当给该实例设置一些默认配置时, 
    - 这个配置就被固定下来了
  - 但是后续开发中
    - 某些配置可能会不太一样
  - 比如某些请求需要使用特定的baseURL或者timeOut等
  - 这个使用 , 我们就需要创建新的实例
    - 并且传入属于该实例的配置信息
- ![image-20240121114836359](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240121114836359.png)



# 请求和响应拦截器

- axios库可以设置拦截器, 
  - 拦截每次网络请求和网络发生响应

- 网络请求拦截
  - axios.interceptors.request.use(**请求**成功拦截的回调函数, **请求**失败拦截的回调函数)
- 网络发生响应拦截
  - axios.interceptort.response.use(响应成功拦截的回调函数,  响应失败拦截的回调函数)

![image-20240121154409556](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240121154409556.png)



# 可以将axios进行进一步封装使用

## 简易封装axios

**![image-20240121154659879](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240121154659879.png)**