---
layout: post
date: 2019-07-28
title: JAVA 捕获唯一索引重复异常
cover: false
categories:	
	- Java
tags:
	- MyBatis
	- MySQL
---

JAVA 捕获 MySQLIntegrityConstraintViolationException （唯一索引重复）异常

<!-- more -->

在 service 层的数据库操作块无法捕捉因唯一索引而引发的数据库更新或插入异常，只能通过service方法抛出 DataAccess 异常，再到 Controller 层捕获

```Java

public Object update(UserEntity user) throws DataAccessException{
	...
}

@RequestMapping("/update")
@ResponseBody
public Object update(@RequestBody userEntity){
	try{
		return userService.update(userEntity);
	}catch(DataAccessException e){
		return FunCommon.getReturnJson("msg","用户名重复");
	}
}

```