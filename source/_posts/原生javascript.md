---
title: 原生js
date: 2016-02-24 09:14:37
tags: 原生
---

 ### input : focus (作为事件触发条件)

-  使用 :focus 作为事件触发条件
```
// 当css为
input : focus +div {
            display:block;
}
// 当给上面的 div 注册事件的时候会注册注册上,但是不能触发 ,
因为一旦离开input的框的焦点就会隐藏div , 所以事件不能触发 . 及时代理事件也不能触发
```

### readonly
- 使用 js 给具有readonly 的input文本框赋值,不能触发onchange事件 , 此处要手动触发
- onChange事件是失去焦点的时候才能触发 

### str.replace();

- 替换

```javaScript

 name = 'aaa bbb ccc';
 uw = name.replace(/\b\w+\b/g, function(word) {
    // 将匹配到的字符串传进来 做处理在return 出去 ,
    //  其实与name.replace(/\b\w+\b/g, "新字段"),相同 
      console.log(word)
      console.log(word.substring(0, 1).toUpperCase());
      console.log(word.substring(1))
      return word.substring(0, 1).toUpperCase() + word.substring(1);
  });
  console.log(uw)

```

### void   

- 相关链接 [undefined](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)

-  [ void 运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/void) 对给定的表达式进行求值，然后返回 undefined。 

-   javaScript URIs

```js
<a href="javascript:void(0);">
  这个链接点击之后不会做任何事情，如果去掉 void()，
  点击之后整个页面会被替换成一个字符 0。
</a>

<a href="javascript:void(document.body.style.backgroundColor='green');">
  点击这个链接会让页面背景变成绿色。
</a>
```

- 立即调用函数表达式 
    + 在使用立即执行的函数表达式时，可以利用 void 运算符让 JavaScript 引擎把一个函数识别成函数表达式而不是函数声明（语句）。


```
void function iife() {
    var bar = function () {};
    var baz = function () {};
    var foo = function () {
        bar();
        baz();
     };
    var biz = function () {};

    foo();
    biz();
}();

```

- javascript 
    +  伪协议执行js


```html

// void (0) 只是加了个运算符号() , 避免0 余其他标识符进行运算

void 0 的返回值是 undefined

// 应用环境

// 阻止a 标签跳转
<a href="javascript: void(0);"> </a>  

// 或者写成这样 , 因为阻止a 标签跳转的原因是javascript的运算结果为undefined , 中间是空值;
<a href="javascript: ;"> </a>  
 

```

### typeof 运算符

- 使用 typeof的是它不会在一个变量没有被声明的时候抛出一个错误。

-

```

var x;
if(x === void 0) {
    // 执行这些语句
}

// 没有声明y
if(y === void 0) {
    // 抛出一个RenferenceError错误(与`typeof`相比)
}

```

### setter / getter 

```javescript
 var obj = {
			asd:123,
            val:100,
			name2:2,
            get getval(){
                return this.val;
            },
			get getas(){return this.asd},
            set setval(x){
                this.val = x;
            }
        }

//获取
obj.getval
// 修改
obj.setval="test"

```

### 变量未声明
- 赋值为null

### 命名空间
- 
 
- 弊端
    + 在"严格模式"下必须使用"var";会创建独立作用域;
    + 无论怎么改造都会创建独立作用域.
    + 或者说这个只用来判断作用域是否创建
- 将a.b这样的字符串做分割成数组,没拼接一次转换成js执行一次typeof,如果不存在就创建一个
```
 // 声明一个全局对象nameSpace，用来注册命名空间  
    var nameSpace = new Object();
    // 全局对象仅仅存在register函数，参数为名称空间全路径，如"Grandsoft.GEA"  
    nameSpace.register = function(fullNS) {
        // 将命名空间切成N部分, 比如Grandsoft、GEA等  
        var nsArray = fullNS.split('.');
        var sEval = "";
        var sNS = "";
        for (var i = 0; i < nsArray.length; i++) {
             
            if (i != 0) {
                sNS += ".";
            }
            sNS += nsArray[i];
            // 依次创建构造命名空间对象（假如不存在的话）的语句  
            // 比如先创建Grandsoft，然后创建Grandsoft.GEA，依次下去  
            // consoel.log()中的字符串需要使用单引号在包一层否则执行的时候会报错;
 
 
           sEval += "if (typeof(" + sNS + ") == 'undefined') {" + sNS + " = new Object();}else{console.log('nameSpace--" + sNS + "已存在-------')}";

        }
// sEval最终拼接为
// if (typeof(a) == 'undefined') a = new Object();if (typeof(a.b) == 'undefined') a.b = new Object();
        if (sEval != "") eval(sEval);
    }


    // 注册命名空间Grandsoft.GEA, Grandsoft.GCM  
    nameSpace.register("Grandsoft.GEA");
    nameSpace.register("Grandsoft.GCM");
    // 在Grandsoft.GEA命名空间里面声明类Person  
    Grandsoft.GEA.Person = function(name, age) {
            this.name = name;
            this.age = age;
        }
        // 给类Person添加一个公共方法show()  
    Grandsoft.GEA.Person.prototype.show = function() {
            alert(this.name + " is " + this.age + " years old!");
        }
        // 演示如何使用类Person  
    var p = new Grandsoft.GEA.Person("yanglf", 25);
    p.show();

```


