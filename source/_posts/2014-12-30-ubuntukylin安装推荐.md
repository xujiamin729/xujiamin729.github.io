---
layout:	post
title:	ubuntukylin(64bit)安装推荐
categories:
- TECHNOLOGY
tags:
- Ubuntu
- Software
permalink:  Explore-software-ubuntu
comments:	true
---
在网上经常会看到[安装ubuntu后必做的n件事](http://www.linuxidc.com/Linux/2014-04/100411.htm),不过这些事情都是大众通用的,并不是完全适合自己的.所以本文就是对自己使用ubuntukylin这些年来的记录总结.
<!-- more -->


## ubuntukylin简介
UbuntuKylin是Ubuntu社区中面向中文用户的Ubuntu衍生版本，与麒麟系统没有关系。它是由工信部软件、集成电路促进中心（CSIP）、国防科技大学（NUDT）与国际著名开源社区UBUNTU的支持公司CANONICAL发起的一款开源社区操作系统项目。

发行版本从13.04开始，其有以下特性  

* Dash中的在线音乐搜索: 更加简单、方便的音乐搜索，帮助用户发现最新、最热的中国流行音乐
* 农历（中国传统历法）： 便于查询传统假日和节气时令的中文日历，包含公历
天气插件：提供来自中国气象局的天气预报信息，为用户日常起居和旅行提供参考
* 中文输入法：默认使用fctix输入法，支持云拼音输入，更加智能的联想功能
* 与WPS合作：提供中国本土办公软件WPS，兼容多种文档格式，具有强大的图形布局功能和丰富的网络资源，文档工作将更加专业和轻松   


## 事后三件事

1. 联网  
	后面所有的操作都依赖于网络。
2. 更新语言包以及软件更新器  
	安装时建议用英语,一方面安装过程更快一些,另一方面保持通用文件夹为英文名(命令行操作更方便快捷).此时更新时需要安装中文语言包，大概有400M左右的应用需要升级到最新。
3. 安装日常所用软件  
	常用软件可以直接在软件中心中查找安装,不过建议是用shell脚本[ubuntukylin_install.sh]({{ site.baseurl }}/assets/attachs/ubuntukylin_install.sh.txt)安装.

	1. 浏览器 -- chrome

		```bash
		# 安装chrome浏览器
		sudo apt-get install chromium-browser
		# 安装在线视频播放插件
		sudo apt-get install pepperflashplugin-nonfree
		```

		> **注意:**   
		> 安装完成后,需要登陆google帐号,可以同步书签并扩展应用
	2. 安装gcc编译环境

		```bash
		sudo apt-get install build-essential
		```
	3. 安装osdlyrics,以方便rhythmbox显示歌词

		```bash
		sudo apt-get install osdlyrics
		```

		> **注意:**  
		> 安装完成,需要启动osdlyrics并设置其自动启动的播放器
	4. 安装starDict字典

		```bash
		sudo apt-get install stardict
		```

		> **安装软件所需要的字典和发音包**  
		>
		> 1. [下载](http://share.weiyun.com/39678cb7bef4a4ad0be537f10578be2d)字典和发音包
		> 2. 命令安装
		>
		>	```bash
		>	cd stardict
		>	chmod 755 installDicts.sh installPron.sh
		>	sudo ./installDicts.sh
		>	sudo ./installPron.sh
		>	```
	5. 安装压缩工具p7zip

		```bash
		sudo apt-get install p7zip-full
		```
	6. 安装文本编辑器geany

		```bash
		sudo apt-get install geany
		```
	7. 安装视频播放器VLC

		```bash
		sudo apt-get install vlc
		```
	8. 安装位图图像处理软件gimp

		```bash
		sudo apt-get install gimp
		```
	9. 安装专业画图软件dia

		```bash
		sudo apt-get install dia
		sudo apt-get install dia-gnome
		```
	10. 安装tex软件

		```bash
		sudo apt-get install texlive-full
		sudo apt-get install texlive-fonts-recommended
		sudo apt-get install texmaker
		```

		> **安装win下的字体**  
		>
		> 1. [下载](http://share.weiyun.com/b298e1e21a18cf7278b4d8005aecfe7d)win字体和安装脚本
		> 2. 命令安装
		>
		>	```bash
		>	cd addWinFonts
		>	chmod 755 addWinFonts.sh
		>	sudo ./addWinFonts.sh
		>	```
	11. 安装java集成环境Eclipse

		```bash
		sudo apt-get install eclipse
		sudo apt-get install eclipse-jdt
		sudo apt-get install eclipse-pde
		```
	12. 安装python集成环境idle

		```bash
		sudo apt-get install idle-python2.7
		```
	13. 安装longene QQ
		* [下载](http://share.weiyun.com/c5367cd7a608d8737770356a70a7f393)deb包
		* 命令安装

			```bash
			sudo dpkg -i wine-qqintl_0.1.3-2_i386.deb
			sudo apt-get -f install
			```
	14. 安装pdf2htmlEx

		```bash
		sudo add-apt-repository ppa:coolwanglu/pdf2htmlex
		sudo apt-get update
		sudo apt-get install pdf2htmlEX
		```

## 待续
