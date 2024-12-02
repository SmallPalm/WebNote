#  程序的执行顺序

在开发中有三种不同的执行的方式

- 顺序
  - 从上向下
- 分支
  - 根据条件判断
- 循环
  - 让特定代码重复执行	



## 代码块

- 代码块

  - 在开发中，一行代码很难完成某个特定的功能 ，我们就会将一些代码放到一个代码块里

- ```js
  {
  var  num1 = 2
  var  mie = 4
  var  koo = "wgrjbo"
  }
  ```

- 对象

- ```js
   var info {
   name:"grdgnd"
   age: 124
   }
  ```

## JavaScript常见分支

- if分支
- wihch分支



# if分支

# 单分支结构  if

- ```js
  if(条件判断){
  
  }
  ```

- if（）语句会计算圆括号内的表达式，并将计算结果转换为Boolean（布尔型）

  - 数字0 ， 空字符串“” ， null ，undefined ，NaN都会被转换为false
  - 它们都称为假值（falsy）
  - 其他值被转换为true 所以它们被称为真值



# 多分支结构 if .. else..

- ```js
  if(){
  
  }else{
  
  }
  ```



# if..else if .. else..

- ```js
  if(){
  
  }else if(){
  
  }
  ```

- 可以判断多个条件





# 三元运算符

- 这个运算符通过问号 ？ 表示

- ```js
  var 变量 = 条件  ？  value1 ： value2;
  ```

- 计算条件结果，结果为真 返回value1 否则返回value2 





# 逻辑运算符

- || （或） ：一个为真  ：  false or frue ：也称短路或
  - 可以使用运算元
  - 从左到右
  - 先将运算元转成Boolean类型
  - 对转成的Boolean类型进行判断
    - 如果为true，直接将结果返回（返回元类型，不会在返回Boolean类型）
    - 如果为false，进行第二个运算元的判断
  - 如果找到最后，也没有找到，那么返回最后一个运算元
  - 
- && （与） ： 同时为真 ： false &&  true
  - 先转成Boolean类型在进行判断
  - 对运算元的boolean类型进行判断
    - 如果是false,返回(原始值)
    - 如果是true,就继续判断下一个运算元
  - 如果查找了所以的都是 true , 那么返回最后一个运算元(原始值)
- ！ （非） ： 取反  ： ！false
  - `它可以将多个表达式或者值放到一起来获取到一个最终的结果



# switch语句

- switch是分支结构的一个语句
  - 它是通过判断表达式的结果（或者变量）是否等于case语句的常量，来执行相对应的分支体的
  - 与if语句不同的是 ， switch语句只能做值的相等判断 （使用全等====运算符），而if语句可以做值范围判断
  
- switch语法

  - switch语句有至少一个case代码块和一个可选的default代码块
  - 默认情况下case是有穿透的
  - 添加break  ，当遇见break的时候，执行语句就会跳出switch ， 后面代码就不会执行

- ```
  switch(变量){
  case 常量1:
  执行语句
  break  //切断符
  
  case 常量2:
  执行语句
  break
  
  default:
  }
  ```

  
