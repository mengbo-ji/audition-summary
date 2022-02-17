**React 18 采用循序渐进的策略，由于 React 18 中的并发性是可选功能，所以并不会立刻对组件行为带来任何明显的破坏性变化。**你几乎不需要对应用程序中的代码进行任何改动就可以直接升级到 React 18，且可以根据自己的节奏和需要来尝试新特性。

总的来说，React 18 带来了以下 3 个方面的更新：

➢ Automatic batching

➢ SSR for Suspense

➢ New APIs for app and library developers

**● Automatic batching**

React 18 通过默认执行更多 batching (批处理) 来增加开箱即用的性能改进，无需在应用程序或库代码中手动批处理更新。

batching 是指，React 可以将回调函数中多个 setState 事件合并为一次渲染。

React 17 只在事件回调中 batching，React 18 则会对任何来源的 setState 做尽可能多的 batching， 即使在 promise、timeout 或者 event 回调中调用多次 setState，也都会合并为一次渲染。

将 ReactDOM.render 替换为 ReactDOM.createRoot 调用方式，即可开启这些新特性。

**● SSR for Suspense**

完整名称是：Streaming SSR with selective hydration。

即像水流一样，打造一个从服务端到客户端持续不断的渲染管线，而不是 renderToString 那样一次性渲染机制。selective hydration 表示选择性水合，水合指的是后端内容打到前端后，JS 需要将事件绑定其上，才能响应用户交互或者 DOM 更新行为，而在 React 18 之前，这个操作必须是整体性的，而水合过程可能比较慢，会引起全局的卡顿，所以选择性水合可以按需优先进行水合。

**● New APIs for app and library developers**

**Concurrent APIs：**

Concurrent Rendering 相关的变动是 React 18 的主要变动之一，简而言之，这个能力会让 React 应用保持更好的响应性。这是一种可中断渲染的设计架构。什么时候中断渲染呢？当一个更高优先级渲染到来时，通过放弃当前的渲染，立即执行更高优先级的渲染，换来视觉上更快的响应速度。

- useTransition：允许组件在切换到下一个界面之前等待内容加载，从而避免不必要的加载状态。
- startTransition：被 startTransition 回调包裹的 setState 触发的渲染 被标记为不紧急的渲染，这些渲染可能被其他紧急渲染所抢占。
- useDeferredValue：返回一个延迟响应的值，例如一个选择输入框过滤列表的场景，我们可以针对列表使用 useDeferredValue 传入选择器对应的值。

新的 startTransition 与 useDeferredValue API，本质上都是允许你将 UI 的一部分标记为较低的更新优先级。

**其他 APIs：**

- useSyncExternalStore：useSyncExternalStore 将替代 useMutableSource 用于订阅外部源，解决 Concurrent Rendering 可能导致的数据不一致的问题，也是库作者可能需要，一般开发者不太能用到。
- useId：useId 用于在客户端与服务端之间产生唯一 ID ，避免 SSR hydrate 时元素不匹配。
- useInsertionEffect：用于插入全局 DOM 节点。

React 18 将在明年与新的 React Native 架构（可用 React 18 特性）一起发布。