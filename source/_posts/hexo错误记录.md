---
title: hexo错误记录
categories: 小技巧
date: 2017-06-28 10:38:46
tags:
---

常见问题使用帮助

[官方 http://hexo.io/docs/troubleshooting.html]( http://hexo.io/docs/troubleshooting.html)

[hexo-issues-geithub](https://github.com/hexojs/hexo/issues)

### 1.错误代码

```
hexo generate fail - Template render error: (unknown path)
```
* 检查代码`"\{\{ \}\}"`改成`"\{\{ \}\}"`,前面的去掉`\`是,这里为了保证输入正确
* 检查代码`"\{\%\}"`改成`"\{\%\}"`
* 删除多余的换行

### 2.错误代码

Module version mismatch. Expected 48, got 47
重新安装一下

```
sudo npm install hexo --no-optional
```
### 3.两个电脑上配置问题

ERROR Local hexo not found in ~/hexo_blog
ERROR Try running: 'npm install hexo --save'

使用node 6.14.2 和删掉 nodemodles 文件夹
```
nvm install 6.14.2
```


### 4.升级NexT v6.0.0以上
下载新版本到`themes`把文件夹改名为`next`

### 5.Cannot find module 'hexo-util'

重新安装

```
npm install -- save-dev hexo-util
```

切换到`master`分支进行提交部署`hexo d`


### 5.hexo长时间未升级导致，执行错误
新建文件夹，执行新的hexo命令来，把新的文件复制到里面里面保证新的格式正确

