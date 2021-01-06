# React Hook 之 useState
## 基础概念
useState 是允许你在 React 函数组件中添加 state 的 Hook，
一般来说，在函数退出后变量就会”消失”，而 state 中的变量会被 React 保留
如果我们想要在 state 中存储两个不同的变量，只需调用 useState() 两次即可
useState 方法的返回值为：当前 state 以及更新 state 的函数
## 注意事项
+ 不可局部更新，如果state是一个对象，是无法局部更新的
```
import React, {useState} from "react";
import ReactDOM from "react-dom";

function App() {
  const [user,setUser] = useState({name:'Frank', age: 18})
  const onClick = ()=>{
    setUser({
      name: 'Jack'
    })
  }
  return (
    <div className="App">
      <h1>{user.name}</h1>
      <h2>{user.age}</h2>
      <button onClick={onClick}>Click</button>
    </div>
  );
}

//使用展开语法将初始user的性质放到新对象中
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

import React, {useState} from "react";
import ReactDOM from "react-dom";

function App() {
  const [user,setUser] = useState({name:'Frank', age: 18})
  const onClick = ()=>{
    setUser({
      ...user,
      name: 'Jack'
    })
  }
  return (
    <div className="App">
      <h1>{user.name}</h1>
      <h2>{user.age}</h2>
      <button onClick={onClick}>Click</button>
    </div>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
第一段代码中，最终更新后的user，内部没有age属性，而通过“...”将初始user的性质放入新对象之后，更新后的user的age没有改变，name改变了
所以setState是无法局部改变对象属性的
+ 传入setState的对象地址要和之前的不一样，否则React会认为数据没有变化
+ useState接受函数
```
const [state, setState] = useState(()=>{
return initialState
})
```
该函数返回初始state，且只执行一次
+ setState接受函数
```
import React, {useState} from "react";
import ReactDOM from "react-dom";

function App() {
  const [n, setN] = useState(0)
  const onClick = ()=>{
    setN(n+1)
    setN(n+1) // 你会发现 n 不能加 2
    // setN(i=>i+1)
    // setN(i=>i+1)
  }
  return (
    <div className="App">
      <h1>n: {n}</h1>
       
      <button onClick={onClick}>+2</button>
    </div>
  );
}
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
当我们传入的参数为（n+1）时，最终显示的结果n为1，当我们传入的参数为（i=>i+1），最终结果为2，所以一般情况下，建议使用函数参数