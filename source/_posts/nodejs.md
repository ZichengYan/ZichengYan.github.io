---
title: nodejs
date: 2017-01-15 21:10:30
tags: nodejs
---

### 其特点为
 
- 它是一个Javascript运行环境
- 依赖于Chrome V8引擎进行代码解释
- 事件驱动
- 非阻塞I/O
- 轻量、可伸缩，适于实时数据交互应用
- 单线程
 
 
### 优缺点
- 优点
   + 高并发
   + I/O密集型应用
   + 为网络服务而设计(微服务SOA)
- 缺点(原因单线程,单进程)
   + 只支持单核CPU，不能充分利用CPU
   + 可靠性低，一旦代码某个环节崩溃，整个系统都崩溃
   + 解决方案:1.Nnigx反向代理，负载均衡，开多个进程，绑定多个端口;2.开多个进程监听同一个端口，使用cluster模块;
   + 开源组件库质量参差不齐，更新快，向下不兼容
   + Debug不方便
 
### 微服务
- Nnigx做负载均衡,将一个网站划分为多个服务(当某个服务压力大的时候就加服务器,各个服务之间可以相互通信),例如:
    + 登录服务
    + 用户信息服务
    + 购物服务
- 问题如何处理在为服务中氢气失败的情况,
    + 比如在一次购买物品的请求中有如下请求, 服务1请求付款,向服务2发送请求,如果失败怎么办 , 回滚吗,

### __dirname   & __filename
- __dirname 当前文件所在文件夹路径

- __filename 当期那文件所在文件件路径+文件名


### require加载流程
- 
 


### fs模块
- `var stat = fs.statSync(filename); console.log(stat)`
```
/ / ，其中atime，mtime，ctime就分别代表了访问时间，修改时间以及创建时间，都为date类型
{ dev: 0,
  ino: 0,
  mode: 33206,
  nlink: 1,
  uid: 0,
  gid: 0,
  rdev: 0,
  size: 1747,
  atime: Tue, 03 Jan 2012 13:35:51 GMT,
  mtime: Tue, 03 Jan 2012 13:35:51 GMT,
  ctime: Wed, 21 Dec 2011 14:31:59 GMT }
来源： http://www.cnblogs.com/xiziyin/archive/2012/01/04/2312498.html

```

### 路由 Router

```
app.use( '/index',routes);
/index是从端口号之后开始截取
```


### request请求
- 在使用request向另一台服务器发送请求的时候需要西那些全路径 , 因为端口不一样

- 请求端
```
// 像这样去请求 , 需要加上http的协议头 , 因为不是用当期服务发送的请求 , 
// 若当期那服务为9000端口 , 如果想请求8000端口资源只发送 /token请求会默认拼接为127.0.0.1:9000/token,
// 所以根本请求不到

const http = require('http');
const request = require('request');
const server = http.createServer((req2, res2) => {
	console.log(req2.url);
    var postData = 'package.json'
    var options = {
        uri: 'http://127.0.0.1',
        port: 8000,
        path: '/upload',
        method: 'GET'
    };
 	request('http://127.0.0.1:8000/token',function (error, response, body) {
 		 console.log('response : ',response)
 		 console.log(error)
 		 res2.end(postData)
 	})
    
});

server.listen(5000);
console.log('app3.js , listen  5000')

```
 - 服务端
```
const http = require('http');

const server = http.createServer((req, res) => {
	console.log(req.url)
    res.end('80001111');
});

server.listen(8000);


```


### 关于根路径

- 服务端请求路径为 `/token` ; 客户端请求路径为 ` 127.0.0.1:3000/token`
- 那么服务端打印请求路径为` / `


- 服务端请求路径为 `/token` ; 客户端请求路径为 ` 127.0.0.1:3000/token/app`
- 那么服务端打印请求路径为` /app `

- 服务端请求路径为 `/` ; 客户端请求路径为 ` 127.0.0.1:3000/token`
- 那么服务端打印请求路径为` /token  `

- 总结 :  服务端与客户端请求路径匹配到的为根路径 ` / `


### node服务相互请求
- 两侧都是用的是express框架
  - 两侧为原生nodejs

 
 
- 左侧为原生 , 右侧为 request包

 