---
title: es6
date: 2016-05-15 21:10:30
tags: es6
---

### 箭头函数
- `()=>{}`
-其中的this会指向其所在环境的父级环境
 
### let
- 块级作用域每次循环都会创建一个作用域
 
```
for (var i = 0; i < 5; i++) {
    setTimeout(function() {
        console.log("这是var打印的数据" + i);
    }, 1000);
}
 
 
for (let j = 0; j < 5; j++) {
    setTimeout(function() {
        console.log("这是let打印的数据" + j);
    }, 1000);
}
 
 
 
//因为每循环一次就会生成一个局部作用域,每个par都保存了当前的i
for (var k = 0; k < 5; k++) {
    (function() {
        var par = k;
        setTimeout(function() {
            console.log("这是闭包打印的数据"+par);
        }, 1000);
    })();
}
 
```
 
### const
- 定义常量(定以后不能修改)
 
 
### import ...  from ... & exports default ...
 
```
//引入模块的方式,前面是变量,后面是包名
import http from 'http'
 
//暴露模块的方式
export default function () {
  console.log('foo');
}
 
```
 
### Class
- 定义类

 