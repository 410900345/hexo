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

- 其他命令

```
yarn list [package]
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

## 4. Object.defineProperty

```
  var a= {}
    Object.defineProperty(a,"b",{
      value:123
    })
    console.log(a.b);//123
```
它接受三个参数都是必填的。。

传入参数
第一个参数:目标对象

第二个参数:需要定义的属性或方法的名字。

第三个参数:目标属性所拥有的特性。（descriptor）

前两个参数不多说了，一看代码就懂，主要看第三个参数descriptor，看看有哪些取值

descriptor
他又以下取值，我们简单认识一下，后面例子，挨个介绍，

value:属性的值(不用多说了)

writable:如果为false，属性的值就不能被重写,只能为只读了

configurable:总开关，一旦为false，就不能再设置他的（value，writable，configurable）

enumerable:是否能在for...in循环中遍历出来或在Object.keys中列举出来。