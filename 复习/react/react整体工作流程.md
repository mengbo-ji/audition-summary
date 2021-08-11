# schedule 调度阶段

> 调度任务的优先级，高优任务优先进入**Reconciler**

这里调用的方法是`ensureRootIsScheduled`。

其中，`scheduleCallback`和`scheduleSyncCallback`会调用`Scheduler`提供的调度方法根据`优先级`调度回调函数执行。

```js
if (newCallbackPriority === SyncLanePriority) {
  // 任务已经过期，需要同步执行render阶段
  newCallbackNode = scheduleSyncCallback(
    performSyncWorkOnRoot.bind(null, root)
  );
} else {
  // 根据任务优先级异步执行render阶段
  var schedulerPriorityLevel = lanePriorityToSchedulerPriority(
    newCallbackPriority
  );
  newCallbackNode = scheduleCallback(
    schedulerPriorityLevel,
    performConcurrentWorkOnRoot.bind(null, root)
  );
}
```

### scheduler

1. 小顶堆 数据结构

# render 协调阶段

> 负责找出变化的组件

开始于`performSyncWorkOnRoot`或`performConcurrentWorkOnRoot`方法的调用

### reconciler

1. fiber
2. dfs
3. update

# commit 渲染阶段

> 负责将变化的组件渲染到页面上

`commitRoot`方法是`commit阶段`工作的起点

在`commit`阶段结尾会再调度一次更新。在该次更新中会基于`baseState`中`firstBaseUpdate`保存的`u1`，开启一次新的`render阶段`。

### renderer

1. ReactDom
2. ReactNative
3. ReactArt

## 流程概览

```sh
创建fiberRootNode、rootFiber、updateQueue（`legacyCreateRootFromDOMContainer`）

    |
    |
    v

创建Update对象（`updateContainer`）

    |
    |
    v

从fiber到root（`markUpdateLaneFromFiberToRoot`）

    |
    |
    v

调度更新（`ensureRootIsScheduled`）

    |
    |
    v

render阶段（`performSyncWorkOnRoot` 或 `performConcurrentWorkOnRoot`）

    |
    |
    v

commit阶段（`commitRoot`）
```