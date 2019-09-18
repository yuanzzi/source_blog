---
layout: post
title: 原生 Ajax 上传文件
date: 2019-02-12 16:18:07
cover: false
categories:	
	- Web前端
tags:
	- JQuery
	- Ajax
---

有时小小的文件上传用 WebUploader 之类嫌费劲，看下原生 Ajax 上传文件
<!-- more -->

值得注意的一点是要在 input[type=file] Dom上添加 Listenner(change) 事件，否则会点击就直接提交 ajax 请求了

```HTML
	<form enctype="multipart/form-data" method="POST">
		<input type="file" id="imgCase" onclick="javascrpit:this.addEventListener('change', upload, false);" multiple="true" />
	</form>
```

```JS
	function upload(){
	 	var formData = new FormData();
	 	for(var i=0;i<$('#imgCase')[0].files.length;i++){
		  	formData.append('file['+i+']',$('#imgCase')[0].files[i]);
		  }
		  $.ajax({
		  	type:"post",
		  	url:serverURL+"/attached/upl_atc",
		  	data:formData,
		  	async:true,
		  	contentType:false,
		  	processData:false,
		  	mimeType:'mutipart/form-data',
		  	success:function(data){
		  		console.log(data);
		  	}
		  });
	 }


补充：ajax 提交 form 表单会出现表单自动提交并跳转，需要添加onsubmit="return false"
	<form onsubmit="return false" method="post" action="#"></form>

```