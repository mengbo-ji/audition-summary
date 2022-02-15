### 背景

> webpack5出了已经有一年的时间了，稳定性已日渐茁壮，vue-cli里面已经使用
>
> 团队构建器是我4月份基于webpack4开发，当时用的loader和插件都是比较保守的，很多已经是两三年的东西了
>
> 特性：webpack5新增了 构建长期缓存、联邦模块, 更好的tree-shaking, 特别在针对打包慢，开发体验差的问题作出了很大的优化
>
> 拿态势感知来举例 现在基于webpack开发，每次build的体验极差，时间很长。

### 目标

- webpack版本升级到5

- webpack-dev-server升级到最新版

- 依赖的loader和插件随着webpack5的升级 肯定也需要升级

### 正文

> 记录下升级过程的坑和问题，还有是如何解决的，已经最后的结果和带来的提升

- 官方地址
  - [印记中文](https://juejin.cn/post/6882663278712094727)
  - [webpack5发布博客](https://webpack.docschina.org/blog/2020-10-10-webpack-5-release/)

#### 以前全是webpack配置项

##### cache [缓存](https://webpack.docschina.org/configuration/cache/#cache)

```js
const config = {
  /** ... */
  // 开启文件缓存，在第一次build之后 后续的build速度会提升一倍左右
  cache: {
    type: 'filesystem',
  },
  /** ... */
}
```

#### stats [统计](https://webpack.docschina.org/configuration/stats/)

```js
const config = {
  /** ... */
  // 添加stats属性, 控制控制台信息展示......
	stats: {
    chunks: false,
    chunkModules: false,
    colors: true,
    children: true,
    builtAt: true,
    modules: false,
    excludeAssets: [
      /assets/,
    ],
    errors: true,
  },
  /** ... */
}
```

##### devServer [webServer](https://webpack.docschina.org/configuration/dev-server/)

```js
const config = {
  devServer: {
    // 删除了contentBase
    // 添加了static属性
     static: {
      directory: 'your static path',
      publicPath: '/',
    },
    // 添加了client字段 将浏览器一些配置组装到client中
    client: {
      overlay: false,
    },
    // 删除了disableHostCheck
    // 删除了stat字段
  }
}
```

#### Module [Link](https://webpack.docschina.org/configuration/module/)

```js
// raw-loader、file-loader、url-loader 删除采用官方推荐的type: 'assets'
// 看官方：https://webpack.docschina.org/guides/asset-modules/
// eg:
  {
    test: /\.(png|jpe?g|gif|bmp|svg|eot|ttf|woff|woff2)$/,
-   loader: require.resolve('url-loader'),
+   type: 'asset',
+   generator: {
+     filename: 'assets/image/[name].[ext]',
    },
  },


//--------分割线
// css-loader、less-loader、postcss-loader升级之后 大多是写法变更
// eg: 
{
  loader: require.resolve('less-loader'),
-  options: {
- 	javascriptEnabled: true,
- }
+  options: {
+    lessOptions: {
+      javascriptEnabled: true,
+    },
  },
}
```

#### Plugin [插件](https://webpack.docschina.org/plugins/)

```js
// CopyWebpackPlugin
// BundleAnalyzerPlugin
// MinniCssExtractPlugin
// ReactRefreshWebpackPlugin (新增HMR插件，代替webpack自带的HRM)
// TerserPlugin
// CssMinimizerPlugin (新增CSS压缩，代替optimize-css-assets-webpack-plugin -> 不支持5)

// CopyWebpackPlugin 写法变了
new CopyWebpackPlugin({
  patterns: [
    { from: paths.appAssets, to: paths.appDistAssets },
  ],
})

// ReactRefreshWebpackPlugin react官方HMR插件，我们团队都是React项目所以就直接拿来用了，他可以帮我们在每一个文件的最后注入Module.hot.accept() 类似react-hot-loader
if (env.raw.NODE_ENV === 'development') {
  // 热更新
  config.plugins.push(new ReactRefreshWebpackPlugin({
    overlay: false, // 错误不展示到浏览器
  }));
}

// TerserPlugin webpack5对这个插件是开箱即用的，但是他默认保留了build之后的注释，导致代码大小增大两倍不止，我们还是要自定义下
if (env.raw.NODE_ENV === 'production') {
  const TerserPlugin = require('terser-webpack-plugin');
  const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');
  config.optimization = {
    minimize: true,
    minimizer: [
      // 添加js压缩
      new TerserPlugin(
        {
          parallel: true,
          terserOptions: {
          // https://github.com/webpack-contrib/terser-webpack-plugin#terseroptions
            compress: {
              comparisons: false,
            },
            safari10: true,
            format: {
              comments: false, //删除注释
            },
          },
          extractComments: false, // 删除注释
        }
      ),
      // 添加css压缩
      new CssMinimizerPlugin(),
    ],
  };

  // 开启性能提示
  config.performance = {};
  // sourceMap 开启nosources
  config.devtool = 'nosources-source-map';
}

```

### 效果

> 从打包速度和打包大小两方面分析

#### V4

![image-20211217173308592](/Users/jimengbo/Library/Application Support/typora-user-images/image-20211217173308592.png)

![image-20211217173905573](/Users/jimengbo/Library/Application Support/typora-user-images/image-20211217173905573.png)

![image-20211217173927542](/Users/jimengbo/Library/Application Support/typora-user-images/image-20211217173927542.png)

#### V5

![image-20211217174014129](/Users/jimengbo/Library/Application Support/typora-user-images/image-20211217174014129.png)

![image-20211217174118349](/Users/jimengbo/Library/Application Support/typora-user-images/image-20211217174118349.png)

![image-20211217174143364](/Users/jimengbo/Library/Application Support/typora-user-images/image-20211217174143364.png)