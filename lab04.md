---
layout: default
title: 我的科普博客
---

##科普博客
###javascript
    我因社团要求，在国庆期间简单的学习了点javascript语法。js这门语言与网页设计息息相关，各种网页中"能动"的东西基本都是用Javascript写出来的，前端设计真的挺有意思的。JS的普遍性让网上有许多与JS相关的meme出现，如:<br />
    到处都有javascript<br />
    ![](https://upload.cc/i1/2018/10/13/GYCkAZ.jpg)
    javascript是一门面对对象的脚本语言，有很多与C不同的地方。最明显的地方便是类型转换，当然也有许多相关图片<br />
    数字1与字符串'1'相加=11，11减去字符串'1'却等于10(涉及js的字符转换)<br />
    ![](https://upload.cc/i1/2018/10/13/U5x7lq.png)
    各种js的类型转换、双等、全等的运算规则<br />
    ![](https://upload.cc/i1/2018/10/13/uHXpVc.png)
    各种类型转换、方法也让我晕头转向<br />
    ![](https://upload.cc/i1/2018/10/13/5mhGJX.jpg)
    当然js也有他的优点，弱类型语言在熟悉类型转换后对比强类型语言优势就很明显了
    ![](https://upload.cc/i1/2018/10/13/zhPgJH.png)
###代码举例
    这里举个简单的js代码(在chrome中运行，包含简单的html和css)
```
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
<style type="text/css">

	#areaDiv {
		border: 1px solid black;
		width: 300px;
		height: 50px;
		margin-bottom: 10px;
	}
	
	#showMsg {
		border: 1px solid black;
		width: 300px;
		height: 20px;
	}

</style>
<script type="text/javascript">

	window.onload = function(){
		/*
		 * 当鼠标在areaDiv中移动时，在showMsg中来显示鼠标的坐标
		 */
		//获取两个div
		var areaDiv = document.getElementById("areaDiv");
		var showMsg = document.getElementById("showMsg");
		
		/*
		 * onmousemove
		 * 	- 该事件将会在鼠标在元素中移动时被触发
		 * 
		 * 事件对象
		 * 	- 当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递进响应函数,
		 * 		在事件对象中封装了当前事件相关的一切信息，比如：鼠标的坐标  键盘哪个按键被按下  鼠标滚轮滚动的方向。。。
		 */
		areaDiv.onmousemove = function(event){
			
			//解决事件对象的兼容性问题(兼容ie8以下及火狐)
			event = event || window.event;
			
			/*
			 * clientX可以获取鼠标指针的水平坐标
			 * cilentY可以获取鼠标指针的垂直坐标
			 */
			var x = event.clientX;
			var y = event.clientY;
			
			//在showMsg中显示鼠标的坐标
			showMsg.innerHTML = "x = "+x + " , y = "+y;
			
		};
		
	};

</script>
</head>
<body>

	<div id="areaDiv"></div>
	<div id="showMsg"></div>

</body>
</html>
```
    这是一个能在方格中显示鼠标位置的代码，应用方面在地图测距、游戏等方面。
    以上便是一个简单的js代码及技术分享，因为学的还很浅薄，所以许多地方完善不了还请见谅。    