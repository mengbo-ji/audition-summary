#### 出现的原因

- Promise 的编程模型依然充斥着大量的 then 方法，虽然解决了回调地狱的问题，但是在语义方面依然存在缺陷，代码中充斥着大量的 then 函数，这就是 async/await 出现的原因。

#### 原理

- async/await 的基础技术使用了生成器和 Promise，生成器是协程的实现，利用生成器能实现生成器函数的暂停和恢复。

#### async

- 我们先来看看 async 到底是什么？根据 MDN 定义，async 是一个通过异步执行并隐式返回 Promise 作为结果的函数。
- 对 async 函数的理解，这里需要重点关注两个词：`异步执行`和`隐式返回 Promise`。

```js

async function foo() {
    console.log(1)
    let a = await 100
    console.log(a)
    console.log(2)
}
console.log(0)
foo()
console.log(3)
```

#### await

1. 当执行到await 100时，会默认创建一个 Promise 对象
2. 在这个 promise_ 对象创建的过程中，JavaScript 引擎会将该任务提交给微任务队列
3. 然后 JavaScript 引擎会暂停当前协程的执行，将主线程的控制权转交给父协程执行，同时会将 promise_ 对象返回给父协程
4. 主线程的控制权已经交给父协程了，这时候父协程要做的一件事是调用 promise_.then 来监控 promise 状态的改变
5. 随后父协程将执行结束，在结束之前，会进入微任务的检查点，然后执行微任务队列，微任务队列中有resolve(100)的任务等待执行，执行到这里的时候，会触发 promise_.then 中的回调函数
6. 该回调函数被激活以后，会将主线程的控制权交给 foo 函数的协程，并同时将 value 值传给该协程
7. foo 协程激活之后，会把刚才的 value 值赋给了变量 a，然后 foo 协程继续执行后续语句，执行完成之后，将控制权归还给父协程

以上就是 await/async 的执行流程。正是因为 async 和 await 在背后为我们做了大量的工作，所以我们才能用同步的方式写出异步代码来

面试题：

```js

async function foo() {
    console.log('foo')
}
async function bar() {
    console.log('bar start')
    await foo()
    console.log('bar end')
}
console.log('script start')
setTimeout(function () {
    console.log('setTimeout')
}, 0)
bar();
new Promise(function (resolve) {
    console.log('promise executor')
    resolve();
}).then(function () {
    console.log('promise then')
})
console.log('script end')
```

