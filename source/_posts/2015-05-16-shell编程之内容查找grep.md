---
layout:	post
title:	shell编程之内容查找grep
categories:
- TECHNOLOGY
tags:
- Shell
permalink:  Explore-grep-Shell
comments:	true
---
GREP (global search regular expression(RE) and print out the line,全面搜索正则表达式并把行打印出来)是一种强大的文本搜索工具，它能使用**正则表达式**搜索文本，并把匹配的行打印出来。
<!-- more -->


## 简介
Unix的grep家族包括grep、egrep和fgrep。egrep和fgrep的命令只跟grep有很小不同。egrep是grep的扩展，支持更多的re元字符， fgrep就是fixed grep或fast grep，它们把所有的字母都看作单词，也就是说，正则表达式中的元字符表示回其自身的字面意义，不再特殊。linux使用GNU版本的grep。它功能更强，可以通过-G、-E、-F命令行选项来使用egrep和fgrep的功能。

## 使用方法
* 基本用法

	```bash
	# 搜索原始字符串
	grep [-cinv] '搜索字符串' filename
	# 用正则表达式搜索字符串
	grep -E 'pattern' filename
	```
* 参数说明
	* `-c`	统计查找到字符串的次数
	* `-i`	忽略大小写
	* `-n`	显示查找字符串的行号
	* `-v`	反向选择
	* `-E`	pattern中可以用扩展的正则表达式

## 样例演示
* 在/etc/passwd中查找root字符串,并显示所在行号

	```bash
	grep -n 'root' /etc/passwd
	```
![grep-n]({{ site.baseurl }}/assets/images/grep-n.png)
* 在/etc/passwd中查找oo字符串出现的行次数

	```bash
	grep -c 'oo' /etc/passwd
	```
![grep-c]({{ site.baseurl }}/assets/images/grep-c.png)
* 在/etc/passwd中查找oo字符串未出现的行

	```bash
	grep -vn 'oo' /etc/passwd
	```
![grep-v]({{ site.baseurl }}/assets/images/grep-v.png)
* 在/etc/passwd中查找以b开头的字符串

	```bash
	grep -E '^[b]' /etc/passwd
	```
![grep-E]({{ site.baseurl }}/assets/images/grep-E.png)
