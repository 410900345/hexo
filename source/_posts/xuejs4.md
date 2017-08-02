---
title:  js基本用法(四)
categories: 'js'
date: 2017-02-13 17:52:01
tags:
---

## 1.'use strict';  
- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。

[Javascript 严格模式详解](http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html)

## 2.yarn的用法,[官网](https://yarnpkg.com/zh-Hans/docs/usage)

- 安装
```
npm install --save 等于 yarn add
npm install 等于 yarn 
```

[地址](https://shenbao.github.io/ishehui/html/%E6%9D%82%E8%B0%88/Facebook%20%E5%BC%80%E6%BA%90%E7%9A%84%20Yarn%20%E6%96%B0%E5%9E%8B%E5%8C%85%E7%AE%A1%E7%90%86%E5%B7%A5%E5%85%B7.html)

- 移除依赖包

```
yarn remove [package]
```

- 升级依赖包

```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```

- 更换淘宝镜像

```
yarn config get registry
# -> https://registry.yarnpkg.com
yarn config set registry 'https://registry.npm.taobao.org'
```

## 3. props和state

- 永远都不要给 props 直接赋值,外面传递
- 永远都不要给 state 直接赋值，通过 setState
用this.setState() 会触发数据流变动重新调用 render 函数,用this.state.value不会，应该是setState()函数里面有某些hook钩子函数。
异步方法,里面有设置完成的回调函数
