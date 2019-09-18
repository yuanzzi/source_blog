---
layout: post
date: 2019-07-13
title: BAT 脚本实现文件夹监控
cover: false
categories:
	- 笔记
tags:
	- .bat
	- Windows
---
Windows 环境下快速编写 BAT 脚本实现文件夹监控
<!-- more -->
bat 脚本监控 windows 文件夹，如有新增文件，则调用另外一个bat脚本，再删除文件

```bat

@echo off & title 监控文件夹 By 放射云
color 0a & mode 35,3
 
::设置要监控的文件夹
set MtrDir=C:\Users\Administrator\Desktop\xp\aaa
 
::设置要调用的bat脚本
set Bat=alert.bat
 
echo 正在初始化记录文件 ...
(for /f "delims=" %%a in ('dir /a-d/s/b "%MtrDir%\*"') do (
    echo "%%~a"
))>"%tmp%\oFiles.Lst"

:Loop
set "Change="
cls & echo 正在监控文件夹中 ...
for /f "delims=" %%a in ('dir /a-d/s/b "%MtrDir%"') do (
    findstr /i "^\"%%~a\"$" "%tmp%\oFiles.Lst" >nul || (
        echo del /f /q "%%~a">>"%tmp%\DelNewFile.bat"
        set Change=1
    )
)
if defined Change (
    echo 发现新增文件，启动其它脚本。
    call "%Bat%"
    call "%tmp%\DelNewFile.bat"
)
goto Loop

```