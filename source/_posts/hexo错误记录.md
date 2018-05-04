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

公司电脑是正确的

```
➜  hexo git:(develop) ✗ hexo -v
hexo: 3.3.7
hexo-cli: 1.0.3
os: Darwin 16.7.0 darwin x64
http_parser: 2.6.0
node: 5.2.0
v8: 4.6.85.31
uv: 1.7.5
zlib: 1.2.8
ares: 1.10.1-DEV
icu: 56.1
modules: 47
openssl: 1.0.2e

➜  hexo git:(develop) ✗ npm ls --depth 0
hexo-site@0.0.0 /Users/hl/hexo
├── g@2.0.1 extraneous
├── hexo@3.3.7
├── hexo-deployer-git@0.2.0
├── hexo-generator-archive@0.1.4
├── hexo-generator-baidu-sitemap@0.1.2
├── hexo-generator-category@0.1.3
├── hexo-generator-feed@1.2.0
├── hexo-generator-index@0.2.0
├── hexo-generator-search@1.0.3
├── hexo-generator-searchdb@1.0.3
├── hexo-generator-sitemap@1.1.2
├── hexo-generator-tag@0.2.0
├── hexo-qiniu-sync@1.4.7
├── hexo-renderer-ejs@0.2.0
├── hexo-renderer-marked@0.2.11
├── hexo-renderer-stylus@0.3.1
└── hexo-server@0.2.0

```

### 4.相关错误

```
$ hexo g
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path) [Line 7, Column 23]
Error: Unable to call `the return value of (posts["first"])["updated"]["toISOString"]`, which is undefined or falsey
```

当移除掉插件hexo-generator-feed和hexo-generator-sitemap后错误消失，怀疑该插件与hexo兼容性不好

```
$npm uninstall hexo-generator-feed
$npm uninstall hexo-generator-sitemap
```

[相关代码](https://github.com/hexojs/hexo-generator-feed/issues/43)