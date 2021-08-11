## Loader

> 原理：模块转换器，用于把模块原内容按照需求转换成新内容。一个 Loader 其实就是一个 Node.js 模块，这个模块需要导出一个函数。 这个导出的函数的工作就是获得处理前的原内容，对原内容执行处理后，返回处理后的内容。
>

1. 使用 `style-loader`  `css-loader` `postcss-loader` `sass-loader` `less-loader`  转换css
2. 使用 `url-loader` 转换图片
3. 使用  `babel-loader`  `@babel/preset-env` `@babel/preset-typescript`  `@babel/preset-react`转转js
4. 使用 `file-loader`  处理文件
5. 使用 `css-modules-typescript-loader` 自动生成css.d.ts 提示文件
6. 使用 `mini-css-extract-plugin.loader` 配合 下面的`mini-css-extract-plugin`  plugin 实现抽取css文件。

## Plugin

> 原理：在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。Webpack 通过 Plugin 机制让其更加灵活，以适应各种应用场景。 

1. 使用 `SplitChunksPlugin` 自动拆分业务基础库
2. 使用 `optimize-css-assets-webpack-plugin` 压缩css
3. 使用 `terser-webpack-plugin` 代替老牌的 `uglify`  自动删除项目中无用的代码 
4. 使用 `optimization.splitChunks` 自动提取公共模块
5. 使用 `webpack-bundle-analyzer.BundleAnalyzerPlugin` 可视化分析 bundle大小
6. 使用 `mini-css-extract-plugin`  将 css 文件单独抽离 要配合对应的loader使用
7. 使用 `css-url-relative-plugin` 将css打包成相对路径
8. 使用 `progress-bar-webpack-plugin` 显示构建进度
9. 使用 `case-sensitive-paths-webpack-plugin`  处理路径大小写问题
10. 使用 `webpack.IgnorePlugin(/^\.\/locale$/, /moment$/)`  处理 .locale 文件
11. 使用 `fork-ts-checker-webpack-plugin`  支持typescript lint 的检查
12. 使用 `copy-webpack-plugin` 复制文件
13. 使用 `define-plugin` 定义环境变量
14. 使用 `html-webpack-plugin` 生成html文件

