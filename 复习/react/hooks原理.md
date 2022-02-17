# 使用原则

1. 不要在循环，条件判断，函数嵌套中使用hooks

2. 只能在函数组件中使用hooks

3. 自定义hooks 必须以use开头 这是约定

# 原理

1. 初次渲染的时候，按照 useState，useEffect 的顺序，把 state，deps 等按顺序塞到 memoizedState 链表中。
2. 更新的时候，按照顺序，从 memoizedState 中把上次记录的值拿出来。

## useEffect和useLayoutEffect

useEffect和useLayoutEffect作为组件的副作用，本质上是一样的。

共用一套结构来存储effect链表。

整体流程上都是先在render阶段，生成effect，并将它们拼接成链表，存到fiber.updateQueue上，最终带到commit阶段被处理。

他们彼此的区别只是最终的执行时机不同，一个异步一个同步，这使得useEffect不会阻塞渲染，而useLayoutEffect会阻塞渲染。

