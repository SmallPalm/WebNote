# 闭包的定义

- 不是JavaScript特有的
- 从两个方面看闭包的定义
- 在计算机科学中和JavaScript中

### 在计算机科学中对闭包的定义

- 闭包 : Closure 
  - 又称词法闭包
  - 函数闭包
- 是在支持头等函数的编程语言中 , 实现词法绑定的一种技术
- 闭包在实现上是一个**结构**
  - 它存储了**一个函数**和**一个关联的环境**
  - 相当于一个符号查找表
- 闭包跟函数最大的区别在于
  - 当捕捉闭包的时候 , 他的**自由变量**会再捕捉时被确定
  - 这样即使脱离了捕捉时的上下文 , 它也能照常运行

##### **闭包的概念出现于60年代**

- 最早实现闭包的程序是Scheme
  - JavaScript中大量的设计是来源于Scheme的

### JavaScript闭包的解释

- 一个函数和对其周围状态 **(lexical environment , 词法环境)** 的引用捆绑在一起
  - 或者说函数被引用包围
  - 这样的组合就是闭包(Closure)
- 就是说 , 闭包让你可以在一个内层函数中访问到其外层函数的作用域
- 在JavaScript中, 每当创建一个函数 , 闭包就会在函数创建的同时被创建出来



## 闭包理解

- 一个普通的函数function , 如果它可以访问外层作用域的自由变量 , 那么这个函数就是一个闭包
- **广义** : JavaScript中的函数都是闭包
- **狭义** : JavaScript中函数 ,如果访问了外层作用域的变量 , 那么它是一个闭包



# 内存泄露

- 对于那些我们永远不会在使用的对象

  - 但是对于GC来说
    - GC是不知道要进行释放对应的内存的
    - 内存会依然保留

  解决方面

  ​	变量  =  null



# 闭包的实际应用

- 闭包常用于创建模块

  - 这种模式可以封装私有变量和方法，只暴露公共接口。

  - ```js
    const counterModule = (function() {
        let count = 0;
    
        function increment() {
            count++;
            console.log(count);
        }
    
        function reset() {
            count = 0;
            console.log(count);
        }
    
        return {
            increment,
            reset
        };
    })();
    
    counterModule.increment(); // 1
    counterModule.increment(); // 2
    counterModule.reset();     // 0
    ```

- 使用闭包可以创建带有私有状态的对象

  - ```js
    function createCounter() {
        let count = 0;
        return {
            increment() {
                count++;
                console.log(count);
            },
            reset() {
                count = 0;
                console.log(count);
            }
        };
    }
    
    const counter1 = createCounter();
    counter1.increment(); // 1
    counter1.increment(); // 2
    counter1.reset();     // 0
    
    const counter2 = createCounter();
    counter2.increment(); // 1
    ```

- 柯里化是一种将函数拆分成多个单一参数函数的技术，闭包在其中起着重要作用。

  - ```js
    function add(a) {
        return function(b) {
            return a + b;
        };
    }
    
    const add5 = add(5);
    console.log(add5(3)); // 8
    console.log(add5(7)); // 12
    ```

  - 