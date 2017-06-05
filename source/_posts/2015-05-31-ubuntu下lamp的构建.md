---
layout:	post
title:	ubuntu下lamp的构建
categories:
- TECHNOLOGY
tags:
- Ubuntu
- OPS
permalink:  Build-lamp
comments:	true
---
LAMP（Linux-Apache-MySQL-PHP）网站架构是目前国际流行的Web框架，该框架包括：Linux操作系统，Apache网络服务器，MySQL数据库，Perl、PHP或者Python编程语言，所有组成产品均是开源软件，是国际上成熟的架构框架，很多流行的商业应用都是采取这个架构，和Java/J2EE架构相比，LAMP具有Web资源丰富、轻量、快速开发等特点，微软的.NET架构相比，LAMP具有通用、跨平台、高性能、低价格的优势，因此LAMP无论是性能、质量还是价格都是企业搭建网站的首选平台。(附带安装mysql的管理软件phpmyadmin)
<!-- more -->


## 安装流程
* 安装apache2

	```bash
	sudo apt-get install apache2
	```
* 在浏览器中输入localhost,显示如下界面
![localhost]({{ site.baseurl }}/assets/images/apache.png)
* 安装php5

	```bash
	sudo apt-get install php5
	```
* 安装mysql

	```bash
	sudo apt-get install mysql-server
	```
* 安装phpmyadmin
phpmyadmin是基于php,并通过web的方式管理mysql数据库.
	* 代码安装

		```bash
		sudo apt-get install phpmyadmin
		# 根据提示选择apache2,输入root密码和数据库密码
		```
	* 更改/var/www目录的权限,并创建phpmyadmin链接

		```bash
		sudo chmod 777 /var/www
		sudo ln -s /usr/share/phpmyadmin /var/www/html/
		```
	* 在浏览器中输入localhost/phpmyadmin
	![phpmyadmin]({{ site.baseurl }}/assets/images/phpmyadmin.png)
