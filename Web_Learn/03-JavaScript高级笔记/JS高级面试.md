# **JS**高级面试

什么是函数式编程

- 支持函数作为头等公民传来传来

## **什么是面向对象**

- 面向对象是一种编程方式 
  - 就是一种编程思想
  - 而JS支持面向对象编程方式和函数是编程方式
  - 它可以将一些数据代码抽取成一个个对象
    - 其实就是让我们在很多操作的时候
      - 第一时间不是立马看怎么做这个操作
        - 而是想着怎么去创建一个类
        - 在根据创建的类去来完成相对应的操作
- 这个类也就是面向对象的特性
  - 封装, 继承 , 多态
    - 而在JavaScript 中到处都是多态
      - 多态就是在不同的对象在执行时表现出不同的形态
        - 继承也是多态的前提

## **什么是对象**

- 对象类型就是一种键值对存储的数据类型
  - key是字符串对应每一个value
  - value可以是任意类型
    - 包含基础数据类型, 函数类型, 对象类型
- 而且其他数据类型通常是原始类型
  - 因为他们的值就包含一个单独的内容
- 而Objcet对象可以表示一组数据, 是其他数据的集合

##  **什么是类**

- 在JS中是ES6出现的Class类
  - 因为是函数中写出了大写开头的构造函数
    - 这种构造函数称之为类
- 而class类有自己的实例方法 , 静态方法
- 其实在JS中就是Class关键字定义的称之为类

## **什么是多态**

- 通俗来说就是不同的对象 , 在同一个事件中执行时 ,有不同的状态表现

  - 就是**多种形态**，具体点就是去完成某个行为，当不同的对象去完成时会产生出不同的状态

- 继承就是在多态的前提下

  - 多态是在不同继承关系的类对象,  去调用同一个函数 , 产生的不同的行为

- 多态是函数方法, 类方法的多态, 不是属性的多态

  - 多态跟属性无关

- 多态存在要有

  - 继承 , 方法重写 , 父类引用指向子类对象

- 当父类引用指向子类对象时

  - 用该父类引用调用子类重写方法时 , 这时多态就体现出来了

- ```js
  function sum(m,n){    
    return m + n 
  } 
  sum(20,30) 
  sum("abc","cba") //函数对不同的数据类型执行同一个操作时，表现出来的行为不一样
  ```

- ```js
  function calcArea(foo){
      console.log(foo.getArea);
  }
  
  let obj1 = {
      name:'why',
      getArea(){
          return 1000
      }
  }
  
  class Person{
      getArea(){
          return 100
      }
  }
  
  var p = new Person()
  //不同的对象-类在函数中执行相同的操作, 返回的结果是不同的
  calcArea(obj1)
  calcArea(p)
  ```

## **this指向 (this的绑定方式)**

this指向 主要看调用方法

### **默认绑定**

- 就是独立函数调用, this指向的window, 严格模式下指向undefined

### **隐式绑定**

- 就是通过一个对象来进行函数调用 , this指向的是本身对象

- 隐式绑定的前提
  - 在调用的对象内部有一个对函数的引用
    - 就是对象中有一个属性定义了一个函数
  - 也是通过这个引用 , 间接将this绑定到了这个对象上

### **显示绑定**

- 可以通过call 和 apply 的方法
  - 给函数绑定一个this指向
- 这种情况就是对象内部不包含这个函数的引用
  - 同时想在这个对象上强制调用,
    - 或者强行指向函数后, 使用对象中的一些数据

### **new绑定**

- 当new一个构造函数时 , new会创建一个对象, 并将this绑定到这个对象上

箭头函数没有this
- 就是箭头函数的作用域中没有this
  - 但是这个this会去外层作用域中去寻找

## **输入URL到页面渲染完成的整个过程**

