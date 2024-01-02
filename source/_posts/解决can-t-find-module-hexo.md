---
title: 解决“can't find module 'hexo'”
abbrlink: 19721
date: 2022-03-20 16:18:16
tags: BUG
categories: 问题
cover: https://picsum.photos/id/515/300/300
---

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/`1JU_}O2G0C%$9G)
解决方法：

```
 $ npm install hexo --no-optional
 if it doesn't work 
  try
 $ npm uninstall hexo-cli -g
 $ npm install hexo-cli -g
```

或者

```
$ cnpm install hexo --no-optional
if it doesn't work
try
$ cnpm uninstall hexo-cli -g
$ cnpm uninstall hexo-cli -g
```
接着cnpm install安装一下hexo博客所需的依赖包

