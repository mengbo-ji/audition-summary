# HTTP0.9

1. HTTP/0.9 在建立好连接之后，只会发送类似GET /index.html的简单请求命令

2. 没有其他途径告诉服务器更多的信息，如文件编码、文件类型等

# HTTP1.0

#### 出现的原因

- 支持多种类型的文件下载是 HTTP/1.0 的一个核心诉求

#### 解决方案

- 通过请求头和响应头来协商
- 在发起请求时候会通过 HTTP 请求头告诉服务器它期待服务器返回什么类型的文件、采取什么形式的压缩、提供什么语言的文件以及文件的具体编码。

#### 特性

- 增加了请求头和响应头
- 引入状态码 处理服务器的错误
- 提供了Cache 机制， 减轻服务器压力
- 增加了用户代理的字段 统计客户端基础信息

# HTTP1.1

#### 特性：

1. 持久链接
2. 浏览器为每个域名最多同时维护 6 个 TCP 持久连接
3. 使用 CDN 的实现域名分片机制
4. 不成熟的 HTTP 管线化

3. 提供虚拟主机的支持

4. 对动态生成的内容提供了完美支持

5. 客户端 Cookie、安全机制

#### 改进持久链接

- 原因
  - HTTP/1.0 每进行一次 HTTP 通信，都需要经历建立 TCP 连接、传输 HTTP 数据和断开 TCP 连接三个阶段

- 解决
  - HTTP/1.1 中增加了持久连接的方法，它的特点是在一个 TCP 连接上可以传输多个 HTTP 请求，只要浏览器或者服务器没有明确断开连接，那么该 TCP 连接会一直保持。

#### 核心问题：带宽利用率低

- 原因
  - TCP慢启动
  - 同时开启了多条 TCP 连接，那么这些连接会竞争固定的带宽
  - HTTP/1.1 队头阻塞的问题

# HTTP2

#### 核心特性：多路复用机制

- 方法
  - 一个域名只使用一个 TCP 长连接
  - 消除队头阻塞问题
- 实现
  - 通过引入二进制分帧层，就实现了 HTTP 的多路复用技术

#### 其他特性

1. 可以设置请求的优先级

2. 服务器推送
3. 头部压缩

# HTTP3

- HTT2的一些问题
  - TCP 的队头阻塞、建立 TCP 连接的延时、TCP 协议僵化等问题
- 解决这些问题
  - 创建新的 QUIC 协议
    - 你可以把 QUIC 看成是集成了“TCP+HTTP/2 的多路复用 +TLS 等功能”的一套协议

- 关于 HTTP/3 的未来，
  - 从标准制定到实践再到协议优化还需要走很长一段路；
  - 因为动了底层协议，所以 HTTP/3 的增长会比较缓慢，这和 HTTP/2 有着本质的区别