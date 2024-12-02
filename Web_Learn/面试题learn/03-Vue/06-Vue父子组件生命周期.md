#### Vue中父组件和子组件生命周期钩子函数执行顺序 ？

**加载渲染过程**

1. 父 beforeCreate
2. 父 Created
3. 父 beforeMount
4. 子 beforeCreate
5. 子 Create
6. 子 beforeMount
7. 子 mounted
8. 父 Mounted

**子组件更新过程**

1. 父 beforeUpdate
2. 子 beforeUpdate
3. 子 updated
4. 父 updated

**父组件更新流程**

1. 父 beforeUpdate
2. 父 Updated

**销毁过程**

1. 父 beforeDestroy
2. 子 beforeDestroy
3. 子 destroyed
4. 父 destroyed



# 细节

### 加载渲染过程

1. **父 beforeCreate**：这是父组件生命周期的开始，此时组件的实例刚刚被创建，但数据观察和事件/侦听器尚未被设置。
2. **父 Created**：在这一步，组件的实例已经完成数据观察和事件/侦听器的设置，但是组件的模板还没有被编译。
3. **父 beforeMount**：在这一步，组件的模板已经被编译，但是还没有挂载到DOM上。
4. **子 beforeCreate**：在父组件的模板开始渲染之前，子组件的生命周期钩子开始执行。
5. **子 Create**：子组件的数据观察和事件/侦听器设置完成。
6. **子 beforeMount**：子组件的模板编译完成，准备挂载到DOM。
7. **子 mounted**：子组件已经挂载到DOM上，可以访问到DOM元素。
8. **父 Mounted**：父组件的所有子组件都已挂载完成，父组件的模板也挂载到DOM。

### 子组件更新过程

1. **父 beforeUpdate**：当父组件的数据发生变化，需要更新DOM时，这个钩子被触发。
2. **子 beforeUpdate**：子组件接收到来自父组件的数据更新，准备更新。
3. **子 updated**：子组件的更新完成，DOM已经更新。
4. **父 updated**：所有子组件的更新完成后，父组件的更新也完成。

### 父组件更新流程

1. **父 beforeUpdate**：同子组件更新过程的第一步。
2. **父 Updated**：父组件的DOM更新完成。

### 销毁过程

1. **父 beforeDestroy**：父组件实例即将被销毁，进行清理工作。
2. **子 beforeDestroy**：子组件实例即将被销毁，进行清理工作。
3. **子 destroyed**：子组件的实例已经销毁完成。
4. **父 destroyed**：所有子组件都销毁后，父组件的实例也销毁完成。