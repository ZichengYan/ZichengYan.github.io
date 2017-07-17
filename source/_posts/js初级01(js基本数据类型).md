---
title: js初级01(js基本数据类型)
date: 2013-09-15 22:14:37
tags: javascript 初级
---

## JavaScript 基本组成
 
- JavaScript由几部分构成？
> ECMAScript、DOM、BOM
 
## 数据类型
 
#### 数据类型有哪些？
 
- 基本数据类型
number、string、boolean、null、undefined
 
- 复杂数据类型
object
 
#### ECMAScript内置对象有哪些？
- Array、Math、Date、Object、String、Number、Boolean、Function、Error、RegExp
 
#### 如何判断数据类型？
- typeof
- typeof无法判断null类型的数据，反过来说typeof判断object类型的数据可能存在误判
- typeof可以判断Function类型的对象
 
## 基本类型与引用类型的赋值问题
 
#### 基本类型
- 赋的是具体的值
 
#### 引用类型
- 赋的是对象的地址
 
## 运算符
 
#### 算术运算符 + %
- 算术运算、字符串连接、把数据类型转换为number
- 取余数
 
#### 逻辑运算符 && || !
- && 从左往右依次把数据转换为boolean类型，如果是false，则返回对应的数据；
如果一直没有找到，则返回最后一个数据。
- || 从左往右依次把数据转换为boolean类型，如果是true，则返回对应的数据；
如果一直没有找到，则返回最后一个数据。
- ! 把数据转换为boolean类型，然后取反
 
#### 相等运算符 == === != !==
- === 类型与值必须全等
- == 会先进行数据类型转换，然后比较（具体转换规则，下面有。）
 
#### 三元运算符 ? :
- 问号前面的表达式结果为true，执行冒号前的表达式，否则执行后面的表达式。
 
## 布尔类型转换
 
#### 如何把数据转换为布尔类型？
- !! Boolean
 
#### 哪些数据在转换为布尔类型时结果为false？
- 0、undefined、null、NaN、''
- 所有的对象转换后为boolean类型，都为true
 
## 语句
 
#### 分支语句
- if else、switch case
 
#### 循环语句
- for、while、do while、for in
 
#### break和continue的作用是什么？
- break：结束循环。
- continue：跳出当前循环，继续下一次循环
 
## 函数
 
#### 创建方式
- 函数声明式
- 函数表达式
- Function
 
#### 参数
- 对函数中重复执行代码中的不同部分的抽象提取
- 形参是用来接收实参传递过来的值。
- 练习：写一个函数，函数接收一个参数并打印，如果参数的值是null或undefined，则不打印。
 
#### 返回值
- 如果没有return语句，则为undefined，如果有则为对应的值。
 
#### arguments
- arguments是一个代表实参的对象，
- 可以通过下标的方式获取实参，
- 可以通过length属性获取实参的个数
 
#### this
- 谁调用就指向谁。
 
#### 错误抛出
- throw 自定义抛出错误。
 
## debugger与断点
 
# +号
- 如果两边含有字符串或者对象，那么转换为string之后再相加
- 除此之外，两数相加，转换为number之后再相加
 
# -号
- 把两边数据转换为number之后再相减
 
# ==运算符比较规则
> 约定：非空数据类型表示除null和undefined两种数据类型。
 
- 任何数据和NaN相比结果都为false
- null等于undefined
- null和非空类型相比结果为false
- undefined和非空类型相比结果为false
- 数字和非空类型比较，先转换为数字再比较
- 布尔和非空类型比较，先转换为数字再比较
- 对象与对象比较内存地址
- 对象与字符串，对象先转换为字符串再比较
 
类型 | 类型 | 规律
---|---|---
NaN | 任意类型 | false
null | undefined | true
null | 非空类型 | false
undefined | 非空类型 | false
数字 | 非空类型 | 转换为数字再比较
布尔 | 非空类型 | 转换为数字再比较
对象 | 对象 | 内存地址比较
对象 | 字符串 | 转换为字符串再比较
