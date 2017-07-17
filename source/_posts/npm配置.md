---
title: npm配置
date: 2016-08-24 20:14:00
tags: npm
---

## npm配置
```
access = null
also = null
always-auth = false
bin-links = true
browser = null
ca = null
cache = "C:\\Users\\robert\\AppData\\Roaming\\npm-cache"
cache-lock-retries = 10
cache-lock-stale = 60000
cache-lock-wait = 10000
cache-max = null
cache-min = 10
cafile = undefined
cert = null
color = true
depth = null
description = true
dev = false
dry-run = false
editor = "notepad.exe"
engine-strict = false
fetch-retries = 2
fetch-retry-factor = 10
fetch-retry-maxtimeout = 60000
fetch-retry-mintimeout = 10000
force = false
git = "git"
git-tag-version = true
global = false
global-style = false
globalconfig = "C:\\Program Files\\nodejs\\etc\\npmrc"
globalignorefile = "C:\\Program Files\\nodejs\\etc\\npmignore"
group = 0
heading = "npm"
https-proxy = null
if-present = false
ignore-scripts = false
init-author-email = ""
init-author-name = ""
init-author-url = ""
init-license = "ISC"
init-module = "C:\\Users\\robert\\.npm-init.js"
init-version = "1.0.0"
json = false
key = null
legacy-bundling = false
link = false
local-address = undefined
loglevel = "warn"
; long = false (overridden)
maxsockets = 50
message = "%s"
node-version = "6.10.3"
npat = false
onload-script = null
only = null
optional = true
parseable = false
prefix = "C:\\Program Files\\nodejs"
production = false
progress = true
proprietary-attribs = true
proxy = null
rebuild-bundle = true
registry = "https://registry.npmjs.org/"
rollback = true
save = false
save-bundle = false
save-dev = false
save-exact = false
save-optional = false
save-prefix = "^"
scope = ""
searchexclude = null
searchopts = ""
searchsort = "name"
shell = "C:\\Windows\\system32\\cmd.exe"
shrinkwrap = true
sign-git-tag = false
strict-ssl = true
tag = "latest"
tag-version-prefix = "v"
tmp = "C:\\Users\\robert\\AppData\\Local\\Temp"
umask = 0
unicode = false
unsafe-perm = true
usage = false
user = 0
; user-agent = "npm/{npm-version} node/{node-version} {platform} {arch}" (overridden)
userconfig = "C:\\Users\\robert\\.npmrc"
version = false
versions = false
viewer = "browser"

```

## npm install 只安装dependencies


```bash
linux & mac: export NODE_ENV=production

windows: set NODE_ENV=development //默认值 production为不下载dev
```


```
export NODE_ENV=production
npm install --save
```

## 切换源 $ npm install -g cnpm --registry=https://registry.npm.taobao.org
 
### request
 
- 发送请求(https://www.npmjs.com/package/request)
 
### nodemon
 
- npm install -g nodemon(服务端程序修改后自动重启)
 
### cheerio
 
- 操作字符串像dom一样
 
### browser-sync
 
- 浏览器开发软件间同步
 
### bower
- npm install -g bower
- 静态js文件管理器,解决依赖问题, 例如bootstrap依赖于jQuery,在下载bootsrap时会同时下载jQuery
- bower install jquery#1.7.2  (下载指定版本)
- bower uninstall jquery(删除,卸载)
- bower search jquery(查找资源信息)
- bower init (初始化,用来记录资源信息及依赖)
- bower info jquery(查看jquery历史版本)
 
### Linux 常用指令
- rm -rf 文件夹名称
 
### node 后台启动
- nohup node app.js &
 
### 查看node后台进程
- ps -ef | grep node
 
### rem布局
- 24/32*rem =为所求
 
#### 浏览器同步刷新
- 改了js代码之后，能够自动刷新！
- 安装:`npm install browser-sync -g `
- 使用:打开命令行工具`browser-sync start --server  --files "./*.html,./*.css"`(备注1)
- 匹配当前文件夹下的全部文件`browser-sync start --server --files "./**/*.html,./**/*.css"`
- 这条命令可以在任何目录下打开,后面的文件跟的是要监听的文件的路径,'*'代表统配所有的css问价挥着html文件
- 输入以上命令后浏览器会自动调出,地址栏会自动显示http://localhost:3000
- 在http://localhost:3000 后面补全你要监听的文件,假如监听的文件是str.html,即地址栏输入:http://localhost:3000/str.html
- 备注1
    + 如果觉得命令长可以使用如下方法(会话级别,)
    + 打开bash ,执行如下命令 `alias bwsync='browser-sync start --server  --files "./*.html,./*.css"'`
    + 成功后执行`bwsync`就可以启动服务,此命令与` browser-sync start --server  --files "./*.html,./*.css" `相同
    + 执行 `type bwsync`  (bwsync属于自定义命令缩写可以改成自己喜欢的,但是使用之前先执行` type 自定义指令` )
 
- 配置地址 
    + UI: http://localhost:3001
    + UI External: http://192.168.0.113:3001
 
#### npm install 名称 --save-dev 
- 会在package.json中记录

#### npm 查看已经全局安装的包
- `npm install -g cnpm --registry=https://registry.npm.taobao.org`
- `npm install -g bower express-generator gulp nodemon webpack grunt-cli yo nrm vue-cli mocha browser-sync eslint hexo-cli electron`
- npm list -g --depth 0
```
+-- bower@1.8.0
+-- cnpm@4.5.0
+-- express-generator@4.15.0
+-- generator-webapp@2.4.1
+-- grunt-cli@1.2.0
+-- gulp@3.9.1
+-- mocha@3.4.1
+-- nodemon@1.11.0
+-- npm@3.10.10
+-- nrm@1.0.2
+-- vue-cli@2.8.2
+-- webpack@2.6.0
+-- yo@1.8.5
+-- electron@  //打包桌面
```
 
### npm 显示安装进度

- ` npm config set loglevel=http`

#### git命令
- 使用`git add * ` 和` git add .` 是有区别的
   +  `git add * ` 会导致已经删除的文件不能正常更新
   + ` git add .`  会把工作区的所有变化提交到暂存区
 

#### 安装express 
```
express 已经把命令行工具分离出来了…

如果你要 Express 3

sudo npm install -g express-generator@3

express 4 的话

sudo npm install -g express-generator

```

# 微信调试
### localtunnel npm 模块
- 域名映射,不能自定义域名 , 

### ngrok 域名映射

### utralhook 域名映射

### QQ浏览器 
- 微信调试
- 

### iconv-lite
- 转码