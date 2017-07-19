---
title: node 入门
date: 2016-10-02 22:00:00
tags: node
---

### 创建分支
  - 命令:`git branch [分支名]`
    + 创建一个新分支
  - 命令:`git branch`
    + 查看当前所有的分支

### 切换分支
  - 命令:`git checkout [分支名]`
    + 切换分支后可以在切换后的分支中进行正常的操作

### 合并分支
  - 命令:`git merge [分支名]`
    + git会将指定的分支合并到当前分支.

### 删除分支
  - 命令:`git branch -d [分支名]`
    + 删除指定分支，-d参数表示要执行删除操作

### git提交中的冲突
  - 如果git不能自动合并分支，就会有冲突，我们需要手动解决冲突，然后再次提交


## github
推荐网站 http://www.crx4chrome.com/
### github与git
  - git 版本管理工具
  - github 就是一个网站，只是这个网站提供git服务器的功能


### 上传代码到git服务器(push)
  - 命令:`git push [远程服务器地址] [远程服务器的分支]`
     + 示例:`git push https://github.com/huoqishi/test002.git master`

  - 上传时可以使用一些简化的命令
    + 将远程服务器地址写成变量的形式
      * `git remote add [变量名]  [远程服务器地址]`
      * 示例:`git remote add origin https://github.com/huoqishi/test002.git`
      * 这样之后就可以直接使用origin来代替git push 后面写的地址了
        `git push origin master`
  - 还可以尽一步简化
    + 在push时加上-u参数，就会默认建立本地当前分支与远程指定分支的关联,下一次push时就不需要输入分支名了`git push origin`;



## git使用ssh方式上传代码与github
  - SSH
    SSH是一种网络协议，用于计算机之间的加密登录。
  - 对称加密&非对称加密&不可逆加密
    对称加密：一个钥匙开一把锁
    非对称加密：公钥和私钥  公钥加密 私钥解密
    不可逆加密：多用于密码的加密


  - git生成公钥和私钥
    + 命令:`ssh-keygen -t rsa`生成的公钥与私钥文件会在当用户目录的.ssh目录下.
### 把代码push到服务器时需要先pull一下
  - 在pull之后如果远程的代码与本地的代码有冲突，git会先自动合并冲突，如果不能自动合并，就必需我们手动去处理冲突。

### 从服务器上pull代码到本地
  - 如果本地没有.git目录，需要先初始化一下。
  - 命令:`git pull [远程服务器地址] [远程的分支]`

### gh-pages分支-搭建博客.

  - 需要把自已博客的网页代码上传到github上的gh-pages分支
  - 然后就直接访问了
    + 访问的url形式: [github用户名].github.io/[仓库的名字]/[具体的页面]

- 流程 
git init
git add *
git commit -m ""
git branch gh-pages
git checkout gh-pages
git push [远程服务器地址] gh-pages

## Markdown

> 专注写作，提高生产力

### Markdown 介绍

轻量级标记语言（html、xml），2004 年被 `John Gruber` 创造，
它允许人们“使用易读易写的纯文本格式编写文档”，
Markdown 最重要的设计就是可读性，
Markdown 可以选择性的转换为 HTML 文档格式，
很多网站目前都使用了 Markdown 或者其变种，例如Github、简书等大型社区。
### Markdown 的优点

- 纯文本，所以兼容性极强，可以用所有文本编辑器打开
- 专注于文字写作而不是排版
- 格式转换方便，可以轻松转换为 HTML、PPT、电子书等
- Markdown 标记语法简单好记，可读性强

### 实时预览编辑器

[月光博客 - 好用的Markdown编辑器一览](http://www.williamlong.info/archives/4319.html)

编辑实时预览工具只是为了辅助教学而已，
我们真正在进行写作的时候，其实是不需要实时预览的，
因为 Markdown 标记语言本身已经足够清晰了。

### Markdown 基本语法

- 标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题 
- 代码块
> 这里是代码块
- 字体
他是最可爱的人*雷锋*（斜体）
他是最可爱的人_雷锋_ （斜体）
他是最可爱的人**雷锋**（加粗）
他是最可爱的人 __雷锋__（加粗）
- 无序列表
  * Candy.
  * Gum.
  * Booze.
  > 加号：
  + Candy.
  + Gum.
  + Booze
  > 减号
  - Candy.
  - Gum.
  - Booze.


- 链接

[github地址](https://github.com/KingNigel)


- 图片

![路飞](pic/1.jpeg)


- 代码引用

``` javascript
var a=123;
for (var i=0;i<10;i++){
}

```

- 表格

|姓名|性别|籍贯|
| ----|-----|-----|
|老赵|男 |河北|
|老朱|女|湖南|
|老段|未知|火星|

### sourceTree , tortoiseGit


### npm
  - 官网[https://www.npmjs.com]
  - node package manager
  - 命令:
    + 初始化:`npm init`
    + 安装指定包:`npm install jquery --save`
    + 删除指定包:`npm remove jquery --save`
    + 下载安装package.json中dependencies属性对的文件:`npm install --production`

### browser-sync
  - 更改代码之后自动刷新浏览器
  - 需要使用npm进行全局安装:`npm install browser-sync -g`,-g表示安装到全局
  - 使用:`browser-sync start --server --files "./index.html,app.css,./css/*.css,*.*" `
  - --files参数指定要监视的文件，后面跟要监视的文件的文件路径以逗号分隔。

