Vuex的Vuejs应用程序的状态管理模式和库

它采用集中式存储管理数据，并使用相应的规则保证状态以一种可预测的方法发生变化



# Vuex通过

State，Getters，Mutations，Actions，Modules来使用工作

State：进行存储组件状态，网络请求数据

Getters：跟组件中Computed类似，进行获取数据派生数据，，拥有响应式

Mutations：进行State中数据同步，在修改State中，需要同步修改State。

- Vuex的规则规定只能通过Mutations才能改变State，并且所有的Mutations都是同步的

Actions：进行异步操作，在网络请求中获取到数据，在提交到Mutations中，不可以直接修改State，

Modules：解决Store对象过大的问题，将Vuex分割为模块，每个模块中都可以拥有自己的State，mutations，actions，getters，甚至可以嵌套子模块





# Vuex工作流程

1. 初始化：创建一个新的Vue Store实例，将 state、getters、mutations、actions 作为选项传入。
2. **组件中使用**：在 Vue 组件中，可以通过 `this.$store` 访问到 Vuex 的 state 和 getters，通过 `this.$store.commit` 触发 mutations，通过 `this.$store.dispatch` 触发 actions。
3. **修改状态**：当需要修改 state 时，必须通过调用 store.commit 方法来触发 mutation。Vuex 会追踪这些 mutation 的调用，在开发模式下提供相应的警告。
4. **异步操作**：在需要进行异步操作时，如从后端 API 获取数据，可以通过调用 store.dispatch 方法来触发 actions。Actions 类似于 mutations，不同之处在于 actions 提交的是 mutation 而不是直接变更 state，并且可以包含任意异步操作。
5. **模块化**：当应用变得复杂时，可以通过模块化来组织 Vuex 的状态管理。每个模块可以有自己的 state、mutations、actions 和 getters，模块内部也可以嵌套子模块。