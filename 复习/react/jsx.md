## 概念

jsx它是一种JavaScript语法的扩展，React使用它来描述用户界面长成什么样子，虽然它看起来非常像HTML，但它确实是JavaScript。在React代码执行之前，Babel会将JSX编译为 React API

```jsx
<div className="container">
  <h3> Hello Reatt </h3>
  <p> React is great </p>
</div>
```

```js
React.createElement(
  "div", {
  className: "container"
	}, 
  React.createElement("h3", null, " Hello Reatt "),
  React.createElement("p", null, " React is great "));

```





