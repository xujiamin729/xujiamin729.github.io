---
layout:	post
title:	ubuntu制作usb启动盘
categories:
- TECHNOLOGY
tags:
- Ubuntu
- Software
permalink:  Make-startupDisk
comments:	true
---
常年与计算机为伴,免不了要经常给计算机安装系统.而重装系统当然需要工具.光盘安装,读取太慢;硬盘安装,需要一个大前提:电脑能正常工作,一旦电脑无法正常开机,该方法无效.现在u盘非常普及,所以用usb作系统启动盘能很好的解决上面的两个问题.
<!-- more -->


## 准备工作

* u盘
* ISO镜像文件 -- [ubuntukylin-14.04.2-desktop-amd64.iso](http://www.ubuntukylin.com/downloads/download.php?id=38)
* 烧盘软件 -- unetbootin-linux-583

	```bash
	sudo apt-get install unetbootin
	```

## 格式化u盘

* 查看u盘信息

	```bash
	mount
	```
	> u盘信息:  
	> /dev/sdb1 on /media/KINGSTON type vfat (rw,nosuid,nodev,uid=1000,gid=1000,shortname=mixed,dmask=0077,utf8=1,showexec,flush,uhelper=udisks)
* 卸载u盘

	```bash
	umount /media/KINGSTON
	```
* 格式化

	```bash
	mkfs -t vfat /dev/sdb1
	```	 

## 启动并设置unetbootin-linux-583参数

* 参数设置

	![图片]({{ site.baseurl }}/assets/images/ubuntu_unetbootin_set.png)
	> **注意：**  
	> 软件能够识别u盘--u盘一定要插在电脑上
