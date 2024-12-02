# **setTimeout和setinterval实现倒计时区别**

```js
    // 使用SetInterval实现倒计时
    let count = 10
    const h1El = document.querySelector('.count')
    let timer = setInterval(() => {
      count--
      h1El.innerText = count
      if(count <= 0) {
        clearInterval(timer)
        timer = null
      }
    }, 1000)



    // 使用setTimeout实现倒计时
    const h2El = document.querySelector('.count2')
    const countDown = (count) => {
      setTimeout(() => {
        count--
        h2El.innerText = count
        if (count > 0) {
          countDown(count)
        }
      }, 1000)
    }

    countDown(100)
```

setTimeout 

每间隔一秒生成一个任务，任务等待一秒后执行，<u>任务执行完成后</u> ，在生成下一个任务，任务等待一秒后执行，如此循环

所以setTimeout任务执行的间隔保存是1秒



setInterval

无视执行时间， 所有的操作就都在一秒中执行

每间隔一秒往任务队列中添加一个任务， 等待一秒后执行

不会等待任务会不会执行完成

反正任务开始执行了， 一秒后，就直接在添加任务就行了

这样会导致任务执行间隔小于一秒， 甚至会造成任务堆积



**setInterval：当任务执行时间大于任务间隔时间，会导致消费赶不上生成，执行还没有完成，下一个任务就又生成了**