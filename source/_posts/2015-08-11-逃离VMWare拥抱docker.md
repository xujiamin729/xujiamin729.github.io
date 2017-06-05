---
layout:	post
title:	逃离VMWare拥抱docker
categories:
- TECHNOLOGY
tags:
- Ubuntu
- OPS
permalink:  Explore-docker
comments:	true
---
Docker是一个开源项目，它是基于linux容器（LXC）等技术，旨在实现轻量级的操作系统虚拟化的一个解决方案。用户操作Docker的容器就像操作虚拟机一样，但是它比虚拟机更轻量更快速。
<!-- more -->

## VMWare VS Docker
这里VMWare只是传统虚拟化方式的一个典型代表--虚拟机。传统方式是在硬件层面实现的，就像我们有时在新建虚拟机时出现这样的错误信息：
> **Error:**  
> The virtual machine could not be started because the hypervisor is not running.

而解决这个问题的方法就是进入BIOS里面打开Hypervisor。这里的Hypervisor是所有传统虚拟化技术的核心。它运行于物理服务器和操作系统之间的中间的的软件层，允许多个操作系统和应用共享一套基础物理硬件。

相较于在硬件层面上实现的传统虚拟化技术，Docker是在操作系统层面上实现虚拟化的，它直接**复用**本地主机的操作系统。下面的两张图片能很好的诠释二者区别。  

![VMWare]({{site.baseurl}}/assets/images/virtualization.png)
![Docker]({{site.baseurl}}/assets/images/docker.png)



作为一种新兴的虚拟化方式，Docker的突出的优势有如下三点：  
1. 秒级启动  
2. 对系统资源利用率很高，一台主机可以同时运行数千个Docker容器  
3. 容器除了运行其中的应用外，基本不消耗额外的系统资源。原因在于Docker容器中只安装配置对应的应用，它可以用最小最基本的内核镜像，用最精简的软件依赖。

总结见下表：  
	|   特性   | Docker       |  VMWare  |  
	| :----:   | :----:       | :-----:  |  
	|   启动   | 秒级         |  分钟级  |  
	| 硬盘使用 | MB级         |  GB级    |  
	|   性能   |接近原生      | 弱于原生 |  
	|系统支持量|单机支持上千个|一般十几个|  


## Docker安装
Docker是基于LXC等技术的，所以linux系统对其的支持是不言而喻的。这里Docker运行的环境是Ubuntu系统。

1. 升级内核
Docker需要的Ubuntu的内核版本要大于3.13。对于Ubuntu 14.04这个版本是不需要升级内核以及安装依赖软件，而之前的版本是需要升级内核的。升级脚本如下：

	```bash
	sudo apt-get update
	sudo apt-get install linux-image-generic-lts-raring linux-headers-generic-lts-raring
	sudo reboot
	```
2. 通过源安装Docker

	```bash
	# 安装apt-transport-https支持
	sudo apt-get install apt-transport-https
	# 获取锁钥
	sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
	# 添加Docker源
	sudo bash -c "echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
	# 更新软件源仓库
	sudo apt-get update
	# 安装Docker
	sudo apt-get install lxc-docker -y --force-yes
	```

## Docker配置
Docker的配置文件是[/etc/default/docker]({{site.baseurl}}/assets/attachs/docker.txt)，里面可以设置Docker的启动路径，参数配置，代理以及临时目录设置。

1. 使用代理

	```bash
	cat << EOF >> /etc/default/docker
	export http_proxy="http://127.0.0.1:8080"
	export https_proxy="http://127.0.0.1:8080"
	EOF
	```
2. 改变docker进程监听的IP和端口

	```bash
	cat << EOF >> /etc/default/docker
	DOCKER_OPTS="-H unix:///var/run/docker.sock -H 0.0.0.0:4243 --insecure-regis    try 127.0.0.1:5000"
	EOF
	```
附：Docker一键安装配置[install_docker.sh]({{site.baseurl}}/assets/attachs/install_docker.sh.txt)

## Docker使用
1. 镜像操作

	```bash
	# 获取注册服务器registry.hub.docker.com上的ubuntu镜像
	sudo docker pull ubuntu:14.04
	# 列出本地镜像
	sudo docker images
	# 启动docker容器
	sudo docker run -it ubuntu:14.04 /bin/bash
	# 提交已有镜像,获得新镜像id
	sudo docker commit -m "commit information" -a "user information" original_docker_id repository:tag
	# 从当前目录下的Dockerfile中生成镜像
	sudo docker build -t="repository:tag" .
	# 修改镜像标签
	sudo docker tag image_id repostory:new_tag
	# 从本地文件系统（容器快照）导入
	sudo cat ubuntu-14.04-x86_64-minimal.tar.gz | docker import - ubuntu:14.04
	# 保存镜像
	sudo docker save -o ubuntu_14.04.tar ubuntu:14.04
	# 载入镜像
	sudo docker load < ubuntu_14.04.tar
	# 上传镜像
	sudo docker push repostory:tag
	# 清理所有未打过标签的本地镜像
	sudo docker rmi $(docker images --quiet --filter "dangling=true")
	```
附：
	1. [Dockerfile]({{site.baseurl}}/assets/attachs/Dockfile.txt)
	2. 本地文件系统导入镜像的下载：[openvz的模板下载](http://openvz.org/Download/templates/precreated)

2. 容器操作

	```bash
	# 容器启动
	## -t	让Docker分配一个终端Terminal并绑定容器的标准输入
	## -i	让容器的标准输入保持打开（交互模式）
	## -d	以守护态运行
	sudo docker run -it ubuntu:14.04 /bin/bash
	# 显示容器状态
	sudo docker ps
	# 获取容器的输出信息
	sudo docker logs container_id
	# 容器快照的导出
	sudo docker export container_id
	# 清理所有处于终止状态的容器
	sudo docker rm $(docker ps -a -q)
	```

3. 仓库操作

	```bash
	# 查找官方仓库的镜像
	sudo docker search ubuntu
	# 创建私有仓库（官方registry镜像）
	sudo docker run -d -p 5000:5000 registry
	# 上传镜像到私有仓库
	sudo docker push localhost:5000/image_id:tag
	```
