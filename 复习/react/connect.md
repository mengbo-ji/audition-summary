# 原理

connect 方法是一个高阶组件，主要的两个参数都是函数，命名为 mapStateToProps 和 mapDispatchToProps，内部原理是获取 store 添加订阅后，将 state 和 dispatch 分别传入上面两个方法，返回需要的 state 和 改变 state 的方法添加到 UI 组件的 props 上。

前提是在应用顶层已经使用 provider 组件，并应用初始化时创建 store。

