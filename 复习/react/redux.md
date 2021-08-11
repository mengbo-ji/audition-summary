## 使用原则

1. 单一数据流原则
   - 统一管理
   - 方便维护和调试
2. state 是只读的
   - 与React的setState相似，直接改变组件的state是不会触发render进行渲染组件的
   - Redux中唯一改变state的方法就是触发action
3. reducer 必须是纯函数
   - 接受旧的state 返回新的state
   - reducer 内部操作必须是无副作用的 他只是起到一个 连接action 和 state 的桥梁的作用

## 工作原理

1. react中state决定ui
2. 当用户触发了一些更新（点击button，搜索），就会为reducer派发一个action
3. reducer 接受到action之后呢 就会去更新state
4. state 变了 ui 就变了
5. store是包含了所有了state，可以把他看做所有状态的集合