1. 当我们在浏览器中输入一个URL网址时
2. 浏览器会根据我们输入的 那个URL然后交给DNS进行对URL的域名解析
3. 解析完成后 , 找到当前URL所在的服务器的ID地址
4. 向当前服务器发送网络请求
5. 服务器交给后台处理完成后返回数据
6. 浏览器就会接受服务器返回的数据文件
7. 这个数据文件包含HTML , JS , CSS , 图片等
8. 浏览器对加载到的资源 ,进行语法解析
9. 建立相对应的内部数据结构 (就如HTML中的DOM一样)
10. 开始解析加载文件, 渲染页面完成
    - 渲染
      - 浏览器在解析时, 先会解析一个index.html文件
      - 当在index文件中遇到link的css文件
        - 在解析css文件
      - 遇见script的文件
        - 在解析script文件
    - 不同的是
      - 不同的浏览器内核有不同的解析、渲染规则
      - 所以同一网页不同内核的浏览器种的渲染效果也可能不同
    - 其次
    - 浏览器在解析html的过程中 , 遇到script元素是不能继续构建DOM树的
    - 停止继续构建 , 首先下载JavaScript代码 , 并执行JavaScript脚本
    - 等到JavaScript脚本执行完成 , 在继续解析html , 创建DOM树

## **作用域**

- 作用域表示一些标识符的作用的有效范围
  - 也可以是作用域就是限制一个变量的使用范围
    - 但是内层作用域可以访问外层作用域
- 函数可以定义自己的作用域
  -  在函数自身作用域中定义的变量, 只能在函数内部可以被访问到
- 通常来说就是变量在什么位置可以被访问

## **作用域链**

- 作用域链 就是可以内层作用域可以访问外层作用域
  - 内从外扩展搜寻变量

## **闭包**

### 闭包的定义

闭包是指在一个函数内部创建另一个函数，内部函数可以根据作用域链访问外部函数的变量，**即使外部函数已经执行完毕，这些变量仍然可以被访问。**

### 闭包的内存泄漏风险

闭包可以导致内存泄漏，特别是在引用的变量或函数没有及时释放时。为避免内存泄漏，可以在不再需要闭包时手动将引用变量设置为 `null`。

### 闭包的实际应用

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



## **执行上下文**

## 原型链

#### 原型链概念

每个 JavaScript 对象都有一个内部链接到另一个对象的链接，这个链接就是原型（prototype）。这个另一个对象也有自己的原型，形成一个链条，称为原型链。对象的 `__proto__` 属性（或在 ES6 中，`Object.getPrototypeOf` 方法）指向它的原型。



## 回调函数

#### 定义

回调函数是作为参数传递给另一个函数的函数，这个函数在某个时间点被调用。

```js
function fetchData(callback) {
  setTimeout(() => {
    const data = 'Hello, world!';
    callback(data);
  }, 1000);
}

function handleData(data) {
  console.log(data);
}

fetchData(handleData); // 1 秒后输出 'Hello, world!'
// 在这个示例中，fetchData 函数接受一个回调函数 callback 作为参数，并在异步操作（setTimeout）完成后调用它。
```

#### 特点

- 简单直接，适合处理简单的异步操作。
- 可能导致“回调地狱”问题，即嵌套的回调函数使代码难以阅读和维护。



## 高级函数

## 函数柯里化

1. ## 为什么要用它

## ES6 - ES13

1. ## 用过APl

## Promise

#### 定义

Promise 是一个表示异步操作最终完成或失败的对象，并返回操作的结果。

#### 状态

- **Pending**：初始状态，操作尚未完成。
- **Fulfilled**：操作成功完成，并返回一个值。
- **Rejected**：操作失败，并返回一个原因。

例

```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = 'Hello, world!';
      resolve(data);
    }, 1000);
  });
}

fetchData()
  .then(data => {
    console.log(data); // 1 秒后输出 'Hello, world!'
  })
  .catch(error => {
    console.error(error);
  });
// 在这个示例中，fetchData 函数返回一个 Promise，该 Promise 在异步操作完成后被 resolve。
```

特点

- 链式调用，避免了回调地狱。

- 提供了更好的错误处理机制



1. ## Promise 实现原理
2. ## 手写Promise

## 迭代器

## 生成器

## 异步函数

## **浏览器的事件循环**

