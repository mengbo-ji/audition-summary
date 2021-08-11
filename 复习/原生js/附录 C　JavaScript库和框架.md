## 附录 C　JavaScript库和框架

JavaScript**库**帮助弥合浏览器之间的差异，能够简化浏览器复杂特性的使用。库主要分两种形式：**通用**和**专用**。通用JavaScript库支持常用的浏览器功能，可以作为网站或Web应用程序开发的基础。专用JavaScript库支持特定功能，只适合网站或Web应用程序的一部分。本附录会从整体上介绍这些库及其功能，并提供相关参考资源。

## C.1　框架

“框架”（framework）涵盖各种不同的模式，但各自具有不同的组织形式，用于搭建复杂应用程序。使用框架可以让代码遵循一致的约定，能够灵活扩展规模和复杂性。框架对常见的任务提供了稳健的实现机制，比如组件定义及重用、控制数据流、路由，等等。

JavaScript框架越来越多地表现为单页应用程序（SPA，Single Page Application）。SPA使用HTML5浏览器历史API，在只加载一个页面的情况下通过URL路由提供完整的应用程序用户界面。框架在应用程序运行期间负责管理应用程序的状态以及用户界面组件。大多数流行的SPA框架有坚实的开发者社区和大量第三方扩展。

### C.1.1　React

React是Facebook开发的框架，专注于模型-视图-控制器（MVC，Model-View-Controller）模型中的“视图”。专注的范围让它可以与其他框架或React扩展合作，实现MVC模式。React使用单向数据流，是声明性和基于组件的，基于虚拟DOM高效渲染页面，提供了在JavaScript包含HTML标记的JSX语法。Facebook也维护了一个React的补充框架，叫作Flux。

- **许可**：MIT

### C.1.2　 Angular

谷歌在2010年首次发布的Angular是基于模型-视图-视图模型（MVVM）架构的全功能Web应用程序框架。2016年，这个项目分叉为两个分支：Angular 1.![x](https://private.codecogs.com/gif.latex?x)和Angular 2。前者是最初的AngularJS项目，后者则是基于ES6语法和TypeScript完全重新设计的框架。这两个版本的最新发布版都是指令和基于组件的实现，两个项目都有稳健的开发者社区和第三方扩展。

- **许可**：MIT

### C.1.3　Vue

Vue是类似Angular的全功能Web应用程序框架，但更加中立化。自2014年Vue发布以来，它的开发者社区发展迅猛，很多开发者因为其高性能和易组织，同时不过于主观而选择了Vue。

- **许可**：MIT

### C.1.4　Ember

Ember与Angular非常相似，都是MVVM架构，并使用首选的约定来构建Web应用程序。2015年发布的2.0版引入了很多React框架的行为。

- **许可**：MIT

### C.1.5　Meteor

Meteor与前面的框架都不一样，因为它是同构的JavaScript框架，这意味着客户端和服务器共享一套代码。Meteor也使用实时数据更新协议，持续从DB向客户端推送新数据。虽然Meteor是一个极为主观的框架，但好处是可以使用其稳健的开箱即用特性快速开发应用程序。

- **许可**：MIT

### C.1.6　Backbone.js

Backbone.js是构建于Underscore.js之上的一个最小化MVC开源库，为SPA做了大量优化，可以方便地更新应用程序状态。

- **许可**：MIT

## C.2　通用库

通用JavaScript库提供适应任何需求的功能。所有通用库都致力于通过将常用功能封装为新API，来补偿浏览器接口、弥补实现差异。其中有些API与原生功能相似，而另一些API则完全不同。通用库通常会提供与DOM的交互，对Ajax的支持，还有辅助常见任务的实用方法。

### C.2.1　jQuery

jQuery是为JavaScript提供函数式编程接口的开源库。该库的核心是通过CSS选择符匹配DOM元素，通过调用链，jQuery代码看起来更像描述故事情节而不是JavaScript代码。这种代码风格在设计师和原型设计者中非常流行。

- **许可**：MIT或GPL

### C.2.2　Google Closure Library

Google Closure Library是通用JavaScript工具包，与jQuery在很多方面都很像。这个库包含非常多的模块，涵盖底层操作和高层组件和部件。Google Closure Library可以按需加载模块，并使用Google Closure Compiler（附录D会介绍）构建。

- **许可**：Apache 2.0

### C.2.3　Underscore.js

Underscore.js并不是严格意义上的通用库，但提供了JavaScript函数式编程的额外能力。它的文档将Underscore.js看成jQuery的组件，但提供了更多底层能力，用于操作对象、数组、函数和其他JavaScript数据类型。

- **许可**：MIT

### C.2.4　Lodash

与Underscore.js一样，Lodash也是实用库，用于扩充JavaScript工具包。Lodash提供了很多操作原生类型，如数组、对象、函数和原始值的增强方法。

- **许可**：MIT

### C.2.5　Prototype

Prototype是对常见Web开发任务提供简单API的开源库。Prototype最初是为了Ruby on Rails开发者开发的，由类驱动，旨在为JavaScript提供类定义和继承。为此，Prototype提供了大量的类，将常用和复杂的功能封装为简单的API调用。Prototype包含在一个文件里，可以轻松地插入页面中使用。

- **许可**：MIT及CC BY-SA 3.0

### C.2.6　Dojo Toolkit

Dojo Toolkit是以包系统为基础的开源库，将功能分门别类地划分为包，可以按需加载。Dojo支持各种配置选项，几乎涵盖了使用JavaScript所需的一切。

- **许可**：“新”BSD许可或Academic Free License 2.1

### C.2.7　MooTools

MooTools是简洁、优化的开源库，为原生JavaScript对象添加方法，在熟悉的接口上提供新功能。由于体积小、API简单，MooTools在Web开发者中很受欢迎。

- **许可**：MIT

### C.2.8　qooxdoo

qooxdoo是致力于全周期支持Web应用程序开发的开源库。通过实现自己的类和接口，qooxdoo创建了类似传统面向对象编程语言的模型。这个库包含完整的GUI工具包和编译器，用于简化前端构建过程。qooxdoo最初是网站托管公司1&1的内部库，后来基于开源许可对外发布。

- **许可**：LGPL或EPL

## C.3　动画与特效

动画与特效是Web开发中越来越重要的一部分。在网站中创造流畅的动画并不容易。为此，不少库开发者已开发了包含各种动画和特效的库。前面提到的不少JavaScript库也包含动画特性。

### C.3.1　D3

数据驱动文档（D3，Data Driven Documents）是非常流行的动画库，也是今天非常稳健和强大的JavaScript数据可视化工具。D3提供了全面完整的特性，涵盖canvas、SVG、CSS和HTML5可视化。使用D3可以极为精准地控制最终渲染的输出。

- **许可**：BSD

### C.3.2　three.js

three.js是当前非常流行的WebGL库。它提供了轻量级API，可以实现复杂3D渲染与动效。

- **许可**：MIT

### C.3.3　moo.fx

moo.fx是基于Prototype或MooTools使用的开源动画库。它的目标是尽可能小（最新版3KB），并使开发者只写尽可能少的代码。moo.fx默认包含MooTools，也可以单独下载，与Prototype一起使用。

- **许可**：MIT

### C.3.4　Lightbox

Lightbox是创建简单图像覆盖特效的JavaScript库，依赖Prototype和script.aculo.us实现特效。其基本思想是可以使用户在当前页面的一个覆盖层中查看一个图像或多个图像。可以自定义覆盖层的外观和过渡。

- **许可**：Creative Commons Attribution 2.5