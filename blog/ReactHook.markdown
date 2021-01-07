# useEffect
Effect Hook 可以让你在函数组件中执行副作用操作,对环境的改变即为副作用
可以把 useEffect Hook 看做 componentDidMount，componentDidUpdate 和 componentWillUnmount 这三个函数的组合。
+ 当把“[ ]”作为第二个参数时，将作为componentDidMount使用
+ 没有第二个参数时，每次渲染之后都会执行
+ 作为componentDidUpdate使用时，可指定依赖
+ 作为componentWillUnmount使用时候，可以通过return来实现，每个effect都可以返回一个清除函数,React会在组件卸载的时候执行清除操作.

# useRef
```
const refContainer = useRef(initialValue);
```
useRef 返回一个可变的 ref 对象，其 .current 属性被初始化为传入的参数（initialValue）。返回的 ref 对象在组件的整个生命周期内保持不变。