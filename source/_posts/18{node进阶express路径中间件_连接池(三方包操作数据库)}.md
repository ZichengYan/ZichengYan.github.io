 ---
 title: node 入门11
 date: 2016-10-20 22:00:00
 tags: node
 ---

###1.1数据库与数据库管理系统
###1.2数据库中的表
###1.3sql语句insert、update、delete
###1.4sql语句简单的select和带条件的查询
###1.5关系型数据库 有行列表结构的传统的数据库
###1.6no sql 数据库 
 - 内存数据库 redis
 - 文档型数据库 mongodb
#2.express进阶
###2.1express项目构建
- express工具全局安装 npm install -g express-
- express 命令的使用 -h 通过帮助命令查看
- 初始化一个项目名称叫demo的项目并且在项目中加入handlbars模板引擎的支持
  express --hbs demo
- 在一个已经进行项目命名的文件夹里面初始化项目
  express --hbs 
###2.1express项目结构
- bin目录 存放脚本文件
- models 存在模型文件
- node_modules 
- public 静态文件
- routes 路由&控制层
- views 视图(存放模板文件)

###2.2脚本文件的执行，与命令行工具的开发
- bin 中www文件是一个脚本文件
- 写一个node脚本只需要在文件一开始写上-->#!/usr/bin/env node
  这句话的意义是这个文件使用node进行运行
- 两种方式调用脚本
  +第一种使用npm进行文件调用
  1.在package.json中设置scripts
  `"scripts": {
    "start": "node ./bin/www"
  }`
  2.在这包的目录中打npm start命令
  +第二种编写一个全局安装的命令行工具
  1.在package.json中设置bin
  `"bin":{
    "haha":"./bin/www"
  }`
  2.是用npm link命令将写好的代码安装到全局
    和npm install -g 区别
  3. 在控制台打haha可以执行./bin/www脚本


#3.express的路径中间件
###3.1为什么需要路由中间件？
1.项目分工
2.提高可读性
3.对比起没有用路由中间件的写法代码更优雅了
###3.2路径中间件的使用
- 在早期的express中没有路由中间件。
- 在express早起版本将代码拆分模块的写法
  1.在routes创建一个user.js，用于user模块代码的编写
  `module.exports = function(app) {
    app.get('/getUser',function  (req,res) {
  		res.send("{success:true}");
    } );
  }`
  2.在app.js中引入这个模块
  var user = require('./routes/user');
  3.启用这个模块里面的路由 
  user(app);
- 使用路由中间件
  1.在routes创建一个user.js，用于user模块代码的编写
```
  var express = require('express');
  var router = express.Router();
  router.get('/getUser', function(req, res) {
     res.send("{success:true}");
  });
  module.exports = router;
  ```
  2.在app.js中引入这个模块
 ` var user = require('./routes/user');`
  3.启用这个模块里面的路由 
  `app.use('/', user);`

#4. express 连接mysql数据库
###4.1 什么是连接池？
连接池是创建和管理一个连接的缓冲池的技术，这些连接准备好被任何需要它们的线程使用。
和线程池很像。
- 减少连接创建时间
- 简化的编程模式
- 受控的资源使用
###4.3使用第三方的mysql的包操作数据库
- https://github.com/mysqljs/mysql
- 创建一个线程池连接数据库

```
'use strict';

const mysql = require('mysql');

const pool  = mysql.createPool({
    host : 'you host',
    user : 'user1',
    password : '123456',
    database : 'itcast'
});

```

```
/**
 * [query description]
 * @return {[type]} [description]
 */
// 如果用户传递了两个参数，那么第一个就是 SQL 操作字符串， 第二个就是回调函数
// 如果是三个参数：第一个SQL字符串，第二个数组，第三个参数回调函数
exports.query = function() {
    let args = arguments;
    let sqlStr = args[0];
    let params = [];
    let callback;

    if (args.length === 2 && typeof args[1] === 'function') {
        callback = args[1];
    } else if (args.length === 3 && Array.isArray(args[1]) && typeof args[2] === 'function') {
        params = args[1];
        callback = args[2];
    } else {
        throw new Error('参数个数不匹配');
    }

    pool.getConnection(function(err, connection) {
        if (err) {
            callback(err);
        }
        connection.query(sqlStr, params, function(err, rows) {
            if (err) {
                callback(err);
            }
            connection.release();
            callback.apply(null, arguments);
        });
    });
};
```
- model的编写
```
var db = require('./db.js');
function User(user) {
	this.username = user.username;
	this.password = user.password;
}
User.getUserbyUsername = function (username,callback) {
	var selectSql = 'select * from user where user_name = ?';
	db.query(selectSql, [username], function (err, res) {

		console.log(res);
		callback(err,res);
	});

};
module.exports = User;
```
- 路由中的调用方法
```
  var express = require('express');
 var user = require('./models/user.js');
  var router = express.Router();
  router.get('/getUser', function(req, res) {
    user.getUserbyUsername(function(err,data){
            if (err) {
                res.send("{error:true}");
            }
            res.send("{success:true}");
        });

  });
  module.exports = router;

```