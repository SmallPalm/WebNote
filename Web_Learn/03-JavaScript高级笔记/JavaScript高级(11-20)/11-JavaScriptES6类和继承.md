# 认识class定义类

- 我们会发现 , 按照前面的构造函数形式创建 **类 **,不仅仅和编写普通的函数过于相似,  而且代码并不容易理解
- 在ES6 新的标准中使用了 class关键字来直接定义类
- 但是类本质上依然是前面 所讲的构造函数, 原型链的语法糖而已

**构造函数也称为类**

- 类的每一个实例都是对象（Object）类型
- JavaScript中的类实际上是一种特殊的对象
- 它们可以有属性和方法，并且可以被复制、传递和使用，就像其他对象一样
- 当你使用类创建一个新的实例时，实际上创建了一个新的对象
- 这个对象具有类定义的属性和方法。

### class类和function构造函数的区别

- class定义的类 , 不能作为一个普通的函数进行调用

# Class类中的实例方法和静态方法

实例方法

- 实例方法是在类的原型上定义的方法

- 实例方法可以被类的每个New 出来的实例来调用

- 实例方法需要通过类的实例来访问或调用

  - ```JS
    class MyClass {
        myMethod(){
        	//instance: 实例
        	//methid: 方法    
            console.log("This is 需要 instance 调用 method")
        }
    }
    
    const instance = new MyClass
    instance.mymethod()
    ```

静态方法

- 静态方法属于类本身
  - 而不是类的实例
  - 静态方法不会被类的实例继承
  
- 可以通过类本身来调用静态方法
  - 而不是类的实例
  
- ```js
  class MyClass {
    // 静态方法
    static myStaticMethod() {
      console.log('This is a static method');
    }
  }
  
  MyClass.myStaticMethod(); // 输出: This is a static method
  ```

# class类的构造函数

如果我们希望在创建对象的时候给类传递一些参数

- 每个类都可以一个自己的构造函数(方法) , 这个方法的名称是固定的constructor
- 当我们通过new操作符 , 操作一个类的时候会调用这个类的构造函数constructor
- 每一个类只能有一个构造函数, 如果包含多个构造函数, 会抛出异常

当我们通过new关键字操作类时，会调用这个constructor函数，并且执行如下操作：

1. 在内存中创建一个新的对象（空对象）
2. 这个对象内部的【【prototype】】（就是隐式原型proto）属性会被赋值为该类的prototype属性
3. 构造函数内部的this，会指向创建出来的新对象
4. 执行构造函数的内部代码（函数体代码）
5. 如果构造函数没有返回非空对象，则返回创建出来的新对象

# 类的实例方法

- 实例方法可以直接在类中定义
- 实例方法也是直接放在class类的原型上的



# 类的静态方法

- 静态方法通常用于定义直接使用类来执行的方法 , 不需要有类的实例 , 使用**static关键字**来定义
  - static : 静态

- 类的实例不能直接调用静态方法
  - 静态方法是属于类本身的，而不是类的实例。
- 调用静态方法时，需要使用类名来访问它们，而不是类的实例。

# ES6类的继承 -  extends

- 在ES6中新增了使用管extends关键性, 可以更方便实现继承

- ```js
  class Person{
  
  }
  class Students extends Person{
  
  }
  ```







# Class的类字段 (Class Fields)

- 类字段用于声明类的实例属性

- 在以前的JavaScript版本中, 通常在构造函数中声明实例属性

  - 但在最新的JavaScript中可以使用类字段语法来声明实例属性

- 类字段使用实例变量的语法来进行声明, 通常在类的最顶层

- ```js
  class MyClass {
    // 类字段
    myField = 10;
  
    myMethod() {
      console.log(this.myField);
    }
  }
  
  const instance = new MyClass();
  instance.myMethod(); // 输出: 10
  ```

# super关键字

-  Class为我们的方法中还提供了super关键字
  - 执行 super.函数名 来调用一个父类方法
  - 执行 super() 来调用一个父类constructor中的this指向的属性
- 注意:
  - 在子类(派生类)中的 构造函数中使用this或者返回默认对象之前
    - 必须通过super调用父类的构造函数
- super的使用位置有三个:
  - 子类的构造函数方法 , 实例方法 , 静态方法



# 继承内置类



## 类的混入mixin

- JavaScript的类只支持单继承 : 也就是只能有一个父类
  - 那么在开发中我们需要在一个类中添加更多相似的功能时
  - 这个时候可以使用混入(mixin)
- 相关的React高阶组件



# 对象字面量的增强

- ES6中对 对象字面量 进行了增强 , 称之为 Enhanced object literals (增强对象字面量)
- 字面量的增强主要包括三部分
  - 属性的简写 : Property Shorthand
  - 方法的简写 : Method Shorthand
  - 计算属性名 : Computed Property Names



# ES6解构

- ES6中新增了一个从数组或对象中方便获取数据的方法
  - 称之为解构 (Destructuring)
- 数组的解构
  - 基本解构过程
  - 顺序解构
  - 解构出数组 : ...语法
  - 默认值
- 对象的解构
  - 基本解构过程
  - 任意顺序
  - 重命名 
  - 默认值 

# 简化定义

var a = []  就是 var a = new Number()

var b = "" 就是 var a = new String()

a.push 就是通过原型链查找，Array 原型上的push等方法
