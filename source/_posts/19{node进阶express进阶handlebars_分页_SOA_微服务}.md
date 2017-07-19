
### 分页接口的设计
1.数据库如何做分页查询
使用limit去做分页查询
limit后面跟两个数字，数字中间用逗号分隔，第一个数字是开始位数，开始位数，从0开始
，也就是说第一条数据的位置为0，第二个数字是取多少条数据
select * from user  limit 0,10
分页返回前端的数据
1.开始位置0，总条数（总页数）
2.页码，总条数（总页数）
总页数=（总条数/每页条数）+1
开始位置=页码*每页条数


计算总条数使用COUNT
SELECT COUNT(*) FROM  USER

#服务器请求服务器
request 
1.可以理解为http里面request方法
2.request第三方包

#2.项目设计
### 2.1SOA（面向服务的体系结构）
- 面向服务的体系结构（SOA）是一个组件模型，它将应用程序的不同功能单元（称为服务）通过这些服务之间定义良好的接口和契约联系起来。接口是采用中立的方式进行定义的，它应该独立于实现服务的硬件平台、操作系统和编程语言。这使得构建在各种这样的系统中的服务可以以一种统一和通用的方式进行交互。
### 2.2服务器之间交互
## 2.3 微服务思想
#3.
###3.1cookie-parser
`https://github.com/expressjs/cookie-parser`
###3.2cookie-session
`https://github.com/expressjs/cookie-session`
###3.3 express-session
`https://github.com/expressjs/session`
###3.3 connect-flash
`https://www.npmjs.com/package/connect-flash`
###3.4 参考
`http://blog.modulus.io/nodejs-and-express-sessions`
#4.handlebars
### 4.1handlebars介绍
`http://handlebarsjs.com/`
### 4.2handlebars使用
`https://github.com/ericf/express-handlebars`
