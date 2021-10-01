#### Proxy 对比Object.defineProperty() 的优点

1. Proxy 更为强大
   - Object.defineProperty() 只能监听属性的读写
   - Proxy可以监听到 delect 操作、对对象方法的调用 等等
2. Proxy 更好的支持数组对象的监视
3. Proxy 是以非侵入的方式监管了对象的读写