---
title: js基本用法(一)
categories: js
date: 2017-02-10 18:12:00
tags:
---
### 基本用法
1.不用new的话,this会变成全局变量

	function Hero(name) { this.name = name ;};
	var h1 = Hero("ceshi");
2.大小写严格
3.Infinity 超出处理范围的数值 1e309,
4.NaN依旧是number,typeof NaN可以查看,特殊数字
5.数字字符串做运算,会当成数字类型使用,转换失败就是NaN,偷懒做法是1*s转换成数字,
	
	var s = "1";s = 3*s
	var s = "100";s = 1*s
	var s = "1avbc";s = 3*s
加法不适用
	
	var s = "1";s += 3	
6.加法是用来把数字转成字符串,取巧的方式

	var s = "1";s += 3	
7.空字符串"",null,undefined,0,NaN,false都是false
8.===等价运算

	1 === '1'	false
!== 不能价运算 	

	NaN == NaN  false
9.undefined为不存在或者未经过赋值的变量,和nul在转换基本类型时有区别
	
	"" + null        "null"
	"" + undefined   undefined
### 数据操作
1.数组操作

	delete a[1]	
	length属性为太长自动填充	undefined
	a.push("last")	 //添加到最后
  	a.pop()   //删掉最后
  	a.sort()  //排序
  	a.join("is ")  //连接"1is is is "
  	a.slice(1,2)  //查看
  	a.splice(1,2,100,200,300) //删掉并添加新的[1, 100, 200, 300, undefined × 1]
  	
2.判断数组存在

	if(typeof somevar == "undefined") {result = "yes"};
	"yes"	
3.常用函数parseInt() 默认十进制,看后面参数的开头"0x","0337"应该避免为8进制<!--并未在google浏览器下出现错误-->
	
	parseInt("123abc") 123
	parseInt("FF",16)  255
	parseInt("0x34")
4.isNaN函数其实等同于回答了这样一个问题：这个值被强制转换成数值时会不会返回IEEE-754​中所谓的”不是数值“（not a number）。

	isNaN({}); // true	
	isNaN("37");      // false: 可以被转换成数值37
5.你可以用这个方法来判定一个数字是否是有限数字。isFinite 方法检测它参数的数值。如果参数是 NaN，正无穷大或者负无穷大，会返回false，其他返回 true。

	isFinite(2e64);      // true
	isFinite(Infinity);  // false
6.encodeURI() 是对统一资源标识符（URI）进行编码的方法。它使用1到4个转义序列来表示每个字符的UTF-8编码	
encodeURIComponent()是对统一资源标识符（URI）的组成部分进行编码的方法。它使用一到四个转义序列来表示字符串中的每个字符的UTF-8编码（只有由两个Unicode代理区字符组成的字符才用四个转义字符编码）。
	
	encodeURI()
	encodeURIComponent()
7.eval(string) 一个字符串表示了一个JavaScript表达式，声明， 或声明的序列。表达式可以包括变量和已存在对象的属性。

	eval(string)
8.总是使用var 来声明全局变量
9.f()执行之后,n()为全局变量,或者返回给全局空间声明,保留了作用域内参数b的值,记录自身在的环境和相关的参数.

```
	var n;
	function f(){
	var  b  = "b";
	n = function(){
	return b;
	}
}
```
留住的是指针,用get,set函数闭包建立私有变量,迭代器.
### 对象操作
1.属性名字一般不加引号,除非:为js保留字,含有特殊字符,用数字开头的属性
2.属性可以是函数,函数是一种数据类型.
3.属性不能用.进行调用和(1)条件一致
4.this标识当前对象.
5.不用new 生成对象 this引用的是window全局对象.
6.对象有一个constructor 构造器属性
7.h12 instanceof Hero 是否有某一个对象初始化来的
8.控制输出数据的内容,函数也是对象也是一种数据类型

	console.info(h12)
	console.log() 
	console.error()
9.一些方法,o会自动调用toString
	
	toString
	"an object" + o	
10.valueOf()返回对象本身.

	o.valueOf() === o	
11.尽量避免使用Function 构造器函数,权限太大

	var sum = new Function("a,b","return a + b") 	sum.length //参数个数 2
12.caller返回调用函数

	function A(){return A.caller;}
	function B(){return A();}
13.prototype为构造函数的内容,该属性为一个对象

	prototype		
14.some_obj.say.call(my_obj,'myobje')为让my_obj 执行say 函数,并且传入参数.本质是修改了this的值,
some_obj.say.apply(my_obj,['ceshi'])为apply 参数为一个数组形式的
```
var some_obj = {
	name:'nanne',
	say:function(who){
	return 'haya ' + who + ', i am a ' +this.name;	
}
}

some_obj.say.apply(my_obj,['ceshi'])
```

15.arguments.callee属性为当前的函数对象,arguments数组,没有sort和slice方法

```
	(
function (count) {
	if(count < 5){
	alert(count);
	arguments.callee(++count);	
}
}
)(1)
```		