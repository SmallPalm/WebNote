# 认识类的使用

- 在早期的JavaScript开发中

  - (ES5)我们需要通过函数和原型链来实现类的继承
  - (ES6) 引入了class关键字, 更加方便的定义和使用类

- TypeScript作为JavaScript的超集

  - 也是支持使用class关键字的
  - 并且还可以对类的属性和方法等进行静态类型检测

- 实际上整正在JavaScript的开发过程中, 我们更加习惯于函数式编程

  如

  - React开发中 : 更多使用的函数式组件以及结合Hook的开发模式
  - Vue开发中 : 更推崇使用Composition API
    - 类更好的作用
      - 类具有更强大的封装性, 所以我们也需要掌握

# 类的定义

- 声明类的属性 : 在类的内部声明类的属性以及对应的类型

  - 如果类型没有声明 , 那么属性的类型默认是any的

    - 也可以进给属性设置初始值

  - 在默认是strict Property Initialization模式下面我们的属性是必须初始化的

    - 如果没有初始化, 代码编译时, 会报错

    - 如果我们在strictPropertyINitialization模式下的确不希望给属性初始化

      - 可以使用name!: string 语法

        ```tsx
        class Person {
          name!: string
          age: number
          
          constructor(name: string, age: number) {
            //this.name = name
            this.age = age
          }
          
          running() {
            console.log(this.name + 'running')
          }
          
          eating() {
            console.log(this.name + 'eating')
          }
        }
        ```

- 类可以有自己的构造函数constructor
  - 当我们通过new 关键字创建in一个实例时,
    - 构造函数会被调用
- 类中可以有自己的函数, 定义的函数称之为方法



# 类的继承

- 面向对象的其中一大特性就是继承
  - 继承不仅仅可以减少我们的代码量, 也是多态的使用前提
    - 为什么是多态的前提
      - 多态性（Polymorphism）是指相同的接口可以使用不同的实现。它允许对象被看作是其父类的实例，从而实现方法的动态绑定。继承是多态实现的基础，因为只有在继承关系中，子类对象才能被看作是父类对象来使用。
        - **方法重载**：子类可以重载（覆盖）父类的方法，实现不同的行为。例如，`Dog`和`Cat`类可以有各自不同的`make_sound`方法
- 使用extends关键字实现继承, 子类使用super来访问父类



# 类的成员修饰符

- 在TypeScript中, 类的属性和方法支持三种修饰符
  - public ,  private, protected
- **public** : 修饰的是在任何地方都可以使用
  - **公有的属性或方法**
    - 默认编写的属性就是public
- **private** : 修饰的是仅在同一类中可见
  - **私有的属性或方法**
- **protected** : 修饰的是仅在类自身及子类中可见
  - **受保护的属性或方法**



# 只读属性readonly

- 如果有一个属性我们不希望外界可以任意的修改, 只希望确定值后直接使用
  - 那么可以使用readonly



# getters/setters

- 在前面一些私有属性 , 我们不能直接访问
  - 或者某些属性我们想要监听它的获取(getter) 和 设置(setter) 的过程
    - 这时可以使用存取器



# 参数属性(Parameter Properties)

TypeScript提供了特殊的语法

- 可以把一个构造函数参数转成一个同名同值的类属性
  - 这些就被称之为参数属性
- 你可以通过在**构造函数参数**前添加一个可见性修饰符
  - public private protected 或者 readonly 来创建参数属性
    - 最后属性字段也会得到这些修饰符



# 抽象类abstract

- 我们知道,  继承是多态使用的前提
  - 所以在定义很多通用的调用接口时
  - 我们通常会让调用者传入父类
    - 通过多态来实现更加灵活的调用方式
  - 但是, 父类本身可能并不需要对某些方法进行具体的实现
    - 所以父类中定义的方法, 我们可以定义为抽象方法

什么是抽象方法: 在TypeScript中没有具体实现的方法(没有方法体), 就是抽象方法

- 抽象方法, 必须存在于抽象类中
- 抽象类是使用abstract声明的类

抽象类特点

- 抽象类是不能被实例的话 (也就是不能通过new创建)
- 抽象方法必须被子类实现, 否则该类必须是一个抽象类