## Proxy 和 Object.definedProperty 区别

## 防抖

## 节流

## 深拷贝

## async / await 

#### `async/await` 是基于 Promise 的语法糖，使得异步代码看起来像同步代码。

例

```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = 'Hello, world!';
      resolve(data);
    }, 1000);
  });
}

async function handleData() {
  try {
    const data = await fetchData();
    console.log(data); // 1 秒后输出 'Hello, world!'
  } catch (error) {
    console.error(error);
  }
}

handleData();
// 在这个示例中，handleData 函数使用 await 来等待 fetchData 函数的 Promise 完成，并返回结果。
```

#### 特点

- 代码更加简洁和易读。
- 错误处理可以使用标准的 `try/catch` 语句。

### 区别

1. **回调函数**：
   - 直接将函数作为参数传递并在适当时调用。
   - 易导致回调地狱，难以维护和阅读。
2. **Promise**：
   - 对异步操作的结果进行链式处理。
   - 解决了回调地狱问题，并提供了更好的错误处理。
3. **async/await**：
   - 基于 Promise 的语法糖，使异步代码看起来像同步代码。
   - 使代码更加简洁和易读，错误处理更加直观。

### 总结

- **回调函数**适用于简单的异步操作，但可能导致回调地狱。
- **Promise**通过链式调用解决了回调地狱问题，并提供了更好的错误处理机制。
- **async/await**进一步简化了基于 Promise 的异步代码，使其更易读和维护。





# 回调函数和高阶函数的区别 

### 回调函数

**定义**： 回调函数是指作为参数传递给另一个函数的函数，通常用来在某个事件或操作完成后执行特定的代码。

**特点**：

- **用途**：用于处理异步操作、事件处理等。

- **简单示例**：

  ```
  javascript复制代码function fetchData(callback) {
    setTimeout(() => {
      const data = 'Hello, world!';
      callback(data);
    }, 1000);
  }
  
  function handleData(data) {
    console.log(data);
  }
  
  fetchData(handleData); // 1 秒后输出 'Hello, world!'
  ```

### 高级函数（Higher-Order Functions）

**定义**： 高级函数是指接受一个或多个函数作为参数，或返回一个函数的函数。这是一个更广泛的概念，涵盖了回调函数的一部分，但不仅限于回调函数。

**特点**：

- **接受函数作为参数**：如 `Array.prototype.map`、`Array.prototype.filter` 等。

- **返回函数**：如函数工厂等。

- **复杂示例**：

  ```js
  // 接受函数作为参数
  function map(array, transform) {
    const result = [];
    for (const item of array) {
      result.push(transform(item));
    }
    return result;
  }
  
  const numbers = [1, 2, 3];
  const doubled = map(numbers, num => num * 2);
  console.log(doubled); // [2, 4, 6]
  
  // 返回函数
  function makeMultiplier(multiplier) {
    return function(number) {
      return number * multiplier;
    };
  }
  
  const double = makeMultiplier(2);
  console.log(double(5)); // 10
  ```

### 区别

1. **范围**：
   - **回调函数**：是一种特定类型的函数，作为参数传递给其他函数，用于在操作完成时执行代码。
   - **高级函数**：是一个更广泛的概念，指的是可以接受函数作为参数或返回函数的函数。
2. **用途**：
   - **回调函数**：主要用于处理异步操作、事件处理等需要在特定时刻执行的逻辑。
   - **高级函数**：用于函数式编程，提供更强的抽象和复用能力，可以用来创建更灵活和通用的函数。
3. **示例**：
   - **回调函数**：在异步操作或事件处理中的使用，如 `setTimeout`、事件监听器。
   - **高级函数**：如 `Array.prototype.map`、`Array.prototype.filter`，这些函数接受回调函数作为参数，并在内部调用这些回调。

### 总结

- **回调函数** 是高级函数的一种应用场景，它是作为参数传递的函数，用于处理异步操作和事件。
- **高级函数** 是一个更广泛的概念，它包括接受回调函数作为参数的函数，也包括返回函数的函数。

