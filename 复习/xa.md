## 自我介绍

- 面试官好，我是吉孟波，河南洛阳人，从去年4月份到现在就职于同盾科技，负责小盾安全前端团队的核心架构和开发工作，在同盾科技之前有将近两年的时间以阿里云生态合作伙伴的身份就职于阿里云应用高可用SRE前端团队，负责SRE前端团队的架构地图业务和团队前端基建的核心开发工作，项目这块 以saas、paas、toB中后台项目为主，技术栈以 react + ts +hooks 为主，以上就是我的一个简单的自我介绍

## 挑一个项目说一说

- 高可用这个项目吧
- 我从两个角度去说一下
- 第一，从项目的体量上说，它是一个巨石应用，多人维护，多人开发，复杂度很高的一个项目
- 第二，从技术架构的角度来讲
  - 项目工程化架构：自建项目，依赖阿里云内部just cli脚手架和自己的一个团队构建器、eslint工具包也是自己搭建的
  - 我们的脚手架非常的定制化，他和cra的一些区别，比如cra如果我们要抽离webpack的配置的话 需要inject，inject之后cra他就不在管你了，要你自己维护了，但是我们的脚手架是提供 一个config-overrides, 在合适的时机 去覆盖我们一些我们想要改动的webpack配置
  - 从项目用到的技术栈来看，我们是ts + react + hooks，还有一些2D的一些图表库，比如bizCharts、3D图表库g6，svg.js
  - 业务上我所主要负责的是架构地图的开发工作，架构地图他是以拓扑图的形式来呈现我们系统的上下有关系，比如 waf - node - k8s ，核心依赖的技术库是svg.js 这个库。他是一个矢量的svg.js的库，
  - svg 和 canvas的区别
    - SVG更适合用来做动态交互，而且SVG绘图很容易编辑，只需要增加或移除相应的元素就可以了，
    - SVG输出的图形是矢量图形，后期可以修改参数来自由放大缩小，不会失真和锯齿。而canvas输出标量画布，就像一张图片一样，放大会失真或者锯齿
    - Canvas是基于位图的图像，它不能够改变大小，只能缩放显示
    - Canvas不支持事件处理器，SVG支持事件处理器
  - 架构地图难点
    - 升级svg.js2.x-3.x
    - 利用requestAnimationFrame来提高svg的渲染性能

## 为什么离职

#### 两个角度考虑

- 第一，对咱们公司我也有一点了解，新奥集团 在全球这个公共事业和能源这一块是非常大的一个巨头公司，核心业务以清洁能源为主，而且新奥在之前已经有几次互联网变革，比如泛能网这些， 现在国家对清洁能源领域大力的支持，我非常看好这个赛道，
- 第二，是我跟老板的关系非常的好，老板安排是我入职以后负责团队基础建设这块的工作，而这正是我在技术上想发展的方向， 所以我没有理由不来。
- 关系好那你为啥离职
  - 组织架构变动，我被放到后端下面了，所以考虑到自身的一个发展就离职了。
  - 现在老板也出来了，正好我们都非常看好这个赛道，又能做自己想做的事，所以真的没有理由不来

## TS能干什么

- js是弱类型语言，在编译阶段是不知道变量的类型的，只有在运行阶段才可以知道
- ts可以帮助我们在编译阶段 判断数据类型，发现编译时错误、

- 静态检查：判断数据类型、低级错误编译时发现、非空判断（重要）、类型推断
- 面向对象编程增强：访问控制、接口、类、ES6模块系统增强

## 项目用到的技术

#### 项目

- 采用dva的包和 团队内部构建器自己搭建项目

#### 技术栈

- 日常开发：react + ts + hooks + bizCharts
- 对内项目：vite

#### 工程化

> 开发 - 构建 - 部署 一整套规范流程

- 开发
  - 分支命名规范：feature、fix等命名
  - 代码风格统一：超严格的eslint、styleLint自动化配置方案
  - 技术栈统一：全部采用react + ts + hooks的方式，二D图表采用bizCharts，微前端采用ConsoleOS
- 构建
  - 打包构建统一：团队有适合自己的内部构建器，可支持 私有云 公有云等的构建发布任务
  - 统一的云构建 中间平台
- 部署
  - cdn部署

## 对vue了解吗

