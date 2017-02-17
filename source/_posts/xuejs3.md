---
title:  js基本用法(三)
categories: js
date: 2017-02-13 17:52:01
tags:
---
### 继承
1.js没有类的概念,只有对象,就是继承也是通过对象的方式;constructor类似于类初始化函数,
prototype 是个类的对象;
2.保持原型链路的基础上,对父类对象的属性隔离;保证重用;

	var F = function(){};
	F.prototype = TwoShape.prototype;
	Triangle.prototype = new F();
3.将uber属性设置成了指向其父级原型的引用;
	
	my.uber = TwoShape.prototype;
4.继承函数封装,具体原理不懂;
	
	function extend(Child,Parent) {
	var F = function(){};
	F.prototype = Parent.prototype;
	Child.prototype = new F;
	Child.prototype.constructor =  Child;
	Child.uber = Parent.prototype;

	extend(TwoShape,shape);//使用内容	
属性的拷贝为自身的,基本数据类型是创建新的,函数和数组都是值的引用;新创建相当于忘记之前的对象,重新生成一个对象;	
	
	function extend2(Child, Parent) {
	var p = Parent.prototype;
	var c = Child.prototype;
	for (var i in p ){
	c[i] = p[i];
	c.uber = p; 
		}
	}