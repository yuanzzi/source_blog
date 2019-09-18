---
layout: post
date: 2018-12-01
title: Ajax 同步状态下获取返回值
cover: false
categories:	
	- Web前端
tags:
	- Ajax
---

实际上 ajax 同步状态下是不可能获取到返回值的，只能利用回调方式在ajax方法外操作返回的数据 

<!-- more -->
```js
function load_val(callback){//定义一个回调函数
    $.getJSON('test.php' , function(dat){
        callback(data);//将返回结果当作参数返回
    });
}

load_val(function(data){
    alert(data);//这里可以得到值
});


function search(arg0,callback){
	$.ajax({
		url:,
		data:{json:arg0},
		dataType:"json"
		async:true,
		success:function(data){
			callback(data);
		}
	});
}
```