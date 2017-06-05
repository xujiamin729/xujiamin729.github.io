---
layout:	post
title:	shell编程之文件检索find
categories:
- TECHNOLOGY
tags:
- Shell
permalink:  Explore-find-Shell
comments:   true
---
`find`命令是用来搜索指定目录下面符合搜索选项的文件.它跟`awk`,`sed`,`grep`的区别是它搜索到的对象是文件,而后三者是文件里的字符或字符串.
<!-- more -->


## 用法
* 命令格式

    ```bash
    find path -option
    ```
* 参数说明
    * `-name 'pattern'	根据名称来查找
    * `-user 'pattern'` 根据所属用户
    * `-size n`		根据文件大小   
    * `-type [fdbl]`	根据文件类型
    * `-empty`		是否时空文件
    * `-exec command {} \;`	对查找到的文件进一步命令处理
    * `-mtime n`	根据文件内容修改时间(单位是天)
    * `-ctime n`	根据文件属性改变[`chmod`]时间(单位时天)
    * `-atime n`	根据文件访问[`cat`]时间(单位是天)

	> ***注意:***  
	> `-mmin n`/`-cmin n`/`-amin n`和上面三个区别是单位是分钟   
	> 对于n,`n`是指正好n天前的当天,`+n`是指所有n天前,`-n`是指所有n天内


## 案例
1. 查找_posts/目录下面文件名包含shell字符串的文件

    ```bash
    find _posts/ -name '*shell*'
    ```
    结果显示如下:
    ![shell]({{ site.baseurl }}/assets/images/shell.png)
2. 查找_posts/目录下面文件名包含shell字符串的文件,并统计每个文件有多少行

    ```bash
    find _posts/ -name '*shell*' -exec wc -l {} \;
    ```
    结果显示如下:
    ![findwc]({{ site.baseurl }}/assets/images/findwc.png)
3. 下面根据文件内容修改时间(单位是分钟)进行查找
目前_posts中的文件显示如下,以时间先后排序,其中swp的文件的修改时间为7月1号18:12,而原文件是17:59,其他的都是6月30号的文件.
![shell]({{ site.baseurl }}/assets/images/states.png)
    1. 查询19分钟之前那一分中哪些文件被修改了

	```bash
	find _posts/ -mmin 19
	```
	结果显示如下:
	![19]({{ site.baseurl }}/assets/images/19.png)
    2. 查询前19分钟之前所有被修改了的文件

	```bash
	find _posts/ -mmin +19
	```
	结果显示如下:
	![+19]({{ site.baseurl }}/assets/images/+19.png)
    3. 查询前19分钟以内所有被修改了的文件

	```bash
	find _posts/ -mmin -19
	```
	结果显示如下:
	![-19]({{ site.baseurl }}/assets/images/-19.png)
4. 查询_posts/目录下面文件大小大于3k的文件

    ```bash
    find _posts/ -size +3k
    ```
    结果显示如下:
    ![10k]({{ site.baseurl }}/assets/images/10k.png)
