---
layout: post
date: 2018-11-22
title: CSS 实现“小三角”
cover: false
categories:	
	- Web前端
tags:
	- css
---

html 页面常常需要画小三角。如下代码，调整宽高和方向。
<!-- more -->
#### > 项目小结

```
	<style type="text/css">
		.triangle{
				width: 0px;
			    height: 0px;
			    border-width: 20px 12px;
			    border-style: solid;
			    border-color: transparent transparent #22364d transparent;
		}
	</style>

	<div class="triangle" id="doc_tri"></div>
```




<style type="text/css">
.triangle{
	width: 0px;
	height: 0px;
	border-width: 20px 12px;
	border-style: solid;
	border-color: transparent transparent #169fe6  transparent;
}
</style>

<div class="triangle" id="doc_tri"></div>