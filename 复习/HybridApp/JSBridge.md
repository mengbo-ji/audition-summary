# JSBridge出现的原因

1. 仅仅嵌入WebView并加载特定的页面并不能完全满足所有的业务场景，
2. 有些业务场景需要使用原生能力，比如获取定位、调用原生弹窗等。有时app也需要通知业务页面作出指定的行为，比如重定向、修改隔离配置等。
3. h5和原生之间需要通信

# Js与Native通信

> JavaScript 调用 Native 的方式，主要有两种：

- 注入 API 和 拦截 URL SCHEME。

### 注入API

1. 注入 API 方式的主要原理是，通过 WebView 提供的接口，向 JavaScript 的 Context（window）中注入对象或者方法，让 JavaScript 调用时，直接执行相应的 Native 代码逻辑，达到 JavaScript 调用 Native 的目的。

### 拦截 URL SCHEME

1. URL SCHEME：URL SCHEME是一种类似于url的链接，是为了方便app直接互相调用设计的，形式和普通的 url 近似，主要区别是 protocol 和 host 一般是自定义的，例如: qunarhy://hy/url?url=http://ymfe.tech，protocol 是 qunarhy，host 则是 hy。

2. 拦截 URL SCHEME 的主要流程是：Web 端通过某种方式（例如 iframe.src）发送 URL Scheme 请求，之后 Native 拦截到请求并根据 URL SCHEME（包括所带的参数）进行相关操作。

# JSBridge原理

JavaScript 是运行在一个单独的 JS Context 中（例如，WebView 的 Webkit 引擎、JSCore）。由于这些Context 与原生运行环境的天然隔离，我们可以将这种情况与 RPC（Remote Procedure Call，远程过程调用）通信进行类比，将 Native 与 JavaScript 的每次互相调用看做一次 RPC 调用。如此一来我们可以按照通常的 RPC 方式来进行设计和实现。

在 JSBridge 的设计中，可以把前端看做 RPC 的客户端，把 Native 端看做 RPC 的服务器端，从而 JSBridge 要实现的主要逻辑就出现了：通信调用（Native 与 JS 通信） 和 句柄解析调用。（如果你是个前端，而且并不熟悉 RPC 的话，**你也可以把这个流程类比成 JSONP 的流程**）

Native 和 Javascript 通信的原理是 JSBridge 实现的核心，实现方式可以各种各样，但是万变不离其宗。这里，笔者推荐的实现方式如下：

- JavaScript 调用 Native 推荐使用 注入 API 的方式（iOS6 忽略，Android 4.2以下使用 WebViewClient 的 onJsPrompt 方式）。
- Native 调用 JavaScript 则直接执行拼接好的 JavaScript 代码即可。
- 也可以将URL SCHEME的Restful形式的接口参数格式同注入API方式相结合，做到接口调用方式上的兼容（只改动底层实现）