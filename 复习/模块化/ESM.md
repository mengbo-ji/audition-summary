## ES Modules 基本特性

- 自动采用严格模式， 忽略 'use strict'
- 每个ESM模块都是单独的私有作用域
- ESM是通过 CORS 去请求外部 js 模块的
- ESM 的script 标签会延迟执行脚本，跟添加了defer 属性一样，等页面渲染完毕 再去执行脚本，会在DomContentLoad 事件之前执行