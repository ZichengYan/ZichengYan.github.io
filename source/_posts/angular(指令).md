---
title: angular路由
date: 2016-07-14 22:09:00
tags: angular
---

### 自定义指令简单介绍及使用
- 自定义指令无外乎增强了HTML,提供了额外的功能。
- 内部指令基本能满足我们的需求。
- 少数情况下我们有一些特殊的需要，可以通过自定义指令的方式实现：
 
- 通过 模块对象的directive方法创建
    + 有两个参数，第一个参数，是指令的名字：必须是驼峰命名法命名
                  第二个参数和控制器的第二个参数一样,在第二个参数的function里直接返回的一个obj对象
    + 使用时：需要将指令的名字转成小写，并以-分割原先在大小写字母
 
    例子： app.directive('myBtn',[function(){
 
 
    }]);
    注意：需要返回一个对象。
### 自定义指令中回函数里返回的对象的属性
- template:需要一个字符串，最终这个字符串值被被添加到自定义指令所在标签的innerHTML位置
 
  1.创建定义指令
 
```
  javascript
     app.directive('myBtn',[function(){
            var obj={
                  template:'<button>我是button</button>'
            }
            return obj;
        }]);
 
```
 
  2.定义指令的引用
   <div my-btn></div>
 
- templateUrl:需要一个字符串，这个字符串是一个文本文件的路径,anuglar最终会异步请求这个文件，
    把拿到的内容插入到自定义指令所在的标签的innerHTML位置,
    该字符串也可以是script标签的id值，把script标签中的内容当作模板字符串来使用
    注意：script的type属性需要为"text/ng-template"
    1.第一种用法：
    templateUrl:'./view.html'
    注意：需要通过静态文件服务器打开查看，因为获取./view.html的方式是一个get请求
    2.第二种用法
    通过id指向一个
    templateUrl:'tpl'
    <script id="tpl" type="text/ng-template">
            <button>我是button</button>
    </script>
    注意：script的type属性需要为"text/ng-template"不是"test/javascript"
 
- restrict:也是需要一个字符，可以是A,E,C 这3个字符中任何一个，也可以任意的组合，
    A:以属性的形式使用
    E:以自定义标签的形式使用
    C:表示以类样式名的形式使用
    1. 在返回的对象中添加控制，如果不写默认是AE
     return {
            template:'<h1>myHello</h1>',
             restrict:'EAC' //restrict用来限制自定义呈现形式
            }
     2.      
    <my-hello></my-hello>  E:自定义标签
    <div my-hello></div> A:属性形式
    <div class="my-hello"></div>  C:类形式
 
- replace: 需要一个布尔值，为true,会将自定义指令所在的标签替换为模板字符串。
   replace:true;
 
```
<body ng-app="myApp">
    <div my-hello></div>
    <hello></hello>
    <div class="my-hello"></div>
    <script src="angular.min.js"></script>
    <script>
    //定义模块
    var app = angular.module('myApp', []);
    //创建自定义指令
    app.directive('myHello', function() {
        return {
            //使用script标签创建模板
            template: '<h1>woshi</h1>',
            restrict: 'AC', //
            replace:true
        };
    });
    app.directive('hello', function() {
        return {
            //使用script标签创建模板
            template: '<h1>woshi</h1>',
            restrict: 'E' ,
            replace:true
            //
        };
    });
    </script>
</body>
 
```
 
- transclude:转置，是需要一个布尔值，为true时会把自定义指令所在标签的innerHTML值添加到模板字符串中，
  需要与ng-transclude指令配合使用，ng-transclude指令需要将值插入到哪个元素的innerHTML位置.
  不能与replace指令同用。
  1.当自定义的标签<my-hello>这是我在外部传进来的值</my-hello>需要将里面的值添加进模板当中
  2.  return {
            template:'<div>' +
            '<h1 ng-transclude></h1><h2 ng-transclude> </h2>' +
            '</div>',
            transclude:true
        }
 
