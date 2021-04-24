---
title: JavaScript this指针
tags: 
    - JavaScript
    - 前端
cover: https://coderhch.oss-cn-shanghai.aliyuncs.com/blog/2021-04-17/JavaScript_this%E6%8C%87%E9%92%88/1.jpg
date: 2021-04-17
---
#	JavaScript this指针

this表示函数的上下文，用一个函数，用不同的方式调用它，则函数的上下文不同。

###	举例

1. **对象打点调它的方法函数，则函数的上下文是这个打点的对象**

```javascript
var obj={
      a:1,
      b:2,
      fun:function(){
        console.log(this.a+this.b) //3
        console.log(this === obj) //true  
      }
    }
    obj.fun()
```

这里函数是obj对象打点调用的，所以这里的this指的就是obj对象

2. **圆括号直接调用函数，则函数的上下文是window对象**

```javascript
var obj={
      a:1,
      b:2,
      fun:function(){
        console.log(this.a+this.b) //NaN
        console.log(this ===window) //true
      }
    }
    var fun = obj.fun
    fun()
```

这里不是对象打点调用的，这里是obj将函数赋值给了一个新变量，然后在加上"()"调用，所以这个里this指代window对象

3. **数组（类数组对象）枚举出函数进行调用，上下文是这个数组（类数组对象）**

```javascript
	var arr=['A','B','C',function(){
      console.log(this[0]) //A
    }]
    arr[3]();
```

4. **IIFE中的函数，上下文是window对象**

```javascript
var a=1;
    var obj={
      a:2,
      fun:(function(){
        var a=this.a;
          return function(){
            console.log(a+this.a) //3
          }
      })()
    }
    obj.fun()
```

由于fun函数是IIFE，所以`var a=this.a`就等于`var a=1`，IIFE返回一个函数，而这个函数是obj对象打点调用的，所以`a+this.a`等于`a+2` ,所以输出3

5. **定时器，延时器调用对象，上下文是window对象**

```javascript
    var obj={
      a:1,
      b:2,
      fun:function(){
        console.log(this.a+this.b) //7
      }
    }
    var a=3;
    var b=4;
    setTimeout(obj.fun,2000)
```

6. **事件处理函数的上下文是绑定事件的DOM元素**

这里我们做一个小案例：点击哪个盒子，哪个盒子就变红，要求使用同一个事件处理函数实现

```html
 <div id="box1"></div>
  <div id="box2"></div>
  <div id="box3"></div>
```

```css
	div{
      width: 200px;
      height: 200px;
      float: left;
      border: 1px solid black;
      margin-left: 10px;
    }
```

```javascript
 function changeColor(){
      this.style.backgroundColor='red';
    }

    var box1 = document.getElementById("box1")
    var box2 = document.getElementById("box2")
    var box3 = document.getElementById("box3")
    
    box1.onclick = changeColor
    box2.onclick = changeColor
    box3.onclick = changeColor
```

###	指定上下文

call和apply函数可以指定上下文

**案例**

```javascript
function sum(){
      console.log(this.c +this.m +this.e)
    }
    var xiaoming={
      c:100,
      m:20,
      e:80
    }
    sum.apply(xiaoming) //200
    sum.call(xiaoming) //200
```

####	call和apply的区别

```javascript
function sum(b1,b2){
      console.log(this.c +this.m +this.e+b1+b2)
    }
    var xiaoming={
      c:100,
      m:20,
      e:80
    }
    sum.apply(xiaoming,[100,100]) //200
    sum.call(xiaoming,100,100) //200
```

我们可以看到，当sum方法有参数时，apply和call传递参数的方式上不一样，call是依次书写参数而apply是将参数放在数组里传递的

###	上下文规则总结

| 规则            | 上下文        |
| --------------- | ------------- |
| 对象.函数()     | 对象          |
| 函数()          | window        |
| `数组[下标]()`  | 数组          |
| IIFE            | window        |
| 定时器          | window        |
| DOM事件处理函数 | 绑定DOM的元素 |
| call和apply     | 任意指定      |

