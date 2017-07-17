---
title: bower配置
date: 2016-02-24 09:14:37
tags: bower
---

### 指定bower配置

1. 创建文件名为`.bowerrc` 的文件 , 放在根目录下
2.  文件内容
```
{
  "directory": "bower_components",  //指定文件路径
  "registry": "http://bower.herokuapp.com",   // 指定加载仓库
  "strict-ssl": false  // 防止被墙
}

```