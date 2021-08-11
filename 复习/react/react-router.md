# 原理

### hash 路由：

1. 核心是监听了 load 和 onHashChange 事件，在页面刷新或者 URL hash 改变时渲染不同页面组件。 

### history API 路由：

1. 核心是通过 replaceState 和 pushState 去改变页面 URL，通过 popState 事件监听 history 对象改变的时候改变页面。

