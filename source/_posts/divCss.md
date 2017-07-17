---
title: divCss
date: 2014-05-24 22:14:37
tags: div Css
---

### 不清边距会导致滚动条
```
body,html{
   padding:0;
   margin:0;
}
body,html {
            height: 100%;
            background-color: green;
  }

```

### 永远不要使用a标签做按钮
- bootstrap中当<a></a>被点击的时候会focus,bootstrap中会对a:focus  的bgc:#2e6da4

### css样式表 优先级
- 行内样式>内联样式表>外联样式表

### a标签不能嵌套chrome会解析成并列的结构

### 禁止选中文本

```

.noselect {
-webkit-touch-callout: none; /* iOS Safari */
-webkit-user-select: none; /* Chrome/Safari/Opera */
-khtml-user-select: none; /* Konqueror */
-moz-user-select: none; /* Firefox */
-ms-user-select: none; /* Internet Explorer/Edge */
user-select: none; /* Non-prefixed version, currently
not supported by any browser */
}
来源： http://www.divcss5.com/rumen/r17062.shtml

```

### 禁止页面缓存

```
<meta http-equiv="Pragma" content="no-cache">
<meta http-equiv="Cache-Control" content="no-cache">
<meta http-equiv="Expires" content="0">
```