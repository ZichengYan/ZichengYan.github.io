---
title: angular路由
date: 2016-06-24 10:14:37
tags: angular
---

# 过滤器
- 过滤器?
    + 过滤器（filter）正如其名，作用就是接收一个输入，通过某个规则进行处理，然后返回处理后的结果。主要用在数据的格式化上，
    例如获取一个数组中的子集，对数组中的元素进行排序等。ng内置了一些过滤器，它们是：currency(货币)、date(日期)、filter(子串匹配)、json(格式化json对象)、limitTo(限制个数)、lowercase(小写)、uppercase(大写)、number(数字)、orderBy(排序)。
- Angular官方的过滤器
    +    currency(货币)
        - {{1000 | currency:"USD$":0}}
    +    date(日期)
        - {{1288323623006|date:"yyyy-MM-dd HH:mm:ss"}}
    +    json(格式化json对象)
        -  ` <pre >{{ {'name':'value'} | json }}</pre>  `
    +    limitTo(限制个数)
        -  {{ numbers | limitTo:numLimit }}
    +    lowercase(小写)
        -  {{ lowercase_expression | lowercase}}
    +        uppercase(大写)
        -  {{ uppercase_expression | uppercase}}
    +    number(数字)
        -  {{1234 | number:0}}
    +    orderBy(排序)
         | orderBy:'name'
    +    filter(子串匹配)
         |filter:{completed:true}
### todomvc 切换不同状态任务的显示与否
 
 
 
### spa
### spa基础原理
-  通过锚点值改变url，切换页面
### $location监视页面锚点的变化
- $location.url()方法可以获取到页面的锚点值，但是不包含#号
- 是通过$watch动态的监视$location.url()方法的返回值,再做相应的处理.
- 要把$location赋值给$scope的一个属性($scope.loaction=$location)
### 修改todomvc使用$location的方式
### 自定义服务
- 通过模块对象的service方法创建，参数类似与controller的参数
- service中的function是当作一个构造函数来使用的,
- 直接在控制器的注入service的名字，它就是这个构造函数的实例对象
 
### 抽象服务
### 回顾todomvc案例
### 准备工作
1.创建service
   var app = angular.module('todos.service',[])
  app.service('todosService',function(){
        this.add=function(v1,v2){
           return v1+v2;
        }
    })
2.服务所在模块加入主模块
   var app = angular.module('todos',['todos.service']);
   app.controller('todosController',["$scope","todosService",function($scope,todosService){}]);
3.把服务所在的js引入页面
###获取数据
        // 拿到数据
        var str = storage.getItem('todos');
        var tasks = JSON.parse(str||'[]');
 
        // 1.获取数据
        this.get=function(){
            return tasks;
        }
###保存数据
 -  // 保存任务
        this.save=function(){
            storage.setItem('todos',JSON.stringify(tasks));
        }
-service里添加
     this.save();
###逐个删除
-$scope.remove=todosService.remove;  
-service里添加
     this.save();    
 
###切换任务是否完成的状态
-$scope.$watch('tasks',function(nowValue,oldVAlue){
            todosService.save();
       },true);
###批量切换任务是否完成的状态
- todosService.toggleAll($scope.isSelected);
- service里添加
     this.save();
 
 
## 路由
 
### 路由介绍
 
 
### 路由初步使用（ngRoute）
` npm instal angular-route`
- 通过模块的config方法来创建路由规则
- 有一个参数：类似于controller的第二个参数
- 有一个需要注入的参数:$routeProvider
    + 这个参数是用来设置具体的规则的
    + $routeProvier.when()
        - when第一个参数是当前url中锚点的值
        - when第二个参数是object对象：template属性
            - 最终angular会把template对应的模板字符串插入到页面拥有ng-view指令的标签的innerHTML位置.
            - controller属性，指向一个控制器,最终控制器的暴露的数据能够在template指定的字符串的使用。
 
 
### 路由参数
- 类似于过滤器中使用参数的形式
- when('/students/:name'),最终在控制器中可以通过$routeParams拿到这个参数，
    + $routeParams就是一个拥有name属性的对象.
    + 可以在参数后加个问号表示当前参数是可选。
        ——- when('/students/:name?')
 
 
 
- otherwise
- 用于匹配前面所有when方法没有匹配到规则。
    +指定了一个对象作为参数，这个对象有个属性:redirectTo:'/students/'
###完整写法
    var app=angular.module('myApp',['ngRoute']);
    //$routeProvider用他来配置路由表
    app.config(function ($routeProvider) {
        //1路径
        //2对象：你要做的事
        $routeProvider
                .when('/my',{
                    template:'<h1>我的音乐</h1>'
                })
                .when('/friend',{
                    template:'<h2>{{name}}</h2>',
                    controller:function ($scope) {
                        //匿名的controller
                        $scope.name='朋友'
                    }
                })
                .when('/mycontroller',{
                    template:'<h3>{{name}}</h3>',
                    controller:'myCtrl'
                })
                .when('/mytemplate',{ //推荐写法
                    templateUrl:'mytemplate.html',
                    controller:'myCtrl2'
                })
                .otherwise({
                    redirectTo:'/my'   //默认跳转现有路径
                });
    });
### webApi介绍--
- url
I/O
 
聚合数据
 
### API
- application programming interface
 
console.log(name)
I/O 有输入有输出的方法
 
document.getElementById('idname')
 
### 豆瓣api介绍
https://developers.douban.com/
http://api.douban.com/v2/movie/in_theaters