---
title: weex使用介绍
categories: 'BFE'
date: 2017-02-17 11:38:28
tags:
---

   最近在折腾weex,不过升级到vue2.0出现了一些问题,现在记录使用情况,暂时有一些问题没有解决,官方的链接:
   
[weex官方github](https://github.com/alibaba/weex)   

[weex-devtool-iOS](https://github.com/weexteam/weex-devtool-iOS/blob/master/README-zh.md)
   
[weexteam-demo](https://github.com/weexteam/weex-hackernews/)
###基本介绍
1.安装环境,nodejs,下面是一些常用的命令.

IDE: Sublime Text + [vue-syntax-highlight](https://github.com/vuejs/vue-syntax-highlight)

```
npm install
npm install -g weex-toolkit@beta
npm run build
npm run copy:ios
```
2.开启服务


```
npm run serve
```
3.开启debug,自动弹出页面

```
weex debug --verbose
```