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

## 5 obj1.func.call(obj)方法
意思是将obj看成obj1,调用func方法

## 6 Array.prototype.slice.call()方法详解
arguments并不是真正的数组对象，只是与数组类似而已，所以它并没有slice这个方法，而Array.prototype.slice.call(arguments)可以理解成是让arguments转换成一个数组对象，让arguments具有slice()方法
Array.prototype.slice.call(arguments)能将具有length属性的对象转成数组
将函数的实际参数转换成数组的方法!
方法一：var args = Array.prototype.slice.call(arguments);

方法二：var args = [].slice.call(arguments, 0);

方法三：

var args = []; 
for (var i = 1; i < arguments.length; i++) { 
    args.push(arguments[i]);
}
[参考](http://blog.csdn.net/i10630226/article/details/49702375)

## 7.Javascript中apply、call、bind
javaScript 中，某个函数的参数数量是不固定的，因此要说适用条件的话，当你的参数是明确知道数量时用 call 。
而不确定的时候用 apply，然后把参数 push 进数组传递进去。当参数数量不确定时，函数内部也可以通过 arguments 这个伪数组来遍历所有的参数。
bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind() 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。
 