---
title: 更新next主题
categories: '小技巧'
date: 2018-01-10 16:30:22
tags:
---

## 1.增加404腾讯公益配置
按照配置说明，新建 404.html 文件，放在主题 next 的 source 文件夹根目录下，配置文件 _config.yml 中
信息如下：

```
menu:
  home: / || home
  about: /about/ || user
  commonweal: /404.html || heartbeat
```
<!-- more -->

## 2.“Updates were rejected because the tag already exists” when attempting to push in SourceTree

tag 已经存在，使用下面命令进行提交，覆盖,一次获取所有新增的标签，进行覆盖

```
git pull --tags
```

## 3.Github 上怎样把新 commits 使用在自己的 fork 上
首先要先确定一下是否建立了主repo的远程源：

```
git remote -v
```

如果里面只能看到你自己的两个源(fetch 和 push)，那就需要添加主repo的源：
URL为原来repo的源

```
git remote add upstream URL
git remote -v
```

然后你就能看到upstream了。

如果想与主repo合并：

```
git fetch upstream
git merge upstream/master
```

## 4.Mac如何关闭指定port

查询 port 对应的 pid

```
lsof -i: port
```

关闭 pid

```
sudo kill -9 pid

```


[参考地址 next](http://theme-next.iissnan.com/theme-settings.html#volunteer-404)

[stackoverflow](https://stackoverflow.com/questions/31929667/updates-were-rejected-because-the-tag-already-exists-when-attempting-to-push-i)

[Github 上怎样把新 commits 使用在自己的 fork 上](https://www.zhihu.com/question/20393785/answer/30725725)

[Git 基础](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)


<!--{% qnimg alfred.png title:配置 alt:preferrence 'class:class1 class2' extend:?imageView2/2/w/1400 %}-->