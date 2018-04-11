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
<a href="{%}" class="anchorLink" onclick={*}>{%}<br /><span>{%}</span></a>{*}
</div>{*}
```

`解释`

`{%}`是替换我们要查看的内容比如 title, 时间,内容等,下一步会用到,按照模板进行替换就可以

`{*}`是替换任意代码的通配符,每行末尾和空白行也加上`{*}`

* Define extraction rules 我们输入,我们在下面输入,会按照内容继续解析
![截图2](https://img3.appinn.com/images/201305/2013-05-315-56-31.png/o)

* 再后面经过简单的设置，注意把第二个和第三个参数连起来：
![](https://img3.appinn.com/images/201305/2013-05-31-6-07.png/o)

*自制版本的 Feed 就成功了,会输出我们的内容

![](https://img3.appinn.com/images/201305/2013-05-31-6-09-10.png/o)

### 其他的订阅软件

[一览](http://www.yilan.io/home/)免费版最多可以订阅100个RSS源、10个微信公众号。

<!-- more -->

---------
[手把手教你制作 RSS 源](https://sspai.com/post/34320)

[为没有 Feed 的网页生成 RSS 格式](https://www.appinn.com/feed43/)

[rss_for_everything](https://github.com/xzonepiece/rss_for_everything)

<!--{% qnimg alfred.png title:配置 alt:preferrence 'class:class1 class2' extend:?imageView2/2/w/1400 %}-->