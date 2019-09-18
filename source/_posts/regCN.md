---
layout: post
date: 2018-12-01
title: 两个非常实用的匹配中文字符正则表达式
cover: false
categories:	
	- 笔记
tags:
	- 正则
	- 字符串处理

---




在处理字符串时，特别是处理 HTML 字符串时，常常需要用到正则表达式来处理中文字符。 以下介绍两个非常实用的表达式
<!-- more -->
#### > 由网络爬虫展开

### 1. 仅仅匹配中文字符：([\u4e00-\u9fa5]+)

```JAVA

	String str = "<img alt=\"甲状腺。\" src= 'd://a.img' >  <p>这是第一句话！</p>";

	String reg = "([\\u4e00-\\u9fa5]+)";
	//String reg = "([^\\x00-\\xff]+)";

	Pattern pattern = Pattern.compile(reg);
	Matcher matcher = pattern.matcher(str);
	while(matcher.find()){
		System.out.println(matcher.group(0));
		
	}

	//打印结果：
	甲状腺
	这是第一句话
```

### 2. 匹配中文字符以及标点：([^\x00-\xff]+)
此表达式又称为双字节字符匹配

```JAVA
	String str = "<img alt=\"甲状腺。\" src= 'd://a.img' >  <p>这是第一句话！</p>";

	//String reg = "([\\u4e00-\\u9fa5]+)";
	String reg = "([^\\x00-\\xff]+)";

	Pattern pattern = Pattern.compile(reg);
	Matcher matcher = pattern.matcher(str);
	while(matcher.find()){
		System.out.println(matcher.group(0));
		
	}

	//打印结果：
	甲状腺。
	这是第一句话！
```
	