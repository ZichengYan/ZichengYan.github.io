---
 title: node 入门01
 date: 2016-10-02 22:00:00
 tags: node
---

 
#1.模型对象化
- 不只是方法，而是曝露完整的对象，用对象的方式在层之间传递

```
function User(user) {
	this.id=user.id;
  ...
};
```
- 添加方法
`User.addUser= function () {};`
- 曝露方法
`module.exports = User;`
#2.express进阶

###2.1express的中间件morgan

```
https://github.com/expressjs/morgan#url
- morgan 是用来展示http请求的这么一个中间件
var logger = require('morgan');
app.use(logger('dev'));
###2.2express的中间件body-parser
bodyParser用于解析客户端请求的body中的内容,内部使用JSON编码处理,url编码处理.
var bodyParser = require('body-parser');
//解析json
app.use(bodyParser.json()); // for parsing application/json 
//解析表单传输的数据
app.use(bodyParser.urlencoded({ extended: true })); // for parsing application/x-www-form-urlencoded
app.post('/', function (req, res) {
  console.log(req.body);
  res.json(req.body);
})
```

###2.3 req取参数的3种方法

```
expressjs里的请求参数，4.x里只有3种
req.params
req.body
req.query
已经废弃的api
req.param(Deprecated. Use either req.params, req.body or req.query, as applicable.)
- 2.3.1. req.params
//用get请求传输过来的参数
app.get('/user/:id', function(req, res){
  res.send('user ' + req.params.id);
});
俗点：取带冒号的参数
```

- 2.3.2. req.body

```
可以肯定的一点是req.body一定是post请求，express里依赖的中间件必须有bodyParser，不然req.body是没有的。
- 2.3.3. req.query

query是querystring

说明req.query不一定是get

// GET /search?q=tobi+ferret
req.query.q
// => "tobi ferret"

// GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse
req.query.order
// => "desc"

req.query.shoe.color
// => "blue"

req.query.shoe.type
// => "converse"
因为有变态的写法

// POST /search?q=tobi+ferret
{a:1,b:2}
req.query.q
// => "tobi ferret"
post里看不的，用req.body取。

```

#3.RESTful
### RESTful是什么？
- 一种软件架构风格，设计风格而不是标准，只是提供了一组设计原则和约束条件。
它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。
- GET /user  获取user信息列表
  GET /user/17  查看id为17的具体的user信息
  POST /user    新建一个user
  PUT /user/17  更新id为17的user信息
  DELETE /user/17 删除id为17的user信息
### 历史
REST这个词，是Roy Thomas Fielding在他2000年的博士论文中提出的。
Fielding是一个非常重要的人，他是HTTP协议（1.0版和1.1版）的主要设计者、Apache服务器软件的作者之一、Apache基金会的第一任主席。
所以，他的这篇论文一经发表，就引起了关注，并且立即对互联网开发产生了深远的影响。
Fielding将他对互联网软件的架构原则，定名为REST，即Representational State Transfer的缩写。我对这个词组的翻译是"表现层状态转化"。
如果一个架构符合REST原则，就称它为RESTful架构。
约定俗成由于配置
#4 基于cookie与session的登录模块
### session cookie配合使用

```
app.use(session({
       secret: 'itcast-secret',
       name: 'itcast-name',
       cookie: {maxAge: 8000000000 },
       resave: false,
       saveUninitialized: true,
}));

```
- secret:用于对sessionID的cookie进行签名，可以是一个string(一个secret)或者数组(多个secret)。
如果指定了一个数组那么只会用 第一个元素对sessionID的cookie进行签名，其他的用于验证请求中的签名。
- resave : 是指每次请求都重新设置session cookie，假设你的cookie是10分钟过期，每次请求都会再设置10分钟
- saveUninitialized: 是指无论有没有session cookie，每次请求都设置个session cookie ，默认给个标示为 connect.sid
req.session.属性添加
### express-session配置项详解

```
http://blog.csdn.net/liangklfang/article/details/50998959

//共用代码的编写
router.get('/news',function(req,res,next){
     if (!req.session.user) {
         return res.redirect('/login.html');
     }
    next();
})
router.get('/news',function(req,res,next){
      
	//res.send('给你新闻页面');
	//页面跳转
	res.redirect('/news.html');
})

```