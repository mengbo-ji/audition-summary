1. Hooks是比[HOC](https://link.zhihu.com/?target=https%3A//reactjs.org/docs/higher-order-components.html)和[render props](https://link.zhihu.com/?target=https%3A//reactjs.org/docs/render-props.html)更优雅的逻辑复用方式。

2. 函数式组件的心智模型更加“声明式”。
3. hooks（主要是useEffect）取代了生命周期的概念（减少API），让开发者的代码更加“声明化”：
   - 新的思维：“我的组件有xxx这个副作用，这个副作用依赖的数据是props.A和state.B”。从过去的**命令式**转变成了**声明式**编程。
   - 其实仔细想一想，人们过去使用生命周期不就是为了判断执行副作用的时机吗？**现在hooks直接给你一个声明副作用的API，使得生命周期变成了一个“底层概念”，无需开发者考虑。开发者工作在更高的抽象层次上了。**

4. 践行 代数效应 view=fn（props）

   > 纯函数，将副作用从函数中剥离出去，我们只需要关注输入和输出.

5. 函数组件没有实例、没有生命周期、没有state和setState，只能接收props
6. 函数更灵活，更易拆分，更易测试

