---
title: git
date: 2016-09-24 11:22:07
tags: bower
---

###  gitlab创建公钥
- `  ssh-keygen -t rsa -C "your.email@example.com" -b 4096`
-` https://gitlab.com/help/ssh/README`

### 移除origin
-`$ git remote rm origin`


### Command line instructions

#### Git global setup

- git config --global user.name "xxxx"
- git config --global user.email "xxxxx@xx.com"

#### Create a new repository

- git clone git@gitlab.com:xxxx/weixinnode.git
- cd weixinnode
- touch README.md
- git add README.md
- git commit -m "add README"
- git push -u origin master

#### Existing folder

- cd existing_folder
- git init
- git remote add origin git@gitlab.com:xxxx/xxxx.git
- git add .
- git commit
- git push -u origin master

#### Existing Git repository

- cd existing_repo
- git remote add origin git@gitlab.com:xxxx/xxxx.git
- git push -u origin --all
- git push -u origin --tags
- 来源： https://gitlab.com/xxxx/xxxx

### 回滚
- `git reset --hard <commit ID号> `

### 强制覆盖本地
- ` git fetch --all  
git reset --hard origin/master 
git pull`

- git clone 远程分支
Git clone只能clone远程库的master分支，无法clone所有分支，解决办法如下：
1. 找一个干净目录，假设是git_work
2. cd git_work
3. git clone http://myrepo.xxx.com/project/.git ,这样在git_work目录下得到一个project子目录
4. cd project
5. git branch -a，列出所有分支名称如下：
remotes/origin/dev
remotes/origin/release
6. git checkout -b dev origin/dev，作用是checkout远程的dev分支，在本地起名为dev分支，并切换到本地的dev分支
7. git checkout -b release origin/release，作用参见上一步解释
8. git checkout dev，切换回dev分支，并开始开发。
