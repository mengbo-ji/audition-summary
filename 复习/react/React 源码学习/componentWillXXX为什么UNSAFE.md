在某个组件`updateQueue`中存在四个`Update`，其中`字母`代表该`Update`要更新的字母，`数字`代表该`Update`的优先级，数字越小`优先级`越高。

```
baseState = '';

A1 - B2 - C1 - D2
复制代码
```

首次渲染时，`优先级`1。`B D`优先级不够被跳过。

为了保证`更新`的连贯性，第一个被跳过的`Update`（`B`）及其后面所有`Update`会作为第二次渲染的`baseUpdate`，无论他们的`优先级`高低，这里为`B C D`。

```
baseState: ''
Updates: [A1, C1]
Result state: 'AC'
复制代码
```

接着第二次渲染，`优先级`2。

由于`B`在第一次渲染时被跳过，所以在他之后的`C`造成的渲染结果不会体现在第二次渲染的`baseState`中。所以`baseState`为`A`而不是上次渲染的`Result state AC`。这也是为了保证`更新`的连贯性。

```
baseState: 'A'          
Updates: [B2, C1, D2]  
Result state: 'ABCD'
复制代码
```

我们发现，`C`同时出现在两次渲染的`Updates`中，他代表的`状态`会被更新两次。

如果有类似的代码：

```
componentWillReceiveProps(nextProps) {
    if (!this.props.includes('C') && nextProps.includes('C')) {
        // ...do something
    }
}
复制代码
```

则很有可能被调用两次，这与`同步更新`的`React`表现不一致！

基于以上原因，`componentWillXXX`被标记为`UNSAFE`。

## 总结

为了保证状态的连续性，当某个`Update`由于优先级低而被跳过时，保存在`baseUpdate`中的不仅是该`Update`，还包括链表中该`Update`之后的所有`Update`。

那些在低优先级后面的高优先级任务可能会之后多次，所以这与同步更新的React表现不一致


