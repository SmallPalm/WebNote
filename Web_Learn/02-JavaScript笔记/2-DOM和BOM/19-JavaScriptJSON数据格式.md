# JSON的由来

- 在目前的开发中 , JSON是一种非常重要的数据格式 , **它并不是编程语言**
- **一种可以在客户端和服务器之间传输的数据格式**
- JSON的全称是 JavaScript Object Notation
  - JSON是Douglas Crockford构想和设计的一种**轻量级资料交换格式**
  - 算是JavaScript的一个子集
- 虽然JavaScript被提出来的时候是主要应用JavaScript中
  - 但**目前已经独立于编程语言**
  - 可以在各个编程语言中使用
- 很多编程语言都实现了将JSON转成对应模型的方式
  - 但是在JavaScript中不需要转换,
    - 因为他是JavaScript的一个子集



## 其他的数据格式

- **XML** : 最早期的数据格式 , 比较占用带宽 
- 在早期的网络传输中主要是使用XML来进行数据交换 , 但是这个格式解析 , 传输各方都弱于JSON , 所以目前已经很少在被使用了
  - 但是后端一些框架还用XML做配置文件



- **Protobuf** : google推出来的
- 在网络传输中目前已经越来越多使用的传输格式是protobuf
  - 但是直到2021年的3x的版本才支持JavaScript
  - 所有目前在前端使用的较少
    - 在很多其他的语言框架里面用的比较多
    - 做即时通讯(聊天,直播),需要频繁请求服务器 , 使用protobuf会更轻量



# JSON的使用场景

- 网络数据的传输JSON数据
- 项目的某些配置文件
- 非关系型数据库(NoSQL) 将json作为存储格式





# JSON的基本语法

- JSON有严格的语法
  - 普通的JSON文件不能写注释
-  JSON的顶层支持的三种类型的值(顶层 : 第一行开始)
  - 简单值
    - 数字(Number)
    - 字符串(String 不支持单引号)
    - 布尔类型(Boolean)
    - null类型
  - 对象值
    - 由key , value组成
    - key是字符串类型 : 并且必须添加双引号
    - value是值 可以是简单值, 对象值 , 数组值  ,函数
  - 数组值
    - 值可以是简单值, 对象值 , 数组值



# JSON序列化

- 某些情况下我们希望将JavaScript中的复杂类型转化为**JSON格式的字符串**
  - 这样方便对其进行处理
- 比如我们希望将一个对象保存在localStorage中
  - 我们存放的对象会被转化成[object Object]格式的字符串
  - 这并不是我们想要的结果
- **方法**
- 在ES5中引用了JSON全局对象
  - **stringify()** : 将JavaScript类型转成对应的JSON字符串
  - **parse()** : 解析JSON字符串 , 转换对应的JavaScript类型



# srtingify的参数

- JSON.stringify()方式将一个JavaScript对象或值转换为JSON字符串
- replacer方法 :可以使用function函数
  - 如果指定了一个replacer函数 , 则可以选择性地替代值
  - 如果指定的replacer是数组 ,则可选择性地仅包含数组指定的属性
- space方法
  - 设置几个空格
  - 可以有更清晰的阅读性
- toJSON方法
- parse()方法 : 可以使用function函数
  - 提供可选的review函数用以在返回之前对所得到的对象执行变换(操作)
- JSON的方法可以帮我们使用对象的深拷贝