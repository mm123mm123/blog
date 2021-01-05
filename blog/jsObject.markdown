# JS对象
## 声明对象的两种方式
`let obj={'name':'frank','age':18}`

`let obj=new Object({'name':'frank'})`
## 如何删除对象的属性
`delete obj.xxx`

`delete obj['xxx']`
## 如何查看对象属性
+ 查看自身所有属性

`Object.keys(obj)`
+ 查看自身以及共有属性

`console.dir(obj)`
+ 判断一个属性是自身的还是共有的

`obj.hasOwnProperty('toString')`
## 如何修改或者增加对象的属性
+ 改自身 `obj['name']='jack'`
+ 批量改自身 `Object.assign(obj,{age:18,...})`
+ 改共有属性 `Object.prototype['toString']='xxx'`
+ 改原型 `let obj=Object.create(common)`

增加属性也是使用这些方法，就是添加对象本身还没有的属性
## 'name' in obj和obj.hasOwnProperty('name')的区别
前者判断这个对象是不是拥有该属性，后者是判断这个属性是不是对象自己拥有而非公有的