- 了解不多，mvvm框架，双向数据流

## var let const

#### 共同点

- 都可以用来声明变量

#### 不同点

- var 声明的变量会默认挂在到window上，而let 和 const 不会
- var 声明的变量存在变量提升，这是因为var声明的变量存在变量环境中，在编译阶段会被赋值默认值，而let 和 const存在词法环境中，在编译阶段不会赋值默认值，所以存在暂时性死区这个概念
- let 和 const 都es6新增的，都可以声明变量
- let 和 const声明变量不可以重复声明，不可以提前使用
- const 代表常量的意思，一般用来声明不会改变的变量，当然引用类型还是会改变的，只是不能重新赋值

## this指向和改变this指向的方法

#### this指向

- 我们可以单纯的理解为 谁调用this 那就指向谁

#### 改变this指向的方法

> call apply bind

- 共同点：都可以改变this的指向，第一个参数都是要指向的this
- 不同点
  - call和apply返回的是函数调用的结果，而bind返回的是函数体
  - call和bind的第二个参数就是传入函数的参数，apply第二个参数是一个数组，数组中每一项才是传入函数的参数

## Vue组件是怎样传参的

- 不了解

#### react

- 组件props的形式传参

## react 生命周期

#### 类组件

- 用的不多

### hooks

- hooks本身就是函数，更优雅的复用

- 函数式组件的心智模型更加“声明式”。

- hooks（主要是useEffect）取代了生命周期的概念（减少API），让开发者的代码更加“声明化”：

  - 新的思维：“我的组件有xxx这个副作用，这个副作用依赖的数据是props.A和state.B”。从过去的**命令式**转变成了**声明式**编程。
  - 其实仔细想一想，人们过去使用生命周期不就是为了判断执行副作用的时机吗？**现在hooks直接给你一个声明副作用的API，使得生命周期变成了一个“底层概念”，无需开发者考虑。开发者工作在更高的抽象层次上了。**

- 践行 代数效应 view=fn（state）

  > 纯函数，将副作用从函数中剥离出去，我们只需要关注输入和输出.

- 函数更灵活，更易拆分，更易测试，函数在打包的时候 如果是空函数是可以被压缩的，class中的函数 存在引用 所以做不到

- hooks 可以发挥react18并发模式最大的优势

  - react为18提供了一些 针对并发模式的hook `useDeferredValue` `useTransition` 而class是没有的

## react-router标签含义

#### Router

- 外层最大的标签，包裹整个路由

#### Route

- 每个路由对应一个route
- path exact component render等

#### Switch

- 匹配唯一

#### Redirect

- 重定向 from to

#### hooks

- useHistory
- useLoaction
- useParams
- useRouteMatch

## react合成事件

#### 特点

- 事件委托的形式

- React自己实现了一套高效的事件注册，存储，分发和重用逻辑，最大化的解决了很多浏览器兼容问题
- 所有组件的事件都会挂在到document上 react17以后是挂在到根节点root上
- 使用对象池管理合成事件的 创建和销毁

## react组件更新的整个过程

- 调用 ReactDom.render 、this.setState、this.forceUpdate、useState的返回的回调函数（dispatchAction）触发更新，创建Update对象
- 调用类组件的render方法或者函数组件本身，获取return 之后新的jsx
- 调度器scheduler根据不同更新不同的优先级 选出优先级最高的更新进入协调器reconciler
- 协调器reconciler 对比current Fbier 和 workInprogress Fiber两颗 fiber树，找到不同，然后打上对应的标记，Placement、Update、Deletion

> 上面两步 随时会由于 浏览器空闲时间不够或者有更高优先级的事件发生而中断

- 标记打完之后 交给渲染器renderer，渲染器根据不同的标记 作出不同的dom操作

## MVVM

#### 概念

- MVVM 可以写成 MV-VM，是 Model View - ViewModel 的缩写，可以算是 MVP 模式的变种，View 和 Model 职责和 MVP 相同，但 ViewModel 主要靠 DataBinding 把 View 和 Model 做了自动关联，框架替应用开发者实现数据变化后的视图更新，相当于简化了 Presenter 的部分功能

  > 前端比较熟悉的 Vue 正是使用 MVVM 模式，使用 Vue 实现示例功能

