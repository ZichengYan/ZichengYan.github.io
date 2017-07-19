---
title: angular路由
date: 2016-09-23 08:10:03
tags: angular
---

##  Api和WebApi

- Api 
    + `Application Programming Interface`, 应用程序编程接口
    + 通常是指方法的集合
- WebApi
    + `Web Application Programming Interface`, 网络应用程序编程接口
    + 通常是指通过发送get、post数据请求不同路径获取数据
- 接口文档&Api文档
- 常用Api和WebApi
    + 百度地图：`http://lbsyun.baidu.com/`
    + 百度api：`http://apistore.baidu.com/`
    + 豆瓣api：`https://developers.douban.com/wiki/?title=api_v2`
- 常用检测工具PostMan
 
头信息 `Access-Control-Allow-Origin:* ` 百度天气api里面有豆瓣的api里面没有
 
## $http

```
angular提供了$http服务来同服务端进行通信，$http服务队浏览器的XMLHttpRequest对象进行了封装，
让我们可以以ajax的方式来从服务器请求数据。
$http服务是一个接受一个参数的函数，参数的类型是对象，用来配置生成的http的请求
{
    method: 'GET',//发送get请求
    url: 'http://apis.baidu.com/apistore/weatherservice/recentweathers?cityname=北京&cityid=101010300',
    headers:{
        'apikey':'8a8efad7ed263d1b8cac9e3354fc16b5'//你的key
    }
}
 
   $http(参数).then(function(data) {
            //成功的回调函数
            console.log('successCallback');
            console.log(data);
            $scope.jsonData=data;
        },function(data) {
            //失败的回调函数
            console.log('errorCallback');
            console.log(data);
        })
        
```
 
##跨域

### script标签跨域(这就是jsonp)

- 场景：需要快捷方便的使用接口的时候
- 原理：1.动态创建script标签，
       2. src指向服务器的js的文件地址
       3.约定传输的callback参数
       4.返回并执行
 
- window.name,iframe, postMessage
    + 在同一个标签页是共用一个name
 
### angular jsonp

- $http
 
angular.callbacks
 
### 百度api

百度天气 支持ajax直接跨域请求 原因`Access-Control-Allow-Origin →*`
 
### 豆瓣api

豆瓣不支持`Access-Control-Allow-Origin` 跨域

#### jsonp方法
 
 
#### 理解封装的jsonp方法