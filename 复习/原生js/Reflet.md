#### Reflet 静态类 跟Math 一样

- 内部封装了 14个 静态方法
- 这些静态方法 就是Proxy 内部默认调用的方法

#### 为啥会有Reflet这个类

1. 统一提供一套用于操作对象的API

```js
const obj = {
  name: 'mengbo',
  age: '15',
};
console.log('name' in obj);
console.log(delete obj.name);
console.log(Object.keys(obj));

console.log(Reflect.has(obj, 'name'));
console.log(Reflect.deleteProperty(obj, 'name'));
console.log(Reflect.ownKeys(obj));
```



