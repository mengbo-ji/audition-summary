## Fiber的理解

`React`内部实现的一套状态更新机制。

支持任务不同`优先级`，可中断与恢复，并且恢复后可以复用之前的`中间状态`。

其中每个任务更新单元为`React Element`对应的`Fiber节点`。

# 出现的原因

1. diff算法是同步更新的。更新过程是同步的，这可能会导致性能问题
2. 阻塞界面的渲染

# Fiber的原理

1. 时间分片

2. 浏览器空闲时期依次调用函数， 这就可以在主事件循环中执行后台或低优先级的任务。借鉴了利用了 requestIdleCallback的特性

   - 因为`requestIdleCallback`这个 API 目前还处于草案阶段，所以浏览器实现率还不高，所以在这里 React 直接使用了`polyfill`的方案。

     这个方案简单来说是通过`requestAnimationFrame`在浏览器渲染一帧之前做一些处理，然后通过`postMessage`在`macro task`（类似 setTimeout）中加入一个回调，在因为接下去会进入浏览器渲染阶段，所以主线程是被 block 住的，等到渲染完了然后回来清空`macro task`。

     总体上跟`requestIdleCallback`差不多，**等到主线程有空的时候回来调用**

3. fiber 借助单向链表数据结构将 diff 算法的递归遍历变为循环遍历。

# Fiber的优势

- 暂停工作，稍后再回来。
- 为不同类型的工作分配优先级。
- 重用以前完成的工作。
- 如果不再需要，则中止工作。

