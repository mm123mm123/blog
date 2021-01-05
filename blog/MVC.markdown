# 浅谈MVC
## MVC三个对象分别做什么
```
//示例
let Model={
    data:{//数据源},
    create:{//增加数据},
    delete:{//删除数据},
    update(data){
        Object.assign(m.data,data)//用新数据替换旧数据
        eventBus.trigger('m:update')//eventBus触发'm:update'信息，通知View刷新界面
    },
    get:{获取数据}
}
```
M - model（模型）：模型model用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法，会有一个或多个视图监听此模型。一旦模型的数据发生变化，模型将通知有关的视图。
```
//示例
let View={
    el://要刷新的元素，
    html：//'要显示在页面上的内容'
    init(){
        v.el://需要刷新的元素
    }，
    render(){
        //重新渲染页面
    }
}
```
V - view（试图）：视图view是它在屏幕上的表示，描绘的是model的当前状态。当模型的数据发生变化，视图相应地得到刷新自己的机会
```
//示例
let Controller={
    init(){
        v.init()//初始化View
        v.render()//第一次渲染页面
        c.autoBindEvents()//自动的事件绑定
        eventBus.on('m:update',()=>{v.render()}//当enentsBus触发'm:update'是View刷新
    }，
    events:{//事件以哈希表的方式记录存储},
    method(){
        data=//新数据
        m.update(data)
    },
    autoBindEvents(){//自动绑定事件}
}
```
C - controller（控制器）：控制器controller定义用户界面对用户输入的响应方式，起到不同层面间的组织作用，用于控制应用程序的流程，它处理用户的行为和数据model上的改变

## EventBus有哪些API,是做什么用的
```
const eventBus = $(window)
const model = {
    data: {
        //数据
    },
    update(data) {
        eventBus.trigger('m:updated')    //触发数据的更新
        localStorage.setItem('n', m.data.n.toString()) //将更新的数据存到本地
    }
}

const Controll = {
    //更新数据的方法
    eventBus.on('m:updated', () => {
             //渲染更新的数据
        })   //监听数据更新
}
```
常用的API有on,trigger,off,如代码所示，trigger用来触发事件，当数据改变时候，执行该函数，之后on函数会
监听到这个触发动作，从而调用相应的函数，对数据的更改做出响应。off函数用于取消监听。

## 表驱动编程
```
const c = {
    events: {    //哈希表
        'click #add1':'add',
        'click #minus1':'minus',
        'click #mul2':'mul',
        'click #divide2':'divide'
    },
    add() {
        m.update({n:m.data.n += 1})
    },
    minus() {
        m.update({n:m.data.n -= 1})
    },
    mul() {
        m.update({n:m.data.n *= 2})
    },
    divide() {
        m.update({n:m.data.n /= 2})
    },
    autoBindEvents(){
        for(let key in c.events){
            const value = c[c.events[key]]
            const spaceIndex = key.indexOf(' ')
            const part1 = key.slice(0,spaceIndex)
            const part2 = key.slice(spaceIndex+1)
            v.el.on(part1,part2,value)  //通过遍历哈希表监听事件
        }
    }
}
```
表驱动的关键在于，我们将变化的参数放置在一个表中，通过for循环遍历表格的方式，将参数传入函数中来执行
不同的任务，这样做的优点是，大大减少了代码重复，提高了代码的可读性和复用性。

## 模块化编程
网页越来越像桌面程序，需要一个团队分工协作、进度管理、单元测试等等......开发者不得不使用软件工程的方法，管理网页的业务逻辑。
Javascript模块化编程，已经成为一个迫切的需求。理想情况下，开发者只需要实现核心的业务逻辑，其他都可以加载别人已经写好的模块。
### 原始写法
```
function m1(){
　　　　//...
　　}

　　function m2(){
　　　　//...
　　}
```
上面的函数m1()和m2()，组成一个模块。使用的时候，直接调用就行了。
这种做法的缺点很明显："污染"了全局变量，无法保证不与其他模块发生变量名冲突，而且模块成员之间看不出直接关系
### 对象写法
```
var module1 = new Object({

　　　　_count : 0,

　　　　m1 : function (){
　　　　　　//...
　　　　},

　　　　m2 : function (){
　　　　　　//...
　　　　}

　　});
```
为了解决上面的缺点，可以把模块写成一个对象，所有的模块成员都放到这个对象里面。上面的函数m1()和m2(），都封装在module1对象里。使用的时候，就是调用这个对象的属性。

### 类写法
```
Class Module{
  constructor(count){
    this._count=count
  }
  m1(){
　　　　　　//...
　　　　},

　m2 (){
　　　　　　//...
　　　　}
}
```
当我们建立多个对象，并且发现某些对象使用了一些重复的函数和属性，这时我们可以通过建立类来构造这些对象，我们还可通过类的继承，来继承其他类的方法。



我们主要是通过面向对象的思想以及MVC框架，将各种属性和函数，放入MVC对象之中，形成三个大模块，然后通过建立类，将对象再一次简化，模块化编程是非常重要的一种编程模式，优势如下：多人协作互不干扰模块化避免了变量污染，并且可以使得分工更加容易灵活架构，焦点分离可以将独立的功能从主干中分离开来单独开发，增加效率
方便模块间组合、分解 、解耦降低各个功能模块间的耦合度，方便维护和管理方便单个模块功能调试、升级
