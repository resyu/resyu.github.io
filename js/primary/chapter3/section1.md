
>**Q**
>
>如何准确判断一个变量是数组类型
>
>写一个原型链继承的例子
>
>描述new一个对象的过程
>
>zepto(或其他框架)源码中如何使用原型链
>

**【原型和原型链】**
*知识点：*
**构造函数**

- 首字母大写
```js
function Foo(name,age){
  this.name=name
  this.age=age
  this.class='class-1'
  // return this //默认有这一行
}
var f=new Foo('z',20)
// var f1=new Foo('l',19) //创建对象
```
**构造函数 - 扩展**
- var a={} 其实是var a=new Object()的语法糖
- var a=[] 其实是var a=new Array()的语法糖
- function Foo(){} 其实是var Foo=new Function()的一个过程
- 使用instanceof判断一个函数是否是一个变量的构造函数

**原型规则和示例**

```js
var obj={};obj.a=100
var arr=[];arr.a=100
function fn(){}
fn.a=100

console.log(obj.__proto__)
console.log(arr.__proto__)
console.log(fn.__proto__)

console.log(fn.prototype)

console.log(obj.__proto__===Object.prototype)
```
- 所有的引用类型（数组、对象、函数），都具有对象特性，即可自由扩展属性（除了‘null’以外）

- 所有的引用类型（数组、对象、函数），都具有__proto__属性，属性值是一个普通的对象（除了‘null’以外）

- 所有的函数，都有一个prototype属性，属性值也是一个普通的对象

- 所有的引用类型（数组、对象、函数），__proto__属性值指向它的构造函数的‘prototype’属性值

- 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的__proto__（即它的构造函数的prototype）中寻找

```js
//构造函数
function Foo(name,age){
  this.name=name
}
Foo.prototype.alertName=function(){
  alert(this.name)
}
//创建实例
var f=new Foo('z')
f.printName=function(){
  console.log(this.name)
}
f.printName()
f.alertName()

//遍历对象的属性
var item
for(item in f){
  //高级浏览器已经在for in 中屏蔽了来自原型的属性
  //但是还是建议加上这个判断保证健壮
  if(f.hasOwnProperty(item)){
    console.log(item)
  }
}
```

**原型链**
```js
//构造函数
function Foo(name,age){
  this.name=name
}
Foo.prototype.alertName=function(){
  alert(this.name)
}
//创建实例
var f=new Foo('z')
f.printName=function(){
  console.log(this.name)
}
f.printName()
f.alertName()
f.toString()//在f.__proto__.__proto__中去找
```
![原型链](proto.jpg)
**instanceof**
- 判断一个引用是否属于某构造函数
>
>**A**
>

**如何准确判断一个变量是数组类型**

- 使用instanceof判断
```js
var arr=[]
arr instanceof Array //true
typeof arr //object, typeof无法判断是否是数组
```
**写一个原型链继承的例子**
```js
//一个常见的例子 不推荐
function Animal(){
  this.eat=function(){
    console.log('animal eat')
  }
}
function Dog(){
  this.bark=function(){
    console.log('dog bark')
  }
}
Dog.prototype=new Animal()
var hashiqi=new Dog()

//封装一个dom查询 推荐
function Elem(id){
  this.elem=document.getElementById(id)
}

Elem.prototype.html=function(val){
  var elem=this.elem
  if(val){
    elem.innerHTML=val
    return this
  }else{
    return elem.innerHTML
  }
}

Elem.prototype.on=function(type,fn){
  var elem=this.elem
  elem.addEventListener(type,fn)
  return this
}

var div1=new Elem('div1')
div1.html('<p>txt</p>').on('click',function(){
  console.log('clicked')
}).html('<p>change</p>')
```

**描述new一个对象的过程**
- 首先new一个对象的时候，构造函数里的this会变成空对象（有参数的时候会对this进行赋值，然后把this给return出去）

1. 创建一个新对象
2. this指向这个新对象
3. 执行代码，即对this赋值
4. 返回this

**zepto(或其他框架)源码中如何使用原型链**
