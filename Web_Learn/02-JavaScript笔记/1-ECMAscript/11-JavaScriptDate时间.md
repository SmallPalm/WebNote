- CMT表示是某个某个时区中的时间
- UTC表示是标准时间



# Date对象

- Date表示时间和处理时间
- 日期的表示方式有两种：RFC 2822标准 ：ISO  8601标准
- 默认打印RFC 2822标准



# Date方法

- **getFullYear() : 获取年**
- **getMonth() : 获取月**
- **getDate() : 获取日 从0到11**
- **gethours() :   获取小时**
- **getminute()  :  获取分**
- **getsecond()  :  获取秒**
  - setFullYear() : 修改年
  - setMonth() : 修改月
  - setDate() : 修改日 从0到11
  - sethours() :   修改小时
  - setminute()  :  修改分
  - setsecond()  :  修改秒

# Date获取Uinx时间戳

- Uinx时间戳
  - 它是一个整数值，表示自1970年1月1日00：00：00
  - UTC以来的毫秒数
- 获取时间戳
  - new Date().getTime()
  - new Date().valueOf()
    - 创建Date ,  然后将一个Date对象转成时间戳
  - +new Date()
    - 直接转成时间戳
  - Date.now()
    - 获取当前时间的时间戳
- 将字符串转成时间戳
  - Date.parse()
    - 从一个字符串中读取日期,并输出对应Uinx时间戳
    - 如果输入的不能解析,输出NaN
- 时间戳有十位和十三位
  - 十位代表从秒开始
  - 十三位代表从毫秒开始
    - 十位单位*1000 = date时间
    - JavaScript将时间戳转换成正常时间
    - 时间戳为10位需*1000
    - 时间戳为13位的话不需乘1000