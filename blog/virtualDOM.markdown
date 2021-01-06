# 虚拟 DOM
虚拟DOM是一个能代表 DOM 树的对象，通常含有标签名、标签上的属性、事件监听和子元素们，以及其他属性
我们直接看react的虚拟dom的真实呈现
```javascript
//React
const vNode={
   key:null,
   props:{ 
     children:[
     {type: 'span', ...},{type: 'span', ...}//子元素们
     ],
     className:'red',//标签属性
     onClick:()=>{} //事件
   },
   ref:null,
   type:'div', //标签名
   ...
}

//Vue   
const vNode = {
  tag: "div", // 标签名 or 组件名
  data: {
    class: "red", // 标签上的属性
    on: {
      click: () => {} // 事件
    }
  },
  children: [ // 子元素们
    { tag: "span", ... },
    { tag: "span", ... }
  ],
  ...
}
```
可以看得出来，虚拟DOM是一个JS对象，里面有各种数据解构，Vue跟React的虚拟DOM几乎一样。
## 创建虚拟DOM
上面的虚拟dom要怎样来创建出来呢？
react使用了一个叫creatElement的函数，它是这样写的
```javascript
createElement('div',{className:'red',onClick:()=> {}},[
    createElement('span', {}, 'span1'),
    createElement('span', {}, 'span2')
  ]
)
```
如果真的要这样写代码，那可真的丑的没边了，于是大神们想到使用编译器来编译上面的代码，让它变得更简单,于是就有了JSX
```html
<div className="red" onClick={fn}>
    <span>span1</span>
    <span>span2</span>
</div>
```
上面的JSX会被babel编译，最后成为原始createlement的形式。
创建了虚拟DOM，怎样渲染呢
```html
<div class='dom'>
  <ul>
    <li></li>
    <li></li>
  <ul/>
</div>
```
上面就是一个dom树，那么我们来结合react的虚拟dom来分析一下dom结构树。
首先，上面的dom中，外层的是一个div的type,class（className）为dom,里面有个children,type是ul...
如果用js对象来表示呢？
```
{
   type:'div', //标签名
   props:{ 
     children:[
       {type: 'ul', 
          props:{
             children:[{type:'li'..}]}
       }//子元素们
     ]
     className:'dom',//标签属性
   }, 
   ...
}
```
上面的代码我们需要注意的点是标签名type，children和className,现在我们好像知道了要插入的节点信息，是不是可以尝试写一个函数复用？
下面的代码不要细究语法，是用伪代码写的。
```javascript
function render(type,className,children){
   let node=document.createNode(type);//创建外层div
   node.style.className=className //设置外层div的className
   let childNode=children.map((c)=>{
     return render(c.type,c.className,c.children)
     ...
   }) //遍历它的children属性
   node.append(childNode) //最后插入到node节点中
   return node
}
document.querySelector('#root').append(render('div','dom',[]))
//最后把整个创建的node插入到浏览器已有的根节点（id为root）中
```
但是因为元素的内容太多了，我们的参数也会很多，所以我们就使用一个对象来包裹所有跟元素相关的属性，并且把要root节点也放到函数参数内，这样就只需要传入两个参数，一个是JS对象（包含要插入节点的信息），一个是需要插入的节点。
这个函数是这样调用的
```javascript
render({type:'div',className:'dom'...},rootNode)
```
再来对比一下React渲染函数
```
//JSX
const App:FC=()=>{ 
   return <div className='demo'>这是一个简单的demo</div>
   // 翻译成return createElement('div',{className:'demo'},...)
   //createElement会返回JS对象---虚拟dom
}

ReactDOM.render(
    <App /> 
    //这里的App就是执行App() 获得一个JS对象---虚拟dom
  ,
  document.getElementById("root")
);
// render函数执行后的参数是虚拟dom对象和要插入在哪个节点内
//render是渲染用的函数
```
那么我们可以得出，JSX语法是用来得到一个JS对象的，这个JS对象就是虚拟DOM，最后的这个JS对象会随着ReactDOM.render变成被渲染成浏览器节点
react在中间做了更多工作，上面所有只是对其思想的一次简单介绍。
## 虚拟DOM的优缺点
### 虚拟DOM的优点
+ 减少次数
  
  例如添加节点，我们可以通过innerHTML或者append插入，但是实践证明，假设插入1000个节点，使用append方式和innerHTML字符串的方式效率并不高，那么虚拟DOM就是通过把节点情况都存入数组，然后再一次性渲染出来，这样能够有效将原本的1000次合并成一次，在减少次数的情况下，浏览器渲染效率提高了，优化变好了。
```
var arr = [];
var a = '<a href="javascript=;">添加</a>';
for (var j = 0; j < 100; j++) {
   arr.push(a); //把a都丢入数组中
	}
div.innerHTML = arr.join('') //把数组变成字符串 然后让innerHtml获取，得到添加元素的效果
```
+ 减少范围

  DOMdiff算法可以把多余的操作省略掉，比如已经在页面中渲染的，那么DOMdiff不回将他重复执行渲染，而是把多出来的部分给渲染出来

+ 跨平台虚拟DOM支持小程序、IOS应用、安卓应用等多平台，因为本身它就是一个JS对象，自然支持各依赖环境平台的语法。

## 虚拟DOM的缺点
需要额外创建函数，也就是上面所说的很难写的createElement或者Vue的h函数,不过这种方式已经被克服，React采用JSX语法，而Vue则通过模板语法
```
//JSX
const App:FC=()=>{ 
   return <div className='demo'>这是一个简单的demo</div>
   // 翻译成return createElement('div',{className:'dom'},...)
}

ReactDOM.render(
    <App /> 
    //这里的App就是执行App() 获得一个JS对象---虚拟dom
  ,
  document.getElementById("root")
);
// render函数执行后的参数是虚拟dom对象和要插入在哪个节点内
//render是渲染用的函数
```