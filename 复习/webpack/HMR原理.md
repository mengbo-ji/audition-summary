## 为什么样式文件可以自动热更新

- 原因
  1. 样式文件被style-loader处理过后，已经处理过热更新了
  2. 所以我们在用webpack HMR的时候样式文件可以开箱即用

- 凭什么样式文件可以自动处理
  1. 因为样式一版比较有规律，在我们替换之后 webpack 可以直接将样式替换
  2. 但是js 太灵活了，毫无规律，有可能导出一个模块 有可能引入了新的东西 



## React 官方 HMR插件

```
npm install -D @pmmmwh/react-refresh-webpack-plugin react-refresh
```

[https://github.com/pmmmwh/react-refresh-webpack-plugin](https://github.com/pmmmwh/react-refresh-webpack-plugin)

