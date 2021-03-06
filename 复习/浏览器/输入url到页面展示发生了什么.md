## 网络篇

##### 网络请求：

1. 构建请求
2. 查找强缓存
3. DNS解析（domain name system）
4. 建立TCP连接
5. 发送HTTP请求

##### 网络响应：

1. 浏览器获得数据

##### 总结:

![img](https://user-gold-cdn.xitu.io/2019/12/15/16f080b095268038?imageslim)

## 解析算法篇

##### 构建dom树：

1. HTML法本（首先，我们应该清楚把握一点: HTML 的文法并不是`上下文无关文法`。）解析 HTML字符串

2. 标记化算法

   - 这个算法输入为`HTML文本`，输出为`HTML标记`，也成为**标记生成器**。其中运用**有限自动状态机**来完成。即在当当前状态下，接收一个或多个字符，就会更新到下一个状态。

3. 建树算法

   - 标记生成器会把每个标记的信息发送给**建树器**。**建树器**接收到相应的标记时，会**创建对应的 DOM 对象**。创建这个`DOM对象`后会做两件事情：

   1. 将`DOM对象`加入 DOM 树中。
   2. 将对应标记压入存放开放(与`闭合标签`意思对应)元素的栈中。

##### 样式计算：

1. 格式化样式 
   - 浏览器是无法直接识别 CSS 样式文本的，因此渲染引擎接收到 CSS 文本之后第一件事情就是将其转化为一个结构化的对象，即styleSheets。
2. 标准化样式
   - 有一些 CSS 样式的数值并不容易被渲染引擎所理解，因此需要在计算样式之前将它们标准化，如`em`->`px`,`red`->`#ff0000`,`bold`->`700`等等。
3. 计算每个样式的具体节点
   - 其实计算的方式也并不复杂，主要就是两个规则: **继承**和**层叠**。

##### 生成布局树：

- 现在已经生成了`DOM树`和`DOM样式`，接下来要做的就是通过浏览器的布局系统`确定元素的位置`，也就是要生成一棵`布局树`(Layout Tree)。

- 布局树生成的大致工作如下:
  1. 遍历生成的 DOM 树节点，并把他们添加到`布局树中`。
  2. 计算布局树节点的坐标位置。

> 有人说首先会生成`Render Tree`，也就是渲染树，其实这还是 16 年之前的事情，现在 Chrome 团队已经做了大量的重构，已经没有生成`Render Tree`的过程了。而布局树的信息已经非常完善，完全拥有`Render Tree`的功能。

##### 总结：

![img](https://user-gold-cdn.xitu.io/2019/12/15/16f080b2f718e4ad?imageslim)

## 渲染过程篇

接下来就来拆解下一个过程——`渲染`。分为以下几个步骤:

1. 建立`图层树`(`Layer Tree`)

2. 生成`绘制列表`

3. 生成`图块`并`栅格化`

4. 显示器显示内容

### 一、建图层树

因为你考虑掉了另外一些复杂的场景，比如3D动画如何呈现出变换效果，当元素含有层叠上下文时如何控制显示和隐藏等等。

为了解决如上所述的问题，浏览器在构建完`布局树`之后，还会对特定的节点进行分层，构建一棵`图层树`(`Layer Tree`)。

那这棵图层树是根据什么来构建的呢？

一般情况下，节点的图层会默认属于父亲节点的图层(这些图层也称为**合成层**)。那什么时候会提升为一个单独的合成层呢？

有两种情况需要分别讨论，一种是**显式合成**，一种是**隐式合成**。

##### 显式合成

层叠上下文也基本上是有一些特定的CSS属性创建的，一般有以下情况:

1. HTML根元素本身就具有层叠上下文。
2. 普通元素设置**position不为static**并且**设置了z-index属性**，会产生层叠上下文。
3. 元素的 **opacity** 值不是 1
4. 元素的 **transform** 值不是 none
5. 元素的 **filter** 值不是 none
6. 元素的 **isolation** 值是isolate
7. **will-change**指定的属性值为上面任意一个。(will-change的作用后面会详细介绍)

##### 隐式合成

接下来是`隐式合成`，简单来说就是`层叠等级低`的节点被提升为单独的图层之后，那么`所有层叠等级比它高`的节点**都会**成为一个单独的图层。

### 二、生成绘制列表

接下来渲染引擎会将图层的绘制拆分成一个个绘制指令，比如先画背景、再描绘边框......然后将这些指令按顺序组合成一个待绘制列表，相当于给后面的绘制操作做了一波计划。

### 三、生成图块和生成位图

现在开始绘制操作，实际上在渲染进程中绘制操作是由专门的线程来完成的，这个线程叫**合成线程**。

绘制列表准备好了之后，渲染进程的主线程会给`合成线程`发送`commit`消息，把绘制列表提交给合成线程。

### 四、显示器显示内容

1. 发送给显卡，

2. 显卡接收到浏览器进程传来的页面后，会合成相应的图像，并将图像保存到**后缓冲区**，然后系统自动将`前缓冲区`和`后缓冲区`对换位置，如此循环更新。

##### 总结：

![img](https://user-gold-cdn.xitu.io/2019/12/15/16f080b7b8926b7f?imageslim)