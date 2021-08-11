# 如何理解React心智 这个名词呢?

1. 一般指react hook里需要手动写入依赖项和useCallback这些的使用，相对vue这种自动依赖收集机制，存在一定的心智(理解)成本

2. 所谓的心智负担是你引入这个依赖会不会导致后面一连串反应的不确定感

3. useEffect 的 dep 引入后就担心会不会导致死循环或者其他问题

4. 需要自己去考虑一些useState引起的不必要渲染，以及啥时候用useMemo和useCallback去进行性能优化，层级过多时要不要使用useContext的，使用useContext传递又会不会引起闭包…………

5. Vue3 中就是 需要判断这个变量到底是不是 reactive 的，如果不是，。。。这些都需要自己去想

