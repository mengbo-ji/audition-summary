## 如何保证`Update`在被打断之后不丢失

1. `shared.pending`的环被剪开并连接在`updateQueue.lastBaseUpdate`后面。

2. 同时也会连接在`workInProgress updateQueue.lastBaseUpdate`与`current updateQueue.lastBaseUpdate`后面

3. 当`render阶段`被中断后重新开始时，会基于`current updateQueue`克隆出`workInProgress updateQueue`。由于`current updateQueue.lastBaseUpdate`已经保存了上一次的`Update`，所以不会丢失。

4. 当`commit阶段`完成渲染，由于`workInProgress updateQueue.lastBaseUpdate`中保存了上一次的`Update`，所以 `workInProgress Fiber树`变成`current Fiber树`后也不会造成`Update`丢失。

   

