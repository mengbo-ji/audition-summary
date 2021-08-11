# 概念

1. 将一次事件回调中的 多次setState合并成一次的方法 就是batchedUpdates（批量更新策略）

# 如何实现

### 老版本

1. 老版本中 在batchedUpdates函数上下文执行的时候 会在executionContext 上下文中获得BatchedContext 上下文
2. 只要保证命中 batchedUpdates 的上下文就可以 保证批量更新策略
3. 源码是在finally阶段通过flushSyncCallbackQueue才会去触发一次更新

### 新版本

1. 新版本 lane 优先级模型下。是保证两次

