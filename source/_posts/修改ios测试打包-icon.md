---
title: 修改ios测试打包 icon
categories: 'tools'
date: 2017-09-08 14:17:25
tags:
---

为了方便测试人,测试人员可以直接从icon上看到当前测试的版本和版本的发布时间,方便,同时在预上线和生成环境上不执行这个脚本,不显示 icon 信息等内容!
原理是在编译完成之后编辑编译后文件里面的appicon 内容!

最终的效果
![](http://dl2.iteye.com/upload/attachment/0092/6414/095e7fb8-efb6-3a57-8ca3-03e3d4e29921.png)
## 1.安装环境

```
brew install imagemagick
brew install ghostscript
```
ImageMagick为在命令行下操作图片提供了很多的功能，而ghostscript则是为了在icon上写的字体好看

## 2.配置脚本
在Target的Build Phases中添加一个Run Script的Build Phase

[脚本地址](https://github.com/sukeyang/IconOverlaying)


[参考链接1](http://merowing.info/2013/03/overlaying-application-version-on-top-of-your-icon/)

[参考链接2](http://ningandjiao.iteye.com/blog/1997117fo/2013/03/overlaying-application-version-on-top-of-your-icon/)

[参考链接3](http://zhoulingyu.com/2017/04/04/iOS%E2%80%94%E2%80%94%E5%86%99%E4%B8%80%E4%B8%AA%E5%BF%AB%E9%80%9F%E5%AE%9A%E4%BD%8D%E9%97%AE%E9%A2%98%E7%9A%84%E8%84%9A%E6%9C%AC/)