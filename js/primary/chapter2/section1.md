
>**Q**
>
>js中使用typeof能得到哪些类型？(Tip：js变量类型)
>
>何时使用 === 何时使用 == ？(Tip：强制类型转换)
>
>window.onload和DOMContentLoaded的区别？(Tip：浏览器的渲染过程)
>
>用js创建10个a标签，点击的时候弹出来对应的序号（Tip：变量的作用域）
>
>简述如何实现一个模块加载器，实现类似require.js的基本功能（Tip：js模块化）
>
>实现数组的随机排序（Tip：js基础算法）
>

**【变量类型和计算】**

**变量类型**
- 值类型：字符串、布尔、数值、undefined
```js
var a=100
var b=a
a=200
console.log(b)//100
```
- 引用类型：对象、数组、函数、null
```js
var a={age:20}
var b=a
b.age=21
console.log(a.age)//21
```
- typeof运算符详解
```js
typeof undefined //undefined
typeof 'abc' //string
typeof 13 //number
typeof true //boolean
typeof {} //object
typeof [] //object
typeof null //object
typeof console.log //function
typeof Symbol() //symbol ES6新增类型
```
>对于值类型：typeof可以分出每一个值类型
>对于引用类型：typeof只能分出function，其他认为是object


**计算**

*强制类型转换*
- 字符串拼接
```js
var a=100+10 //110
var b=100+'10' //'10010'
```
*数值与字符串拼接的时候，先把数值转换成了字符串*
- ==运算符
```js
100=='100' //true
0=='' //true
null==undefined //true
```
- if语句
```js
var a=true
if(a){
  //...
}
var b= 100
if(b){
  //... 发生了类型转换
}
var c=''
if(c){
  //... 发生了类型转换
}
```
- 逻辑运算
```js
console.log(10&&0) //0 10强制类型转换成false
console.log(''||'abc') //'abc' ''强制类型转换成false
console.log(' '||'abc')//' ' ' '强制类型转换成true
console.log(!window.abc)//true window.abc为undefined取反为true
//!!判断一个变量会被当做true还是false
var a=100
console.log(!!a)
```
**js中有哪些内置函数—数据封装类对象**
- Object
- Array
- Boolean
- Number
- String
- Function
- Date
- RegExp
- Error

**js变量按照存储方式区分为哪些类型，并描述其特点**
- 值类型
- 引用类型
*减少内存开销*

**如何理解json**

- json是一种格式规范，在js中可以看作是一个对象
- JSON.parse() //string转成json对象
- JSON.stringify() //json对象转成string

>**A**

**js中使用typeof能得到哪些类型？(Tip：js变量类型)**
- boolean、string、number、object、undefined、function、symbol
- 拓展：变量操作

**何时使用 === 何时使用 == ？(Tip：强制类型转换)**

**window.onload和DOMContentLoaded的区别？(Tip：浏览器的渲染过程)**

**用js创建10个a标签，点击的时候弹出来对应的序号（Tip：变量的作用域）**

1.对象属性index
```js
window.onload=function(){
  var aDom=document.getElementsByTagName('a')
  for(var i=0;i<aDom.length;i++){
    aDom[i].index=i
    aDom[i].onclick=function(){
      alert(this.index)
    }
  } 
}
```
2.闭包

**简述如何实现一个模块加载器，实现类似require.js的基本功能（Tip：js模块化）**

**实现数组的随机排序（Tip：js基础算法）**
