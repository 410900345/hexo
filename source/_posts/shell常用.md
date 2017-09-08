---
title: shell常用
categories: 'tools'
date: 2017-09-08 14:15:03
tags:
---

1.shell 中判断字符串为空的正确方法

```
#!/bin/sh
STRING=
if [ -z "$STRING" ]; then 
    echo "STRING is empty" 
fi
if [ -n "$STRING" ]; then 
    echo "STRING is not empty" 
fi
```