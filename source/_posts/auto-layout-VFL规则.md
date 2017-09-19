---
title: auto layout VFL规则
categories: 'ios'
date: 2017-09-01 16:12:40
tags:
---

在使用 Auto Layout 时，首先需要将视图的 setTranslatesAutoresizingMaskIntoConstraints属性设置为 NO。这个属性默认为 YES。当它为 YES 时，运行时系统会自动将 Autoresizing Mask 转换为 Auto Layout 的约束，这些约束很有可能会和我们自己添加的产生冲突。

### 1.常用api

#### 1).NSLayoutConstraint API

```
NSLayoutConstraint
+ (NSArray *)constraintsWithVisualFormat:(NSString *)format options:(NSLayoutFormatOptions)opts
metrics:(NSDictionary *)metrics
views:(NSDictionary *)views;
```

参数介绍:

format:此参数为你的vfl语句，比如:@"H:|-[button]-|"

opts:枚举参数，默认写0，具体跟据你所实现的需求去选择你想要的枚举

metrics:这里是一个字典，当在format中使用了动态数据比如上现这句:@"H:|-[button(==width)]-|",表示这个button的宽度为width,那么这个参数去哪里找呢？就是在这个字典里面找到key对就的值，如果没有找到这个值，app就会crash.

views:顾名思义，这是传所有你在vfl中使用到的view，那在上面这句例子中的应该怎么传呢？结果是这样的：NSDictionaryOfVariableBindings(button).如果你使用到了多个view，就可以这样NSDictionaryOfVariableBindings(button,button1,button3...),这个名字也要跟参数format中的一一对应，缺一不可.

#### 2).+(instancetype)constraintWithItem:(id)view1 attribute:(NSLayoutAttribute)attr1 relatedBy:(NSLayoutRelation)relation toItem:(nullable id)view2 attribute:(NSLayoutAttribute)attr2 multiplier:(CGFloat)multiplier constant:(CGFloat)c;

前三个和被约束的视图有关，后四个和他的父视图有关。这个方法连起来可以翻译如下：view1的某个属性（attr1）等于view2的某个属性（attr2）的值的多少倍（multiplier）加上某个常量（constant）。描述的是一个view与另外一个view的位置和大小约束关系。其中属性attribute有上、下、左、右、宽、高等，关系relation有小于等于、等于、大于等于。需要注意的是，小于等于 或 大于等于 优先会使用 等于 关系，如果 等于 不能满足，才会使用 小于 或 大于。例如设置一个 大于等于100 的关系，默认会是 100，当视图被拉伸时，100 无法被满足，尺寸才会变得更大。

如果是设置view自身的属性，不涉及到与其他view的位置约束关系。比如view自身的宽、高等约束时，方法constraintWithItem:的第四个参数view2（secondItem）应设为nil；且第五个参数attire（secondAttribute）应设为NSLayoutAttributeNotAnAttribute 。
在设置宽和高这两个约束时，relatedBy参数使用的是 NSLayoutRelationGreaterThanOrEqual，而不是 NSLayoutRelationEqual。因为 Auto Layout 是相对布局，所以通常你不应该直接设置宽度和高度这种固定不变的值，除非你很确定视图的宽度或高度需要保持不变。

### 2.举个栗子

```
NSArray *constraints1=[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-[button]-|"
　　　　　　　　　　　　　　　　　　　　　　　　　options:0
　　　　　　　　　　　　　　　　　　　　　　　　　metrics:nil
　　　　　　　　　　　　　　　　　　　　　　　　　views:NSDictionaryOfVariableBindings(button)];
```
说明
H:"是表示这是水平方向上的约束，

"|"是表示superView，

"-"表示一个间隔空间，这个间隔如果是如superView之间的，那么就是20px,如果是两个同级别的view，比如@"[button]-[button1]"，那么这里表示的是8px.

```
NSArray *constraints2=[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-20-[button(==30)]"
　　　　　　　　　　　　　　　　　　　　　　　　　options:0
　　　　　　　　　　　　　　　　　　　　　　　　　metrics:nil
　　　　　　　　　　　　　　　　　　　　　　　　　views:NSDictionaryOfVariableBindings(button)];
```
说明
V:"中代表这是垂直方向上的约束,

"|-20-"这里的意思就是距离头部为20px，相当于y坐标为20。

后面的"[button(==30)]"，是指定这个button的高度为30px.y坐标固定

### 3.总结
三：最后对格式的字符串作一个总结介绍

功能　　　　　　　　表达式

水平方向  　　　　　　  H:

垂直方向  　　　　　　  V:

Views　　　　　　　　 [view]

SuperView　　　　　　|

关系　　　　　　　　　>=,==,<=

空间,间隙　　　　　　　-

优先级　　　　　　　　@value

[参考地址](http://www.cnblogs.com/wupei/p/4150626.html)
[链接：](http://www.jianshu.com/p/d1ddedee832f)