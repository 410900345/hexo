---
title: 使用Sublime Text 进行Markdown 编辑
categories: 'tools'
date: 2016-12-18 15:36:25
tags:
---

## 安装包管理器
同时按下ctrl+"`",将会在窗口底部出现一个小控制台，下面代码粘贴到控制台的编辑栏里：

```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

## 安装我们要用到的插件

```
Markdown Editing // Markdown编辑和语法高亮支持 
Markdown Preview// Markdown导出html预览支持
```

## 插件配置
1.在设置里面Sublime Text -- >preference--> key bunding user 	输入

```
[
    {"keys": ["alt+r"], "command": "markdown_preview", "args": { "target": "browser"}}
]
```
然后按住alt + r ，预览你编辑的文件吧。