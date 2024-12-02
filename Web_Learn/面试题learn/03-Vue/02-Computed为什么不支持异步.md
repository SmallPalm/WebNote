# Computed不支持异步

这是Vue设计层面的原因

computed的定义 就是 **依赖值改变 computed值就重新计算**

所以这里必须是同步的

否则 就可能 **依赖值改变 但 computed值没有进行重新计算**

一旦 computed 支持异步 computed就违背 定义了

computed会变得不稳定

相反

watch 定义 就是 监听数据的改变 , 从而做某件事

那 watch 在侦听 数据发生变化后 做同步 异步 都可以

不会违背定义



```js
//有效
computed: {
  async value() {
    return this.a + this.b // 有效
  }
}

// 无效
computed: {
  async value() {
    const res = await Promise(resolve => {
      setTimeout(() => {
        resolve(this.a + this.b)
      }, 0) 
    })
    
    console.log(res) //输出 3
    return
  }
}
```

