# Moment.js库 VS Day.js库

**Moment库官网的描述**

- Moment 是一个 JavaScript 库
  - 可以帮助我们快速处理时间和日期
  - 已在数百万的项目中使用
  - Moment对浏览器的兼容性比较好
    - 例如，在Internet Explorer 8+版本运行良好
- 现在比较多人反对使用 Moment是因为它的包大小
  - Moment 不适用于“tree-shaking”算法
  - 因此往往会增加 Web 应用程序包的大小
    - 如果需要国际化或时区支持，Moment 可以变得相当大

- Moment团队也希望我们在未来的新项目中不要使用Moment 
  - 而推荐使用其它的替代品。例如：**Day.js。**

**Day.js库官网的描述**

- Day.js 是 Moment的缩小版

  - Day.js 拥有与 Moment相同的 API

  - 并将其文件大小减少了 97%

- Moment完整压缩文件的大小为 67+Kb
  - Day.js 压缩文件只有 2Kb
- Day.js所有的 API 操作都将返回一个新的 Day.js 对象
  - 这种设计能避免 bug 产生，减少调试时间
- Day.js 对国际化支持良好
  - 国际化需手动加载
    - 多国语言默认是不会被打包到Day.js中的。

# Day.js获取、设置时间

- 获取(Get) + 设置(Set)
- .year()
  - 获取年
- .month()
  - 获取月
- .date() 
  - 获取日
- .hour()
  - 获取时
- .minute()
  - 获取分
- .second()
  - 获取秒
- .day() 
  - 获取星期几
- .format() 
  - 格式化日期

# Dayjs操作时间

操作日期和时间

- .**add**(numbers , unit)
  - 添加时间
- .**subtract**(numbers , unit)
  - 减去时间

- .**startOf**(unit)
  - 时间的开始
    - 例如获取今年的第一天零时零分零秒

## Day.js解析、国际化、插件

- 解析时间
  - dayjs(毫秒|秒) 
    - 时间戳（毫秒 和 秒）
  - dayjs('2022-06-15')
    - ISO 8601格式的字符串
  - dayjs(new Date()) 
    - 接收日期对象
- Day.js的插件应用
  - .fromNow()
    - 从现在开始的时间
      - 需要依赖：relativeTime 插件
  - relativeTime插件
    - https://cdn.jsdelivr.net/npm/dayjs@1.11.3/plugin/relativeTime.js

