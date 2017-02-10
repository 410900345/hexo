---
title: xuejs2
categories: js
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