- link:指向一个function，这个function有三个参数：
    + scope: 类似于控制器中的$scope,也可以暴露一些值。
    + element:这是一个jqLite对象，是自定义指令所在标签的jqLite对象
    + attributes:是自定义指令所在标签的所以属性的集合.
 
    return {
            link:function (scope,ele,attr) {
                console.log(scope);
                console.log(ele);
                console.log(attr);
                //ele就是咱们的jqLite元素
                ele.on('click',function () {
                    console.log('这是jqLite的做出来的log');
                })
                //在angular中所有的dom处理建议在自定义指令中完成
            }
        }
 
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .red{
            height: 100px;
            width: 100px;
            background-color: red;
        }
    </style>
</head>
<body ng-app="myApp">
    <div my-link="" class="red">
 
    </div>
</body>
<script src="angular.js"></script>
<script>
    //定义一个模板
    var app=angular.module('myApp',[]);
    //创建一个自定义模板
    app.directive('myLink',function () {
      return {
        link:function (scope,ele,attr) {
          console.log(scope);
          console.log(ele);
          console.log(attr);
          ele.on('click',function () {
            console.log("这是使用jqLite添加的事件");
          });
        }
      };
    });
</script>
</html>
 
```
 
## todomvc案例
http://todomvc.com/
https://github.com/tastejs/todomvc-app-template
 
### todomvc 简单介绍
 
 
### todomvc 功能分析
 
1.显示数据列表
 
 
 
2.添加任务
 
 
 
 
3.删除任务
    - 使用了数组的splice
 
4.修改任务
- 只是改变页面是否可以编辑的一个状态
 
 
5.切换是任务是否完成的状态
 
6.批量的切换任务是否完成的状态
    - 使用了ng-change事件
 
7.清除已完成任务
- 尽量不要在循环中添加或删除数组元素。
 
7.1 控制清除已完成任务按钮的显示与否
 
8.显示未完成的任务数
- 是给ng-bind指定一个方法,方法最终会返回一个具体的值,
- ng-bind 会把这个值渲染到页面。
 
 
##todomvc的开发步骤
###准备工作
1.把js代码写入app.js里，统一管理起来,引入angular,将app.js里面的window改成angular
2. 创建模块与页面进行关联
//创建模块
var app =angular.module("todos",[]);
3.创建控制器
app.controller('todosController',['$scope',function($scope){}]);
 
###1 显示任务列表
1. 写一些静态数据
 
    var tasks=[
    {id:1,name:'吃饭',completed:false},
    {id:2,name:'睡觉',completed:true},
    {id:3,name:'学习',completed:false},
    {id:4,name:'休息',completed:true},
    {id:5,name:'打球',completed:true},
    ];
    $scope.tasks=tasks;
2. 在<ul class="todo-list">标签里面删除一个li标签
3.通过ng-repeat把数据循环显示在页面中，设置样式通过item.completed是否完成
<li ng-class="{'completed':item.completed}" ng-repeat="item in tasks">
4.     <label>Taste JavaScript</label>把任务内容替换成{{item.name}}
 
###2 添加任务
1. 找到任务输入的文本框
2. 绑定 ng-model到input输入框里面
ng-model="newTask"
3.用一个from表单包裹这个input输入框,在form表单上添加点击事件
    <form ng-submit="add()">
        <input ng-model="newTask" class="new-todo" placeholder="What needs to be done?" autofocus>
    </form>
4. 初始化newTask定义add方法
  $scope.newTask='';
       $scope.add=function(){
            if(!$scope.newTask){
                return;
            }
            // 动态的计算id
            var id;
            if(!$scope.tasks){
                id=1;
            }else{
                id=$scope.tasks[$scope.tasks.length-1].id+1;
            }
            // 添加数据到数据中
           $scope.tasks.push({id:id,name:$scope.newTask,completed:false});
           // 清空文本框架的值
           $scope.newTask='';
       } 
  注意：id取值法 Math.random()或数字的增长
###3 删除任务
1.给button添加一个点击事件remove()
  ng-click="remove()"
2. 定义一个删除的方法
       $scope.remove=function(id){
           for (var i = 0; i < $scope.tasks.length; i++) {
               var item = $scope.tasks[i];
               if(item.id==id){
                // 从数组中移除数据
                 $scope.tasks.splice(i,1);
                 return;
               }
           }
       }
3.remove()方法中添加item.id
###4 修改任务
1.<label ng-dblclick="edit(item.id)">{{item.name}}</label>
2.在<li ng-class="{'completed':item.completed}" ng-repeat="item in tasks">
中添加'editing':isEditingId==item.id
<li ng-class="{'completed':item.completed,'editing':isEditingId==item.id}" ng-repeat="item in tasks">
3.给<input ng-model="item.name" class="edit" value="Create a TodoMVC template">
包上   <form ng-submit="save()"></form>   
3.添加编辑代码
     $scope.isEditingId=-1;
       $scope.edit=function(id){
 
           $scope.isEditingId=id;
       }
       $scope.save=function(){
           $scope.isEditingId=-1;
       }
###5 切换任务是否完成
1.把item.completed 与<input   class="toggle" type="checkbox" checked>绑定
ng-model="item.completed"
###6 批量设置是否完成
1. <input  class="toggle-all" type="checkbox">
    给标签添加点击事件ng-click="toggleAll()"
2.给标签绑定模型 ng-model="isSelected"
<input ng-cilck="toggleAll()" ng-model="isSelected" class="toggle-all" type="checkbox">
3.添加方法&初始化isSelected选中的状态
        $scope.isSelected=false;
 
       $scope.toggleAll=function(){
           for (var i = 0; i < $scope.tasks.length; i++) {
              var item = $scope.tasks[i];
              item.completed=$scope.isSelected;
           }
}
 
###7 移除完成项
1. ng-click="clearCompleted()" 添加到标签里面
    <button class="clear-completed">Clear completed</button>
2.错误的写法
  $scope.clearCompleted=function(){
 
         // 尽量不要在循环中删除或添加数据中的元素。
            for (var i = 0; i < $scope.tasks.length; i++) {
               var item =  $scope.tasks[i];
               if(item.completed){
                 $scope.tasks.splice(i,1);
               }
            }
       }
3.正确的写法      
  $scope.clearCompleted=function(){
           var tmp = [];
 
           // 将未完成的任务添加到临时数组中
           for (var i = 0; i < $scope.tasks.length; i++) {
              var item = $scope.tasks[i];
              if(!item.completed){
                tmp.push(item);
              }
           }
 
           $scope.tasks=tmp;
       }
 
###7.5 清除已完成的按钮如果没有需要清除则不显示
1.把 ng-show="isShow()"添加到
<button class="clear-completed">Clear completed</button> 中   
 2.     $scope.isShow=function(){
           for (var i = 0; i < $scope.tasks.length; i++) {
               var item = $scope.tasks[i];
               if(item.completed){
                 return true;
               }
           }
           return false;
       }   
 
 
###8 显示未完成的任务数
1.ng-bind ng-bind="unCompleted()"
<span class="todo-count"><strong>0</strong> item left</span>
 
  $scope.unCompleted=function(){
            var count =0;
           for (var i = 0; i < $scope.tasks.length; i++) {
             var item =  $scope.tasks[i];
             if(!item.completed){
                count++;
             }
           }
           return count;
       }
 
 
 
 
 
 
# Angular服务
-  什么是服务
    +  在 AngularJS 中，服务是一个函数或对象，可在你的 AngularJS 应用中使用。AngularJS 内建了30 多个服务。
-     Angular主要用到的服务
    +  $scope：作用域，用来负责连接View和Controller，也就是MVVM中的ViewModel相当于桥梁一样。
    +  $log
    +  $interval和setInterval区别
    在数据变换过程中有时候angular监视不到数据变化:
        setInterval(function () {
            $scope.time=new Date();
            console.log($scope.time);
             $scope.$apply();//告诉angular进行数据更新
        },1000)
        //但是如果说使用 $interval这种angular的服务有时候服务内部就帮我们完成了这种数据更新
            $interval(function () {
            $scope.time2=new Date();
            },1000)
-  创建服务
   通过module创建： service、factory
   + service创建：
     app.service('myService',function () {
        this.name='myService';
    });
   + factory创建:
      app.factory('myFactory',function () {
        return {
            name:'myFactory',
        }
    });
