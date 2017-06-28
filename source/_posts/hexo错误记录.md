---
title: hexo错误记录
categories: 小技巧
date: 2017-06-28 10:38:46
tags:
---

常见问题使用帮助,[官方 http://hexo.io/docs/troubleshooting.html]( http://hexo.io/docs/troubleshooting.html)

## 1.错误代码

```
hexo generate fail - Template render error: (unknown path)
```
* 检查代码`"{{ }}"`改成`"{/{ }/}"`
* 删除多余的换行