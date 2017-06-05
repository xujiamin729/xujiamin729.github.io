---
layout:	post
title:	shell运行环境之sudo的环境
categories:
- TECHNOLOGY
tags:
- Ubuntu
- Shell
permalink:  Explore-sudo-Shell
comments:	true
---
上篇[博文]({{site.baseurl}}/2015/09/09/shell运行环境之环境配置文件.html)讲解了shell里面四个配置文件的作用域以及shell的四种常用模式。在此基础上，我们进一步探究一下在用户切换过程中，运行环境的变化。在Ubuntu里，我们通常使用`sudo`来提权，使用`su`来切换用户，而这两种操作都会对bash运行环境产生影响。搞明白运行环境的变化，你将明白在公司怎样使用代理。
<!-- more -->


## 简介
我们经常在终端中使用`sudo`来提权--以普通用户的身份去行使管理员的权限（前提是知道管理员用户的密码），这样减少了root用户的登录次数和管理时间，也提高了系统的安全性。不过有时候我们会直接用`su`切换到管理员进行一系列操作。`su`和`sudo`虽然不是具有相似功能的命令，但是它们的目的大部分情况是为了获取root权限。  

* su命令  
su命令是switch user的简写，是用来切换用户的。当不加任何参数时，它将切换到root用户。它需要你想**切换到的用户**的密码，在输入密码后，你将切换到那个用户的运行环境。
* [sudo][sudo]命令  
该命令是superuser do的简写，能够以root的权限取执行命令，但是它需要的是**当前用户**的密码，而不是像su需要的是想要切换到的用户的密码。这样需要执行一些需要root权限的命令时就不需要频繁输入root用户的密码，当然前提是当前用户的信息是存档在特殊的文件（/etc/sudoers）中。默认情况下，系统将记住当前用户的密码一段时间，以方便用户不用经常输入密码。

## [运行环境的变化][su&sudo]

* sudo
根据man的说明，sudoers提供了两种方法来限制sudo从用户环境中继承的变量。默认是env_reset变量是enabled，此时将会执行一个新的，最小的环境/etc/environment。另一种是设置env_reset变量是disabled，此时env_check和env_delete充当白列表的作用，因此不建议第二种情况。
* sudo su  
bash将以一个交互非登录模式运行，所以只有两个bashrc文件将被执行。所以当用户切换成root后，我们还在当前的工作的目录，而非/root目录。
* sudo su -  
bash将以登录模式运行的，此时/etc/profile，~/.profile将会被执行，隐形的/etc/bash.bashrc和~/.bashrc也将会被执行。此时，我们的当前目录是/root。
* sudo -i将
-i是--login的简写，所以接近sudo su -的情况
* sudo /bin/bash
bash将以非登录模式运行，上面四个文件将不会被执行。


## 试验

* 问题  
今天在公司准备使用命令行`sudo /opt/logstash/bin/plugin install logstash-output-webhdfs`给logstash安装logstash-output-webhdfs插件，以实现将logstash收集的日志信息存储到Hadoop文件系统这一目的。但是却一直提示如下错误：

	> Unable to download data from https://rubygems.org/ - 连接被对端重置 (https://rubygems.global.ssl.fastly.net/latest_specs.4.8.gz)  
	> ERROR: Installation aborted, verification failed for logstash-output-webhdfs

这里公司上网环境是使用了代理。本人在~/.bashrc中添加了`export http_proxy=xxx`和`export https_proxy=xxx`。接下来按照网上的解决方法作了如下尝试，均已失败告终。    

1. 用Google搜索错误提示[Unable to download data from https://rubygems.org][unable]  
2. [手动安装插件logstash-output-webhdfs][manual]  

* 解决方案

1. [设置sudo的运行环境][sudo_change]
使用`sudo visudo`对/etc/sudoers文件进行如下修改：

	```sh
	Defaults env_keep = "http_proxy https_proxy"
	Defaults        env_reset
	```
通过保留当前用户的http_proxy和https_proxy变量，使得sudo情况下也能使用代理。具体参考[这里][sudo_env]。

2. 进入root用户，并设定http_proxy和https_proxy代理。

## 参考文献
2. [如何更换rubygem镜像的源][unable]
3. [如何手动安装logstash插件logstash-output-elasticsearch-shield][manual]
5. [维基百科sudo][sudo]
7. [su和sudo对运行环境的影响][su&sudo]
1. [sudo使用代理][sudo_change]
2. [sudo环境设置][sudo_env]


[unable]:   http://www.sjsjw.com/kf_jiagou/article/027841ABA028365.asp
[manual]:  https://discuss.elastic.co/t/shield-w-logstash-offline-install/25072
[sudo]:     https://zh.wikipedia.org/zh/Sudo
[su&sudo]:  http://askubuntu.com/questions/376199/sudo-su-vs-sudo-i-vs-sudo-bin-bash-when-does-it-matter-which-is-used
[sudo_change]:	https://getpocket.com/a/read/149876899
[sudo_env]:			http://my.oschina.net/alphajay/blog/28811
