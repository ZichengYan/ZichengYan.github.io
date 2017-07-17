---
title: gulp配置
date: 2017-04-24 09:14:37
tags: gulp
---

#  [大公司是怎么样开发和部署前端代码的](https://www.zhihu.com/question/20790576)

# cdn资源
- 静态资源 CDN 公共库是指一些服务商将我们常用的 JavaScript 库存放到网上，方便开发者直接调用，并且还对其提供 CDN 加速，这样一来可以让用户加速访问这些资源，二来还可节约自己服务器的流量。  
-  [百度静态资源公共库](http://cdn.code.baidu.com/)
    + `http://cdn.code.baidu.com/`
    + 提供的库比较全，但是不支持 https，使用了 https 加密站点使用会出现警告。
-  [新浪云计算公共库](http://lib.sinaapp.com/)
    + `http://lib.sinaapp.com/`
    + 支持的库比较少，但是支持 https。
-  [360网站卫士常用前端公共库](http://libs.useso.com/)
    + `http://libs.useso.com/`
    + 除了提供前端库之外，只需替换一下域名，360 就可以让你继续使用 Google 提供的前端公共库和免费字体库。但是同样最大的问题，不支持 https。
-  [七牛云存储开放静态资源文件](http://staticfile.org/)
    + `http://staticfile.org/`
    + 国内目前最全的前端库了，使用 https 要换用另外一个域名：`https://dn-staticfile.qbox.me/`

## 常用cdn资源

-  jquery 
    + `http://cdn.staticfile.org/jquery/3.2.1/jquery.js`
    + `https://cdn.staticfile.org/jquery/3.2.1/jquery.min.js`
    + `https://cdn.staticfile.org/jquery/3.2.1/jquery.min.map`
- angular 
    + `https://cdn.staticfile.org/angular.js/1.5.9/angular.js`
    + `https://cdn.staticfile.org/angular.js/1.5.9/angular.min.js`
    + `https://cdn.staticfile.org/angular.js/1.5.9/angular.min.js.map`

# gulp 


## 常用插件

- gulp-less 编译LESS文件
- gulp-autoprefixer 添加CSS私有前缀
- gulp-cssmin 压缩CSS
- gulp-rname重命名
- gulp-imagemin 图片压缩
- gulp-uglify 压缩Javascript
- gulp-concat 合并
- gulp-htmlmin 压缩HTML
- gulp-rev 添加版本号 
    + 版本号替换的只有当内容修改了之后才会更换版本号 , 因为修改版本号就是解决缓存问题 , 但是我的文件并没有进行修改 , 如果强制做了版本号修改,那么缓存资源就浪费了
- gulp-rev-collector 内容替换
- gulp-useref  替换文件注释块 ,合并输出(不可控制,例如只使用其替换注释快的功能是不行的)
- gulp-if  

## BUG

- @import url("./index.less");
   + 需要注意行尾的分号

#### 压缩css(gulp-cssmin)

```

// 这个文件里可配置一些信息
// 来支配gulp如何工作

// 引入包
var gulp = require('gulp');

// 具体负责压缩任务
var cssmin = require('gulp-cssmin');

// gulp 是一个对象，此对象下有一系列方法可
// 以实现压缩合并等功能

// 通过任务来实现不同资源（css、js、imgage）进行不同处理
gulp.task('css', function () {
   // console.log('压缩css');
   // 通过gulp所要压缩资源的位置（路径）
   gulp.src('./css/main.css')
      .pipe(cssmin())
      .pipe(gulp.dest('./css/main.min.css'));

   // gulp 是一个总指挥，不参与具体事务
   // 通过调用gulp插件(基于nodejs的)来实现

});

// 调用任务，通过命令行进行调用

```

```
var gulp = require('gulp');
var cssmin = require('gulp-cssmin')
var autoprefixer = require('gulp-autoprefixer')
var less = require('gulp-less')
gulp.task('css', function() {
    gulp.src('./css/main.less')
        .pipe(less())
        .pipe(cssmin())
        .pipe(autoprefixer({
            browsers: ['last 5 version']
        }))        
        .pipe(gulp.dest('./dist1/css'))
})

```
#### 加私有化前缀(gulp-autoprefixer)
- 因为当时chrome浏览器属性处于测试阶段,需要加上私有化前缀才能使用

#### 图片压缩

```
gulp.task('image', function() {
    gulp.src('./src/img/**/*',{base:"./src"})//两个**是代表递归操作,{base会将这个目录下的目录搬到./dist目录下,即执行后为./dist/img/文件}
        .pipe(img())
        .pipe(gulp.dest('./dist/'))
    console.log(111);
})

```
#### js合并压缩

```
gulp.task('js', function() {
    gulp.src('./src/js/*',{base:"./src"})
        .pipe(uglify())  //压缩
        .pipe(concat('./js/all.js'))  //合并
        .pipe(gulp.dest('./dist/'))
    console.log(111);
})

```


#### html压缩

```
gulp.task('html', function() {
    gulp.src('./src/*.html', { base: "./src" })
        .pipe(htmlmin({ 
          collapseWhitespace: true, //去掉空白符号
          minifyCSS: true, //压缩css
          removeComments:true,//去掉注释
          minifyJS:true }))//压缩js代码
        .pipe(gulp.dest('./dist/'))
    console.log(111);
})

```


#### js压缩

```
gulp.task('js', function() {
    gulp.src('./src/js/*', { base: "./src" })
        .pipe(uglify())
        .pipe(concat('./js/all.js'))
        .pipe(gulp.dest('./dist/'))
    console.log(111);
})

``` 

#### 添加版本号

- 因为浏览器缓存功能

```
gulp.task('css', function() {
    gulp.src('./src/css/main.less', { base: "./src" })
        .pipe(less())
        .pipe(cssmin())
        .pipe(rev()) //给名字加上版本号
        .pipe(autoprefixer({
            browsers: ['last 5 version']
        }))
        .pipe(gulp.dest('./dist'))
        .pipe(rev.manifest()) //收集替换信息
        .pipe(rename('css-reanem.json'))//修改名称
        .pipe(gulp.dest('./dist/rev'))
})

```


#### 替换引用

- rev

```
//替换内容
gulp.task('rev',function () {
  gulp.src(['./dist/rev/*.json','./dist/html.html'])
  .pipe(revCollector())
  .pipe(gulp.dest('./dist'));

})

```

- gulp-useref

```

gulp.task('useref', function() {
    gulp.src('./src/html.html')
        .pipe(useref())
        .pipe(gulpif('*.js',uglify()))//判断html文件中如果是js文件那么就压缩
        .pipe(gulp.dest('./dist'));
})

```
  
```
//替换
 <!-- build:js ./js/all.js --> 
    <script src="js/js.js"></script>
    <script src="js/js2.js"></script>
  <!-- endbuild -->

```


```
<!-- build:remove --> 
    <script src="js/js.js"></script>
    <script src="js/js2.js"></script>
  <!-- endbuild -->

```

# gulp完整版

### gulpfile.js

- userf

```js
const gulp = require('gulp');
const gulpSequence = require('gulp-sequence');
const cssmin = require('gulp-minify-css');
const htmlmin = require('gulp-htmlmin');
const rev = require('gulp-rev');
const revCollector = require('gulp-rev-collector');
const clean = require('gulp-clean');
const rename = require('gulp-rename');
const gulpif = require('gulp-if');
const base64 = require('gulp-base64');
const useref = require('gulp-useref');
const concat = require('gulp-concat');
const cssimport = require('gulp-cssimport');
const uglify = require('gulp-uglify');
const babel = require("gulp-babel"); //转为es5 否则html压缩的时候会报错 

const src = {
    bower: {
        css: [
            './bower_components/font-awesome/css/font-awesome.min.css',//字体图标
            './bower_components/weui/dist/style/weui.min.css',//weui css库
        ],
        js: [
            './bower_components/jquery/dist/jquery.min.js',//jquery
            './bower_components/art-template/dist/template.js',//artTemplate模板
            './bower_components/i18next/i18next.min.js',//国际化核心插件
            './bower_components/jquery-i18next/jquery-i18next.min.js',//国际化扩展插件
            './bower_components/weui.js/dist/weui.min.js',//weui js库
            './bower_components/fastclick/lib/fastclick.js'
        ]
    }
}
//清空
gulp.task('clean', function () {
    return gulp.src('./dist')
        .pipe(clean());
});

//css
gulp.task('css', function () {
    console.log('css  finished');
    return gulp.src(['./theme/default/css/**/*.css', '!./theme/default/css/main.css'], {base: "./"})
        .pipe(gulpif('*.css', cssimport()))
        //.pipe(gulpif('*.css'),base64())
        .pipe(cssmin({}))
        .pipe(rev()) //给名字加上版本号
        .pipe(gulp.dest('./dist/'))
        .pipe(rev.manifest()) //收集替换信息
        .pipe(rename('css-rename.json'))//修改名称
        .pipe(gulp.dest('./dist/rev'));// 保存位置
});

//image
gulp.task('image', function () {
    console.log('image  finished');
    return gulp.src(['./theme/default/images/**/*'], {base: "./"})
        .pipe(gulp.dest('./dist/'));// 保存位置
});





//html
gulp.task('html', function () {
    var options = {
        removeComments: true,//清除HTML注释
        //collapseWhitespace: true,//压缩HTML
        //collapseBooleanAttributes: true,//省略布尔属性的值 <input checked="true"/> ==> <input />
        removeEmptyAttributes: true,//删除所有空格作属性值 <input id="" /> ==> <input />
        //removeScriptTypeAttributes: true,//删除<script>的type="text/javascript"
        //removeStyleLinkTypeAttributes: true,//删除<style>和<link>的type="text/css"
        minifyJS: true,//压缩页面JS
        minifyCSS: true//压缩页面CSS
    };
    console.log('html  finished');
    return gulp.src(['./html/**/*', './index.html', './clear.html'], {base: "./"})
        .pipe(useref())
        .pipe(htmlmin(options))
        .pipe(gulp.dest('./dist'));
});

//js
gulp.task('js', function () {
    console.log('js  finished');
const condition = function (f) {
    if (f.path.endsWith('config.js')) {
        return false;
    }
    return true;
}
    return gulp.src('./js/**/*', {base: "./"})
                  .pipe(stripDebug()) // 清除console debugger alert
        .pipe(gulpif(condition, uglify()))// 压缩js
        .pipe(gulpif('*.js', rev())) //给名字加上版本号
         .pipe(gulp.dest('./dist/'))
        .pipe(rev.manifest()) //收集替换信息
         .pipe(rename('js-rename.json'))//修改名称
         .pipe(gulp.dest('./dist/rev'));// 保存位置;
});

//bower静态资源
gulp.task('bower', function () {
    console.log('bower静态资源  finished');
    return gulp.src('./bower_components/**/*', {base: "./"})
        .pipe(gulp.dest('./dist/'));
});

//插件
gulp.task('plugins', function () {
    console.log('插件  finished');
    return gulp.src('./plugins/**/*', {base: "./"})
        .pipe(gulp.dest('./dist/'));
});

//替换css,js引用
gulp.task('rev', function () {
    console.log('替换css,js引用');
    return gulp.src(
        ['./dist/rev/**/*.json',
            './dist/html/**/*.html',
            './dist/*.html',
            './dist/js/**/*.js'],
        {base: './dist'})
        .pipe(revCollector({replaceReved:true }))
        .pipe(gulp.dest('./dist'));
});


// parallel 'js', 'bower', 'plugins',


// parallel 'html'   'css'

// gulp.task('default', ['js', 'bower', 'plugins', 'html', 'css']);

gulp.task('default', gulpSequence('clean', ['js', 'bower', 'plugins', 'css', 'html'], 'image', 'rev'));
//gulp.task('default', gulpSequence('clean', ['css', 'html'], 'rev'));

```

### package.json
```
{
  "name": "itopwx",
  "version": "1.0.0",
  "description": "",
  "main": "gulpfile.js",
  "dependencies": {
    "gulp": "^3.9.1"
  },
  "devDependencies": {
"babel-plugin-add-module-exports": "^0.2.1",//babel-1  三个配合使用
"babel-preset-es2015": "^6.24.1",//babel-2   三个配合使用
"gulp-babel": "^6.1.2",//babel-3   三个配合使用 ,否则会报错
"gulp": "^3.9.1",
"gulp-base64": "^0.1.3",
"gulp-clean": "^0.3.2",
"gulp-concat": "^2.6.1",
"gulp-cssimport": "^5.0.0",
"gulp-htmlmin": "^3.0.0",
"gulp-if": "^2.0.2",
"gulp-less": "^3.3.0",
"gulp-minify-css": "^1.2.4",
"gulp-rename": "^1.2.2",
"gulp-rev": "^7.1.2",
"gulp-rev-collector": "^1.1.1",
"gulp-sequence": "^0.4.6",
"gulp-strip-debug": "^1.1.0",
"gulp-uglify": "^2.1.2",
"gulp-useref": "^3.1.2"  
},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "robert",
  "license": "ISC"
}
```