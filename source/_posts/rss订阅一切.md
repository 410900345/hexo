---
title: RSS 订阅一切
categories: 'tools'
date: 2018-04-11 17:23:40
tags:
---

本人使用 RSS 订阅信息流,查看相应的文章,但是由于一些 Blog或者简书等内容不支持 RSS, 尝试自己生成 feed 链接.

### 具体步骤
* RSS 订阅软件[inoreader](https://www.inoreader.com)特点是无订阅上限,缺点是需要翻墙使用.

* [Feed43](http://feed43.com/feed.html?name=2441323566728440)可以为静态网站制作RSS.

* 首先输入页面地址：http://love.appinn.com，点击 Reload，就能看到页面代码了。
![截图1](https://img3.appinn.com/images/201305/2013-05-31_5-54-24.png/o)
替换成

```
<div class="n1">{*}
<a href="\{\%\}" class="anchorLink" onclick={*}>\{\%\}<br /><span>\{\%\}</span></a>{*}
</div>{*}
```

`解释`

`\{\%\}`是替换我们要查看的内容比如 title, 时间,内容等,下一步会用到,按照模板进行替换就可以

`{*}`是替换任意代码的通配符,每行末尾和空白行也加上`{*}`

* Define extraction rules 我们输入,我们在下面输入,会按照内容继续解析
![截图2](https://img3.appinn.com/images/201305/2013-05-315-56-31.png/o)

* 再后面经过简单的设置，注意把第二个和第三个参数连起来：
![](https://img3.appinn.com/images/201305/2013-05-31-6-07.png/o)

*自制版本的 Feed 就成功了,会输出我们的内容

![](https://img3.appinn.com/images/201305/2013-05-31-6-09-10.png/o)

### 安装RSS Subscription Extension插件
在Chrome中使用RSS服务，可以安装一个RSS Subscription Extension的插件，快捷添加 RSS 订阅源到指定的订阅服务.

* 点击图标进入RSS Subscription Extension
![](https://raw.githubusercontent.com/tiomke/TempPics/master/RSS%E8%AE%A2%E9%98%85%E6%9C%8D%E5%8A%A1%E7%9A%84%E4%BD%BF%E7%94%A8/%E8%AE%A2%E9%98%85%E6%9C%8D%E5%8A%A1.png)

* 点击管理,添加相应的订阅源
![](https://raw.githubusercontent.com/tiomke/TempPics/master/RSS%E8%AE%A2%E9%98%85%E6%9C%8D%E5%8A%A1%E7%9A%84%E4%BD%BF%E7%94%A8/%E9%80%89%E9%A1%B9%E8%AE%BE%E7%BD%AE.png)

在RSS订阅选项设置页面中点击添加，在编辑供稿阅读器中加入说明和网址`http://www.inoreader.com/?add_feed=%s`。

<!-- more -->
### 其他的订阅软件

[一览](http://www.yilan.io/home/)免费版最多可以订阅100个RSS源、10个微信公众号。

### 替换模板，删掉里面的\
* github.io 等 blog,根据实际博客样式情况,进行替换，

```
</a>{*}
{*}
</h1>{*}
{*}
<div class="post-meta">{*}
<time {*}
content="\{\%\}" >{*}
{*}
</time>{*}
</div>{*}
```
解析完后内容

```
\{\%1\} = 
\{\%2\} = http://xxx.html/
\{\%3\} = 
\{\%4\} = xxx
\{\%5\} = 
\{\%6\} = 
\{\%7\} = 
\{\%8\} = 2017-09-24
\{\%9\} = 09-24
```

取出的内容

```
title 为 \{\%4\} \{\%8\}
link 为 \{\%2\}
titlecontent 为 \{\%4\}
```

* 简书等内容的模板

```
<div class="content">{*}
<div class="author">{*}
{*} <span class="time" data-shared-at="\{\%\}"></span>{*}
</div>{*}
</div>{*}
<a class="title" target="_blank" href="\{\%\}">\{\%\}</a>{*}
<p class="abstract">{*}
\{\%\}
</p>{*}
<div class="meta">{*}
```
解析完后内容

```
\{\%1\} = xxx
\{\%2\} = 2017-08-22T22:06:41+08:00
\{\%3\} = https://www.jianshu.com/p/xxx
\{\%4\} = ixxx
\{\%5\} = xxx

```
取出的内容

```
title 为 \{\%4\} \{\%2\}
link 为 \{\%3\}
titlecontent 为 \{\%5\}
```
* 掘金个人下面的专栏模板

```
<div data-src="\{\%\}" {*}>\{\%\}</span></a></div><span class="date" data-v-36108f72>\{\%\}</span></div><!----><div class="row abstract-row" data-v-36108f72><a href="\{\%\}" target="_blank" rel="" st:name="title" class="title" data-v-36108f72>\{\%\}</a><a href="\{\%\}" target="_blank" rel="" st:name="abstract" class="abstract" data-v-36108f72>\{\%\}</a>
```
解析完后内容

```
\{\%1\} = xxx
\{\%2\} = xxx
\{\%3\} = 4月前
\{\%4\} = https://juejin.im/post/xxx
\{\%5\} = xxx）
\{\%6\} = https://juejin.im/post/xxx
\{\%7\} = 
```

```
title 为 \{\%5\} \{\%3\}
link 为 \{\%4\}
titlecontent 为 \{\%7\}
```

* 微信公众号订阅
[传送门](http://chuansong.me/)


---------
[手把手教你制作 RSS 源](https://sspai.com/post/34320)

[为没有 Feed 的网页生成 RSS 格式](https://www.appinn.com/feed43/)

[rss_for_everything](https://github.com/xzonepiece/rss_for_everything)

[安装RSS Subscription Extension插件](https://www.jianshu.com/p/a589bce7d7cf)

<!--{% qnimg alfred.png title:配置 alt:preferrence 'class:class1 class2' extend:?imageView2/2/w/1400 %}-->