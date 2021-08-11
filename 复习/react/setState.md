![image-20201223225436537](/Users/jimengbo/Library/Application Support/typora-user-images/image-20201223225436537.png)

1. react里的更新都要经过requestWork，执行setState的时候通过debug可以看到三次setState过程`isBatchingUpdates`都为true，也就是都会return，并不会执行react的调度更新`performSyncWork`。那为什么会这样呢，我们往前看执行过程，可以找到一个`batchedUpdates`的方法。

2. 可以看到，它会return执行一个函数，这个函数相当于我们上面的`handleClick`（当然还会经过一系列的事件绑定），然后它会判断`!isBatchingUpdates && !isRendering`如果正确的话就执行`performSyncWork()`也就是react的指挥调度更新，正常情况下，它会等三个updates都创建完之后，再触发调度更新。但是在setTimeout的上下文它的执行环境是window，并没有`isBatchingUpdates`设置true的情况，所以它就会立即执行更新。
    那我们想在setTimeout里执行函数函数，也不想多次触发更新该怎么办呢，在react-dom里引用`batchedUpdates`方法，并使用它就ok了。

https://www.jianshu.com/p/9e5d510b6b2c

# setState的第二个参数 callback

1. 该函数会在setState函数调用完成并且组件开始重渲染的时候被调用
2. 所以会拿到最新的值

# setState它的主要流程如下：

  1、当调用setState时，实际上会执行enqueueSetState方法，并对partialState以及_pendingStateQueue更新队列进行合并，最终通过enqueueUpdate执行state更新

  2、 如果组件当前正处于update事务中，则先将Component存入dirtyComponent中。否则调用batchedUpdates处理。

而performUpdateIfNecessary方法获取_pendingElement、_pendingStateQueue、_pendingForceUpdate，并调用reciveComponent和updateComponent方法进行组件更新。
  3、batchedUpdates发起一次transaction.perform()事务
  4、开始执行事务初始化，运行，结束三个阶段
      初始化：事务初始化阶段没有注册方法，故无方法要执行
      运行：执行setSate时传入的callback方法，一般不会传callback参数
       结束：更新isBatchingUpdates为false，并执行FLUSH_BATCHED_UPDATES这个wrapper中的close方法
   5、FLUSH_BATCHED_UPDATES在close阶段，会循环遍历所有的dirtyComponents，调用updateComponent刷新组件，并执行它的pendingCallbacks, 也就是setState中设置的callback。