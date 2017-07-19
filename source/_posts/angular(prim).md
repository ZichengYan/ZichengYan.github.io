---
title: angular路由
date: 2016-06-23 11:12:35
tags: angular
---

## mvvm
### $scope
- 视图和控制器之间的数据桥梁
- 用于在视图和控制器之间传递数据
- $scope的生命周期

   + 创建、链接、更新、销毁
 
 
### ViewModel
 
- $scope 实际上就是MVVM中所谓的VM（视图模型）
- 正是因为$scope在Angular中大量使用甚至盖过了C（控制器）的概念，所以很多人把Angular称之为MVVM框架
## Angular全局Api使用
- 数据比较API
    + angular.isArray()    判断给定的对象是否为数组。
    + angular.isDate()    判断给定的对象是否为日期类型。
    + angular.isDefined()    判断给定的对象是否定义过。
    + angular.isElement()    判断给定的对象是否为一个DOM元素。
    + angular.isFunction()    判断给定的对象是否为一个函数。
    + angular.isNumber()    判断给定的对象是否为数字。
    + angular.isObject()    判断给定的对象是否为object类型。
    + angular.isString()    判断给定的对象是否为字符串。
    + angular.isUndefined()    判断给定的对象是否没有定义过（与angular.isDefined()相反）。
    + angular.equals()    判断给定的两个对象是否相等。
- 其他API使用
    + angular.lowercase()    将字符串转换为小写形式。
    + angular.uppercase()    将字符串转换为大写形式。
    + angular.copy()    深拷贝一个对象或数组。
    + angular.forEach()    遍历对象或数组中的每一个元素并执行一个函数。
 
```javascript
 
    var values = {name: 'feifei', gender: 'zhuzhu'};
    angular.forEach(values, function(value, key) {
    });
 
    var objs =[1,2];
    angular.forEach(objs, function(data,index,array){
        console.log(data);
        console.log(index);
        console.log(array);
    });
```
## 模块
### 控制器的作用
    - 初始化属性
    - 暴露属性或者行为
    - 监视数据变化
      $scope.name='';
        $scope.$watch('name',function (newVal,oldVal) {
            console.log(newVal);
            console.log(oldVal);
        })
### 控制器代码压缩问题
    - 当代码进行js压缩时候controller里面的内容会被当成变量替换掉，
    为了防止这个问题发生在controller中出现 controller('myCtrl',['$scop',function($scope){}])
### 控制器的多种写法
  - 1.标准写法
     app.controller('myCtrl',function(){})
  - 2.早期使用 （angular-1.2.29版本）
    function  myController(\$scope) {
        $scope.name="angular早期使用";
    }  
  - 3. fuction写在外面（写在外面不能被压缩）
   function otherCtrl($scope) {
        $scope.name='123';
    }
    app.controller('myCtrl',otherCtrl)
- 4. fuction写在外面（写在外面不能被压缩）
   function otherCtrl(otherscope) {
        otherscope.name='123';
    }
    //依赖注入
    otherCtrl.$inject=['$scope'];//这里对方法添加$inject
    app.controller('myCtrl',otherCtrl)
 
 - 5.  面向对象方法使用
        - 1.控制器的function不写改为引用function app.controller('myCtrl',demoCtrl);
        - 2.创建一个面向对象的function ` function demoCtrl() {
                this.name='123';
            } `
        - 3.使用的时候添加 ` as scope ` ng-controller="myCtrl as scope"
#依赖注入
- 没事你不要来找我，有事我会去找你。
- 原理
   框架在调用方法的过程中通过获取到传递的参数，然后框架内部将方法toString处理以后，
   再通过正则表达式将其获取到然后依次实例化。
### 指令
 
- 在 AngularJS 中将前缀为 ng- 这种属性称之为指令，其作用就是为 DOM 元素调用方法、定义行为绑定数据等
- 简单说：当一个 Angular 应用启动，Angular 就会遍历 DOM 树来解析 HTML，根据指令不同，完成不同操作
 
- ng-bind
    + 用来解决表达式闪烁问题
    + `<p ng-bind="数据模型"></p>替代了{{数据模型}}`
 
       {{name}}  <p ng-bind="name"></p>
 
    *注意：只能够在双标签中使用ng-bind指令*
 
- ng-cloak
    + 用来解决表达式闪烁问题
    + 写一个样式使页面的元素隐藏
    <style>
        .ng-cloak{
            display: none;
        }
    </style>
    + `<p class="ng-cloak">{{name}}</p>`
    + 利用angular在加载会移除页面上所以名为ng-cloak的样式名的特性。
- 页面安全的问题
   直接编写一些
    <script>
        document.write('<script>alert("");<\/script>')
    </script>
- ngSanitize模块
      `npm install angular-sanitize`
    + 在module的中括号中添加ngSanitize
    + 使用的是ng-bind-html指令来渲染数据模型。
    <p ng-bind-html="name"></p>
 
- ng-repeat
    + 可以用来循环输出数组
    + 写在哪个元素上就是循环哪个元素。
    + 语法：类似于forin 循环
        > `<div ng-repeat="item in data ">{{item}}</div>`
 
    + 还可以用来渲染key,value对
    + ng-repeat 在遍历里会暴露一些数据模型,
        - $even:提供了一个布尔值，当为true时表示当前数据是第偶数条数据,从索引0开始计算
        - $odd:提供了一个布尔值，当为true时表示当前数据是第奇数条数据,从索引0开始计算
ng-class:
    + 从多种样式中选择一个样式
        - 语法：类似于从一个key,value对象中获取其中一个属性的值
        - `ng-class="{'A':'red','B':'blue','C':'green'}"`
    + 从多种样式中选择多个
        - 语法：也是写一个key,value对象，这里的key是我们提供的类样式名，value是一个布尔值，为true时对应的key会被作为样式名加入到class中
 
ng-hide/ng-show
- ng-hide：需要一个布尔值：当为true时为隐藏当前元素
- ng-show: 需要一个布尔值：当为true时为显示当前元素
- ng-switch:与ng-switch-when同用，类似与js中的switch case
 
```html
    <div ng-switch="name">
            <div ng-switch-when="小明">我是小明</div>
            <div ng-switch-when="小红">我是小红</div>
            <div ng-switch-when="小月">我是小月</div>
    </div>
```
 
### 其他常用指令
 
- ng-checked：
  + 单选/复选是否选中,是单向数据绑定
- ng-selected：
  + 是否选中
- ng-disabled：
  + 是否禁用
- ng-readonly：
  + 是否只读
 
### 常用事件指令
 
- 不同于以上的功能性指令，Angular还定义了一些用于和事件绑定的指令：
- `ng-blur：失去焦点`
- `ng-focus：获得焦点`
- `ng-change：改变事件`
- `ng-click： ng-click="add()"`
- `ng-dblclick：双击事件`
- `ng-submit： 表单提交事件`