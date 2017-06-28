---
title: js基本用法(二)
categories: 'js'
date: 2017-02-10 18:12:03
tags:
---

### 常见类
1.Boolean 验证类的布尔值

	Boolean("")  false
	Boolean("123")  true
2.Number任何都转成number,toString加参数转换
	
	var n = Number("123")
	n.toString(2)  //1111011
3.String类对象方法

	test.toUpperCase();
	test.toLocaleLowerCase()
	test.indexOf("m",2) //返回某个指定的字符串值在字符串中2出现的位置。找不到为-1 
	test.charAt(0)

字符串的搜索用下面的方式
	
	if(test.indexOf ("c") == -1){
	alert("yes");
	}
substring()	提取字符串中两个指定的索引号之间的字符。
split()	把字符串分割为字符串数组。
concat()	连接两个或更多字符串，并返回新的字符串。
lastIndexOf()	从后向前搜索字符串。
4.math类常用数学常数
	
	Math.random()*100
	8*Math.random()+2  //2到10之间的某一个数	
	Math.round(Math.random()*10)  //四舍五人
	Math.ceil(Math.random()*10)  //取值
	Math.floor(Math.random()*10) //舍去
	Math.min(1,10) 取最小值
	Math.max(1,10) 取最大值
	Math.pow(2,4) 指数运算
	Math.sqrt(9); 平方根
5.Date类相关,不一个new则为当前日期

	new Date(2008,0,1)	//月从0开始计算 Tue Jan 01 2008 00:00:00 GMT+0800 (CST)
	dateTest.setMonth(2) //设置为3月
	dateTest.getMonth() // 2
	Date.parse("Jan 1,2009") //转为时间戳
	ateTest.getDay() //获取星期几 0为每星期的第一天
6.正则表达式

	var re = new RegExp("j.*t","gmi");	
	
修饰符	描述,一旦设置不能更改
i	执行对大小写不敏感的匹配。默认false
g	执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。默认false 
m	执行多行匹配 默认false

	var s = new String("HelloJavaScriptWorld");
	s.match(/a/); //匹配字符串
	s.search(/j.*a/i); //匹配字符串索引位置
	s.replace(/[A-Z]/g,''); //替换为空字符串
replace() 方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。()为分组匹配分组的第一组;这些函数还可以匹配普通字符串;
	
	var email = "stoyan@phpied.com";
	var username= email.replace(/(.*)@.*/,"$1");
	
	var callback = function(){ 
	glob = arguments;
	return arguments[1] +" at" + arguments[2] + " dot " + arguments[3];
	}
	"stoyan@phpied.com".replace(/(.*)@(.*)\.(.*)/, callback); //分组
	"stoyan atphpied dot com" 
	
	var csv = "one, two, three, four";
	csv.split(/\s*,\s*/); //空格匹配;
7.error错误捕捉,,自定义错误对象,

	try {
	idont();
	} catch (e) {
	alert(e.name + ': ' + e.message);
	}	
	
	try {
	var total = mybeE();
	if(total === 0) {
	throw new Error("division by zero");
	} else {
	alert(50/total);
	}
	} catch (e){
	alert(e.name + ': ' + e.message);
	}
	
### 重要的属性-原型
1.原型类似于父类的东西,gadget的父类gadget.prototype,可以增加属性,可以修改原型,然后影响原来的对象
	
	function gadget (name ,color) {
	this.name = name;
	this.color = color;
	this.whatAreYou = function () {
	return "i am a " + this.color + " " +this.name;
	}
	}			
	
	gadget.prototype = {
	price : 100,
	rating: 3,
	getInfo :function() {
	return "rating" + this.rating + "  price" + this.price;
	}
	}
2.对象自身属性没有找到指定的属性,会去原型里面继续查找,如果相同,以对象的属性为准;打印属性;
	
	for (var prop in newToy) {
	 console.log(prop + " = " + newToy[prop]);
	 	
newToy.hasOwnProperty属于自身的属性
	 	
	 for (var prop in newToy) {
	if(newToy.hasOwnProperty(prop)){
	console.log(prop + " = " + newToy[prop]);
	}}	
newToy.propertyIsEnumerable自身属性为true,原型中的为false;
monke是对象george的原型;

	monkey.isPrototypeOf(george);
3.prototype和_proto_属性不是等价的,prototype改变并不会影响到_proto_

	monkey.test = 1;
	developer.test; //修改monkey的属性,修改developer内容;
4.扩展内建函数常用Array,相当于iOS分类

	Array.prototype.inArray = function (needle) {
	for (var i = 0,len = this.length;i< len;i++){
	if (this[i] === needle) {
	return true;
	}
	}
	}	
5.判断函数是否可以使用,如果想添加一个属性或者方法最好看是不是已经存在其中;

	if (!String.prototype.reverse) {
	alert("1111");
	}
6.当我们重写某对象的prototype时候,重置相应的constructor是一个好习惯;		