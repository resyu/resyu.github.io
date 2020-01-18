> 
>**Q**
> 
>说一下对变量提示的理解
>
>说明this几种不同的使用场景
>
>如何理解作用域
>
>实际开发中闭包的应用 
>
*知识点*

**执行上下文**

- 范围：一段'<'script'>'（全局上下文）、或者一个函数（函数上下文）
- 全局：变量定义、函数声明（先把这些拿出来放到最前面进行一个占位）
- 函数：变量定义、函数声明、this、arguments（先把这些拿出来放到最前面进行一个占位）

*注意“函数声明”和“函数表达式”的区别*

```js
console.log(a)//undefined
var a=100

fn('zhangsan') //'zhangsan' 20
function fn(name){
  age=20
  console.log(name,age)
  var age
}
```
**this**

- this要在执行时才能确认值，定义时无法确认

```js
var a={
  name:'A',
  fn:function(){
    console.log(this.name)
  }
}
a.fn() //this===a
a.fn.call({name:'B'}) //this==={name:'B'}
var fn1=a.fn
fn1() //this===window
```
**作用域**
**作用域链**
