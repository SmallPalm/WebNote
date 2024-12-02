# while循环语句

```js
var 变量 = ""
while(){
变量++
}
```



# do..while循环语句

- do..while循环和while循环非常像，二者经常可以相互替代（不常用）

  - 但是do..while的特点是不管条件成不成立，do循环代码块都会先执行一次

- ```js
  var count = 0
  do{
  console.log("holle world")
    count++
  }while(count < 10)
  ```



# for循环

- for循环更加复杂，但是他是最常用的循环形式

- ```js
  for(begin ; condition ; step){
  //循环代码块
  }
  ```

- begin :  let i = 0 : 进入循环时执行一次

- condition ：i < 3 ：在每次循环迭代之前检查，如果为false，停止循环

- body（循环体）：条件为真时， 重复运行 ：**循环代码块**

- step：i++：在每次循环体迭代后执行

- begin执行一次，然后进行迭代，每次检查condition后，执行body和step

# for循环的嵌套

- 在开发中 ，某些情况下一次循环是无法达到目的的，我们就是需要使用循环嵌套

# 循环控制

- 跳出循环
- 本次循环不执行，执行下次循环



break：依旧适用于for

- 跳出循环



continue：跳过本次循环，执行下次循环

- continue指令是break的轻量版
- continue莫一条件满足时，不执行后续重复的代码



