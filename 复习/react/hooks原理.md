# 使用原则

1. 不要在循环，条件判断，函数嵌套中使用hooks

2. 只能在函数组件中使用hooks

3. 自定义hooks 必须以use开头 这是约定

# 原理

1. 初次渲染的时候，按照 useState，useEffect 的顺序，把 state，deps 等按顺序塞到 memoizedState 链表中。
2. 更新的时候，按照顺序，从 memoizedState 中把上次记录的值拿出来。

