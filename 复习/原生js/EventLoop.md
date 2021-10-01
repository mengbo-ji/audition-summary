# 浏览器EventLoop

## 同步和异步

javascript语言是一门“单线程”的语言，不能同时进行多个任务和流程,无论如何，js做事情的时候都是只有一条流水线，同步和异步的差别就在于这条流水线上各个流程的执行顺序不同。

### 同步任务

- 指的是，在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；

### 异步任务

- 指的是，不进入主线程、而进入"任务队列"的任务，只有等主线程任务执行完毕，"任务队列"开始通知主线程，请求执行任务，该任务才会进入主线程执行。

### 异步运行机制如下：

（1）所有同步任务都在主线程上执行，形成一个[执行栈](http://www.ruanyifeng.com/blog/2013/11/stack.html)（execution context stack）。

（2）主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。

（3）一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。

（4）主线程不断重复上面的第三步。

用一句话总结浏览器的 event loop 就是：

> 先执行一个 MacroTask，然后执行所有的 MicroTask；
> 再执行一个 MacroTask，然后执行所有的 MicroTask；
> ……
> 如此反复，无穷无尽……



# Node EventLoop

1. timer阶段 执行 setTimeout/setInterval回调
2. pedding callbacks阶段  执行由上一个 Tick 延迟下来的 I/O 回调（待完善，可忽略）
3. idle prepare阶段  内部调用（可忽略）

4. poll阶段 执行几乎所有的回调，除了 close callbacks 以及 timers 调度的回调和 setImmediate() 调度的回调，在恰当的时机将会阻塞在此阶段)

5. check阶段 执行setImmediate的回调
6. close callbacks

### 区别：

- 其实nodejs与浏览器的区别，就是nodejs的 MacroTask 分好几种，而这好几种又有不同的 task queue，而不同的 task queue 又有顺序区别，而 MicroTask 是穿插在每一种【注意不是每一个！】MacroTask 之间的。

### 执行过程：

1. 先执行所有类型为 timers 的 MacroTask，然后执行所有的 MicroTask（注意 NextTick 要优先哦）；

2. 进入 poll 阶段，执行几乎所有 MacroTask，然后执行所有的 MicroTask；

3. 再执行所有类型为 check 的 MacroTask，然后执行所有的 MicroTask；

4. 再执行所有类型为 close callbacks 的 MacroTask，然后执行所有的 MicroTask；

5. 至此，完成一个 Tick，回到 timers 阶段；
    ……
    如此反复，无穷无尽……