 ---
 title: node 入门06
 date: 2016-10-06 22:00:00
 tags: node
 ---
 
 
# es6


```

js--->浏览器-->引擎执行js代码
ie ff chrome
node---->v8执行js代码
node 不考虑兼容性，es6能给我们带来很多好处。
Node.js 6覆盖了93%的ECMAScript 6

```


- [阮一峰es6入门](http://es6.ruanyifeng.com/#README)
###3.4 use strict严格模式


```

消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
　　- 消除代码运行的一些不安全之处，保证代码运行的安全；
　　- 提高编译器效率，增加运行速度；
　　- 为未来新版本的Javascript做好铺垫。

保留字：
一旦出现Unexpected strict mode reserved word这样的错误说明你用保留字做了参数名了。
es6-->implements, interface, let, package, private, protected, public, static, yield
es5-->class, enum, export, extends, import, super

```


 [阮一峰 严格模式](http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html)
 
###3.5 let

在使用let命令声明变量时，一个变量名只能声明一次，不存在命名冲突。
let定义作用域在代码块里,解决命名冲突问题，能体现代码的封装性
变量提示，用let不存在变量提示，会直接报错，告诉你变量没有定义
let命令每次定义的作用域都在本次循环的方法体内

###3.6 const

//定义常量，不会发生变化
//如定义了常量，再去修改就会报错error  Assignment to constant variable 不可以给常量赋值
//const定义的常量，作用域与let相同
//应用场景const用来定义静态变量,加载模块的时候，定义个常量，把模块赋值给常量
###3.7 块级作用域

凡是被{}包裹的代码属于一个代码块
###3.8 字符串的一些扩展

## 4. 文件操作
### 4.1 Buffer

十六进制：0、1、2、3、4、5、6、7、8、9、a、b、c、d、e、f  满16进位 所以 0X10=16
计算机最早诞生的时候，没有中文，在美国

26个英文字母，@ ! , . - + =

计算机只能识别 0 或者 1

把你的字符和计算机真正存储的二进制数据做了一个字典：

可以通过 开源中国 官网网站提供的一个工具页面：http://tool.oschina.net/

随着计算机普及到了世界各地，ASCII 码 已经不能满足世界各地人们的需求了

计算机进入中国之后，后来在原来的 ASCII 码基础之上扩展了一个新的字符集编码：gb2012，
字典 
用来支持中文
字节的转化

1汉字=2字节  00100010 00000000
1字节（Byte)＝8字位＝8个二进制数 
1字位(bit)＝1个二进制数 
1B=8b 
1KB=1024B 
1MB=1024KB 
1GB=1024MB 

#### 4.1.1 创建Buffer



Buffer 是一个像 Array 的对象，它的元素为16进制的两位数（0-255的值），主要用于操作字节，
Buffer 是一个全局对象，使用的时候不需要 require

- new Buffer(size)
- new Buffer(str,[encoding])

#### 4.1.2 Buffer的一些属性和方法


- buf[index] 通过下标访问 buffer 的某个字节的数据
- buf.indexOf(value,[byteOffset],[encoding]) 查找某个字符在 buffer 内存中的字节下标
- buf.includes(value,[byteOffset],[encoding])
- buf.length
- buf.slice([start,[end]])
- buf.toString([encoding],[start], [end])
- buf.write(string,[offset],[length],[encoding])


#### 4.1.3 造成乱码的原因


我们通常所说的编码一般就是指 字符集编码，一般用于字符串

当你把一个 `gbk` 编码文件发送给了你的一个国外友人的时候，
乱码的原因就是：他的机器上没有该编码　

计算机为了让多语言操作系统下可以识别和共享一种编码格式：所以诞生了 超级大字典：`utf-8`

造成乱码的原因其实就是　读取的编码和文件的编码不一致　

要想解决乱码：让文件编码和读取编码统一即可

- 什么是字符集编码
- 为什么要有编码
  + 计算机只能识别二进制
  + 为了让计算机可以识别字符，人类做了一个字典 二进制 -> 字符 的映射关系
- 为什么会产生乱码
  + 文件编码和读取该文件的编码不一致导致的
- 如何解决乱码
  + 让文件和读取的字符编码集一致即可
- 如何解决 Node 原生不支持的一些编码
  + 通过 第三方包：[iconv-lite ](https://www.npmjs.com/package/iconv-lite)
  + 该第三方包可以解决 gbk 等编码不支持的问题
###4.2文件流 

- 流对象 stream
- fs.readFile()和fs.writeFile()问题？
  + 对大文件的处理，例如下载
- 通过文件流的形式传输大文件
    const rs = fs.createReadStream(path1);
    const ws = fs.createWriteStream(path1);
    rs.pipe(ws);
- 控制流

```
const fs = require('fs');
//读文件的流
const rs = fs.createReadStream('1.itcast');


//写文件流
const ws = fs.createWriteStream('./b/234234.itcast');
var stats = fs.statSync('1.itcast');
//stats.size 文件大小
//rs.pipe(ws);

rs.on('data', function(chunk) {
    console.log(chunk.length);
    ws.write(chunk);
})

rs.on('end', function() {
    console.log("读取结束");
    ws.end();
})

```

# 其它

- vsc教程[http://i5ting.github.io/vsc/](vsc教程)
- 装node-inspector
- 读http://es6.ruanyifeng.com/#README
- vsc教程[http://i5ting.github.io/vsc/](vsc教程)

