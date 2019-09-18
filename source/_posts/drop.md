---
layout: post
date: 2018-11-20
title: BootStrap 下拉菜单组件关闭点击事件 ( 转换为鼠标悬停事件 )
cover: false
categories: 
	- Web前端
tags:
	- BootStrap

---


有些时候需要关闭 BootStrap 下拉按钮组件的点击弹出菜单事件
 ```$(document).off('click.bs.dropdown.data-api')```
<!-- more -->
#### 由官网项目小结
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>

<div class="dropup up_menu">
  <a class="dropdown-toggle" id="dropdownMenu2" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
     友情链接
    <span class="caret"></span>
  </a>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenu2">
    <li><a href="http://www.chinaradiology.org" target="_blank">中华放射学分会</a></li>
    <li><a href="http://www.cjrjournal.org/" target="_blank">中华放射学杂志</a></li>
    <li><a href="http://www.fsxsj.net" target="_blank">放射学实践杂志</a></li>
    <li><a href="http://www.cjmit.com" target="_blank">中国医学影像技术</a></li>
    <li><a href="http://www.wanfangdata.com.cn" target="_blank">万方数据库</a></li>
    <li><a href="http://epub.cnki.net" target="_blank">CNKI</a></li>
    <li><a href="http://www.dxy.cn/" target="_blank">丁香园</a></li>
  </ul>
</div>