- 在 View 中做了数据和视图的绑定，在 ViewModel 中只需要更新数据，视图就会自动变化，DataBinding 由框架实现

## 设计模式

#### 概念

1. 发布-订阅
2. 一对多，一个被观察者，多个观察者
3. 优点：支持广播，解耦性强
4. 缺点：大量观察者，广播有性能问题

#### 应用场景

1. vue的数据绑定 就是利用了观察者模式

   ![img](https://img2018.cnblogs.com/blog/1492200/201810/1492200-20181023200852131-291342969.png)

2. js事件绑定 也是观察者模式

## leader 如何搞定这个项目

1. 第一步 产品、前后端、测试同学 大家需求评审完毕

2. 第二步 技术评审+排期，在这步之前其实需求评审的结果基本可以作出用什么技术架构的判断了，排期这块，要根据实际项目的紧急度。和目前团队的实际情况，人员配置、手头工作量等
3. 确定排期、确定技术架构、确定人员 、建好teamwork 就开始全力开发了
4. 现在基本都是 前后端分离的年代了，所以前端同学 可以做一些前期的准备，比如公共模块的抽离、方法的复用。针对一些评审时 觉得难的一些地方提前调研，避免后期影响到项目的上线
5. 在开发过程中也要随时的了解开发进度，把控项目整体进度
6. 开发完毕之后，前后端联调完毕、提测结束、上线

## 深拷贝和浅拷贝（区别、一些相关的方法以及自己如何实现一个深拷贝）

#### 浅拷贝

- 扩展运算符
- Object.assign()

#### 深拷贝

- JSON.parse和JSON.stringify
- 递归拷贝
- 防止循环引用（采用Map的形式来存储数据）

## loader和plugin的区别

#### Loader

> 原理：模块转换器，用于把模块原内容按照需求转换成新内容。一个 Loader 其实就是一个 Node.js 模块，这个模块需要导出一个函数。 这个导出的函数的工作就是获得处理前的原内容，对原内容执行处理后，返回处理后的内容。

1. 使用 `style-loader`  `css-loader` `postcss-loader` `sass-loader` `less-loader`  转换css
2. 使用 `url-loader` 转换图片
3. 使用  `babel-loader`  `@babel/preset-env` `@babel/preset-typescript`  `@babel/preset-react`转转js
4. 使用 `file-loader`  处理文件
5. 使用 `css-modules-typescript-loader` 自动生成css.d.ts 提示文件
6. 使用 `mini-css-extract-plugin.loader` 配合 下面的`mini-css-extract-plugin`  plugin 实现抽取css文件。

#### Plugin

> 原理：在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。Webpack 通过 Plugin 机制让其更加灵活，以适应各种应用场景。
>
> Plugin实际是一个类（构造函数），通过在plugins配置中实例化进行调用， 它在原型对象上指定了一个apply方法，入参是compiler对象

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

## 做过哪些webpack的配置

........可多了，loader、plugin、alias、entry、output、publicPath

## 说一下bundle和chunks

1. 对于一份同逻辑的代码，当我们手写下一个一个的文件，它们无论是 ESM 还是 commonJS 或是 AMD，他们都是 **module** ；
2. 当我们写的 module 源文件传到 webpack 进行打包时，webpack 会根据文件引用关系生成 **chunk** 文件，webpack 会对这个 chunk 文件进行一些操作；
3. webpack 处理好 chunk 文件后，最后会输出 **bundle** 文件，这个 bundle 文件包含了经过加载和编译的最终源文件，所以它可以直接在浏览器中运行。

`module`，`chunk` 和 `bundle` 其实就是同一份逻辑代码在不同转换场景下的取了三个名字：

我们直接写出来的是 module，webpack 处理时是 chunk，最后生成浏览器可以直接运行的 bundle。

## react类组件和函数式组件的区别（展开说一下，例如hooks什么的）

## 为什么不能在if里写

## setState和useState的区别

## react怎么在根结点之外插入节点（例如模态框、Toast）

1. ReactDOM.createPortal

```js
function createPortal(
  children: ReactNodeList,
  container: Container,
  key: ?string = null,
): React$Portal {
  invariant(
    isValidContainer(container),
    'Target container is not a DOM element.',
  );
  // TODO: pass ReactDOM portal implementation as third argument
  // $FlowFixMe The Flow type is opaque but there's no way to actually create it.
  return createPortalImpl(children, container, null, key);
}
```

createPortal函数主要有三个参数，分别是children（需要渲染的组件）、container（需要渲染到的指定节点）、key。开发中我们主要关注children和container即可

## react hooks有哪几种？其中useEffect是做什么的？

## useMemo在什么情况下使用

## 相比class component，hooks有哪些优势？

## 请挑一个项目聊聊你在其中做的亮点

## webpack都用过哪些打包优化手段？

#### 减少打包体积

1. `webpack.IgnorePlugin(/^\.\/locale$/, /moment$/),`
   - 忽略不需要的moment文件
2. 路由懒加载
   - React.lazy
3. CDN
   - externals配置
4. 压缩css
   - `optimize-css-assets-webpack-plugin`压缩css
5. 压缩js
   - `optimization.splitChunks` 提取公共模块
   - `optimization.minimizer 配合 terser-webpack-plugin` 压缩js 删除无用代码
6. `webpack.DllPlugin`自带插件
   - 业务代码和第三方模块可以被打包到不同的文件里
   - 避免打包出单个文件的大小太大，不利于调试
   - 将单个大文件拆成多个小文件之后，一定情况下有利于加载（不超出浏览器一次性请求的文件数情况下，并行下载肯定比串行快）
   - 提升构建速度，第三方库没有变更时，由于我们只构建业务相关代码，相比全部重新构建自然要快的多。

#### 优化打包速度

##### 不要让 `loader` 做太多事情

1. 用 `include` 或 `exclude` 来帮我们避免不必要的转译

##### 减少路径深度

1. 配置路径别名 alias

##### 删除冗余代码 

##### `Tree-Shaking`

1. Tree-Shaking 可以在编译的过程中获悉哪些模块并没有真正被使用，这些没用的代码，在最后打包的时候会被去除

2. Tree-Shaking 的针对性很强，它更适合用来处理模块级别的冗余代码

##### webpack 按需加载

1. require.ensure(dependencies, callback, chunkName)

2. 在 React-Router4 中，我们确实是用 Code-Splitting 替换掉了楼上这个操作

3. 所谓按需加载，根本上就是在正确的时机去触发相应的回调。理解了这个 require.ensure 的玩法，大家甚至可以结合业务自己去修改一个按需加载模块来用。

## 读过react源码哪一部分，能否讲一两个点

- ReactFiber.new.js

```js
function FiberNode(
  tag: WorkTag,
  pendingProps: mixed,
  key: null | string,
  mode: TypeOfMode,
) {
  // 作为静态数据结构的属性
  this.tag = tag; // Fiber对应组件的类型 Function/Class/Host...
  this.key = key; // key属性
  this.elementType = null; // 大部分情况同type，某些情况不同，比如FunctionComponent使用React.memo包裹
  this.type = null; // 对于 FunctionComponent，指函数本身，对于ClassComponent，指class，对于HostComponent，指DOM节点tagName
  this.stateNode = null; // Fiber对应的真实DOM节点

  // 用于连接其他Fiber节点形成Fiber树
  this.return = null; // 指向父级Fiber节点
  this.child = null; // 指向子级Fiber节点
  this.sibling = null; // 指向右边第一个兄弟Fiber节点
  this.index = 0;

  this.ref = null;

  // 作为动态的工作单元的属性
  this.pendingProps = pendingProps;
  this.memoizedProps = null;
  this.updateQueue = null;
  this.memoizedState = null; //保存的对应组件的hook
  this.dependencies = null;

  this.mode = mode;

  // Effects
  this.flags = NoFlags;
  this.subtreeFlags = NoFlags;
  this.deletions = null;

  // 调度优先级相关
  this.lanes = NoLanes;
  this.childLanes = NoLanes;

  // 指向该fiber在另一次更新时对应的fiber
  this.alternate = null;
}
```

- ReactFiberHooks.new.js

  - mount和update阶段 调用的是不同的hooks
    - Mount: HooksDispatcherOnMount
      - mountXXX
    - Update: HooksDispatcherOnUpdate
      - updateXXX

  - useState的 callback返回函数 dispatchAction
    - 接受本次update，并把本地的update 挂在到 hook.queue.pending环状链表
  - useState的源码

