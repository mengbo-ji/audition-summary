### 要进入高优先级打断低优先级的条件：

1. 当前正在render的workInProgressRoot 不等于 已经存在的root，**或者**当前要render的workInProgressRootLanes 不等于上次的上一次的lanes
2. 执行preparFreshStack()函数重置 fiber树（root）

