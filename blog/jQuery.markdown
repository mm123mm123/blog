# jQuery设计思想
## 如何获取元素
使用jQuery的第一步往往就是获取网页的元素，方法就是在构造函数jQuery()（jQuery语法将这个构造函数简写为 $ ）中，放入选择表达式，
然后就可以得到被选中的元素。
```javaScript
$(document) //选择整个文档对象
$('#myId') //选择ID为myIdD的网页元素
$('div.myClass') //选择class为myClass的div元素
```
## 链式操作
在第一步获取元素之后，我们可以通过链式操作对元素进行修改
```javaScript
$('div')
.find('.red') //找到class为red的元素
.addClass('circle') //为元素的class添加一个名字叫circle
```
链式操作的原理是，每次函数调用返回的对象可以继续调用这个对象内部的函数，对所找到的元素进行连续的操作
## 创建，删除元素
```javaScript
$('<div>你好</div>') //创建一个div元素，内容为你好
$('div.blue').remove()  //将所class为blue的div元素删除
$('div.blue').empty() //将class为blue的div元素里的内容清空
```
## 移动元素
```javaScript
$('div').insertAfter($('p')) //把div元素移动到p元素的后面，返回div元素
$('p').after($('div'))  //把p元素放在div元素的前面，返回p元素
```
类似这种模式的操作方法总共有四对：
```javaScript
.insertAfter()和.after() //在现存元素的外部，从后面插入元素
.insertBefore()和.before() //在现存元素的外部，从前面插入元素
.appendTo()和.append() //在现存元素的内部，从后面插入元素
.prependTo()和.prepend() //在现存元素的内部，从前面插入元素
```
## 元素的取值和赋值
这里用到的设计模式是getter和setter，即'取值器''赋值器'合一，是取值还是赋值，是由函数的参数决定的
```javaScript
$('h1').html(); //html()没有参数，表示取出h1的值
$('h1').html('Hi'); //html()有参数Hi，表示对h1进行赋值
.html() 取出或设置html内容
.text() 取出或设置text内容
.attr() 取出或设置某个属性的值
.width() 取出或设置某个元素的宽度
.height() 取出或设置某个元素的高度
.val() 取出某个表单元素的值
```