### formData
- 前端上传代码
```html

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <title>exercise</title>
    <script src="https://cdn.staticfile.org/jquery/3.2.1/jquery.min.js"></script>
    <style type="text/css">
    #contents img {
        width: 100px;
        height: 100px;
    }
    </style>
</head>

<body>
    <div id="uploadForm" enctype="multipart/form-data">
        <p id="uploadBox">上传文件：
            <input type="file" name="uploadFile" id="files" multiple="" />
        </p>
        <div id="contents"></div>
    </div>
    <script>
    function doUpload($dom) {
        var formData = new FormData();
        var files = $dom[0].files;
        var dataUrl = null;
        var imgStr = '';
        for (var k = 0; k < files.length; k++) {
            formData.append(k, files[k]);
            console.log(k)
            dataUrl = window.URL.createObjectURL(files[k]);
            imgList += '<img src="' + dataUrl + '" alt="" />';
        }
        $.ajax({
            url: 'http://localhost:8002/upload',
            // url: 'http://wx.bokedata.com/yatou/wechat/common/upload',
            // url: 'http://192.168.0.107:8080/yatou/wechat/common/upload',
            type: 'POST',
            dataType: "JSON",
            data: formData,
            cache: false,
            // headers:{
            //  "Content-Type":"multipart/form-data"
            // }
            contentType: false,
            processData: false,
            context: $dom,
            success: function(data) {
                console.log("成功", data)
                $("#contents").append(imgStr);
            },
            error: function(data) {
                console.log();
                console.log("失败", data)
            },
            complete: function(data) {
                console.log("完成", data);
                //替换input
                $(this).parent().html($(this).parent().html());
            }
        });

    }
    $("#uploadForm").on("change", "#files", function() {
        var $this = $(this);
        doUpload($this);
    })
    </script>
</body>

</html>

```
- 后台代码

```JavaScript
var formidable = require('formidable');
var uuid = require('node-uuid');
var fs = require('fs');
var express = require('express');
var http = require('http');

var app = express();
var allowCrossDomain = function(req, res, next) {
    res.header('Access-Control-Allow-Origin', '*');
    res.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
    res.header('Access-Control-Allow-Headers', 'Content-Type');

    next();
};
app.use(allowCrossDomain);


function upload_path(path) {
    var _path = `${__dirname}/${path}`;
    try {
        fs.accessSync(_path);
    } catch (e) {
        fs.mkdirSync(_path);
    }
    return `${_path}/`;
}

function node_upload(req, callback, next) {
    var form = new formidable.IncomingForm();
    form.encoding = 'utf-8';
    form.uploadDir = upload_path('uploads');
    form.maxFieldsSize = 10 * 1024 * 1024;
    //解析
    form.parse(req, function(err, fields, files) {
        if (err) return callback(err);

        for (var file in files) {
            //后缀名
            var extName = /\.[^\.]+/.exec(files[file].name);
            var ext = Array.isArray(extName) ? extName[0] : '';
            //重命名，以防文件重复
            var avatarName = uuid() + ext;
            //移动的文件目录
            var newPath = form.uploadDir + avatarName;
            fs.renameSync(files[file].path, newPath);
            fields[file] = {
                size: files[file].size,
                path: newPath,
                name: files[file].name,
                type: files[file].type,
                extName: ext
            };
        }
        callback(null, fields);
    });
}
app.post('/upload', function(req, res, next) {
    // console.log(req.body)
    node_upload(req, function(err, fields) {
        setTimeout(function() {
            // res.end('1232344')
            res.json(fields);
        }, 1000);
    }, next);
});

http.createServer(app).listen(8002, function() {
    console.log('Express server listening on port 8002');
});


```

## 文件上传  
- 使用同步ajax上传文件的时候会是页面阻塞, 请求前面的额代码执行效果不能展示
- 与alert(1)原理相同, alert会阻塞页面渲染,渲染dom阶段与看到dom阶段是不同的
