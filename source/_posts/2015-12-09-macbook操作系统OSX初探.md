---
layout:	post
title:	macbook操作系统OSX初探
categories:
- TECHNOLOGY
tags:
- Mac
- OSX
permalink:  Explore-OSX
comments:	true
---
经过一番货比三家后，终于通过苹果内部员工的85折拿下了这款Macbook Pro MF840。今天怀着激动兴奋的心情，拆了配送包裹，好好把玩了一天。本篇博文对OS X系统内置的APP进行一些摸索，最后在系统中安装了VMWare Fusion虚拟机来搭建自己的Ubuntu工作环境。而下篇博文[macbook常用软件及其管理]({{site.baseurl}}/2015/12/10/macbook常用软件及其管理.html})将详细介绍苹果系统的[软件包管理][homebrew]以及常用的软件。
<!-- more -->

## OS X系统
苹果原生的系统还是很给力的，省电啥的还没有深刻体会，但是界面的美观，操作的流畅还是留下很深的印象。其内置的APP也是挺给力的，详细介绍见[Mac之妙][mac_app]，下面简要介绍一些。

* 融入日常类
    * 邮件  
    集成iCloud，126和Gmail等常见的电子邮件服务。**赶快使用**
    * 日历  
    创建多个单独的日历来跟踪管理看似复杂却简单的日程。**赶快使用**
    * 提醒事项  
    相当于一个便笺，在特定的日期和时间提醒你该干什么。**赶快使用**
    * 备忘录  
    相当于一个随手笔记，可以随手记下闪现的灵感，还可以和Safari，照片和地图等APP联合使用。功能方面和印象笔记有点类似。**赶快使用**
    * 通讯录  
    它可以配合信息/FaceTime/邮件等使用。非常方便。**赶快使用**
    * 信息/FaceTime  
    Apple设备之间通信的工具，分别对应文本图片和音频视频。**跟微信/QQ有的一拼**
    * iBooks  
    Mac上用来看书的工具，书的排版没得说，缺陷就是书源少要收费。**可以和iKindle组合使用**
    * 地图  
    怎么说呢，甩百度两条街吧，配合它的触摸板，完美。**赶快使用**
* 重点研究类
    * automator[crontab]/脚本编辑器
    自动执行常用任务，这个是日后重点研究的工具。**重点研究**
    * 照片  
    该应用除了让图库的管理更加轻松，可以添加位置信息，还可以批量更改图片信息等。最关键的是可以和强大且易用的编辑工具（PS/Gimp）配合使用。**重点研究**
    * iMovie  
    和照片的的功能类似，不过处理的对象是视频。**等图片摸透再了解吧**
    * GarageBand  
这次的对象是音频，可以玩转音乐。**目前只想听听歌，码码代码**
* 打入冷宫型
    * Pages/Numbers/Keynote  
    分别对应Office里面的Word/Excel/PowerPoint，但是却兼容它们。**基本被Tex取代，只用来查看Office文档**
    * App Store  
    它的功能和Ubuntu里的软件中心类似，不过作为一个码农，还是打算将软件的管理通过命令来来维护。 **基本被HomeBrew取代**
    * Safari  
    苹果内置的浏览器，看视频需要adobe flash player插件。**完全被Chrome取代，可以打入冷宫**
    * iTunes  
    Mac上的娱乐大本营，可以听歌看电影。缺陷就是片源少还要钱。**基本被XBMC取代**
* 不常用但实用型
    * 活动监视器[任务管理器]
    * 数码测色计[取色板]
    * 迁移助理  
    支持Mac-Mac，PC-Mac，TimeMachine-Mac快速迁移文件。
    * 钥匙串访问  
    安全存储你使用的所有密码

## 更新&设置
1. 系统更新  
可能你当前的系统的并不是最新版本，所以进入系统后第一件事情就是联网，然后到APP Store里把系统和软件更新到最新版本。更新的同时可以了解苹果系统。

2. 偏好设置  
    * 触控版[学习触控版的手势]
    * 鼠标滚轮方向[取消自然的滚动方向]

## 虚拟机[VirtualBox][virbox]
原因很简单，苹果的硬件+苹果的软件这样的组合才能奉献最佳的性能，多系统对于Macbook而言就是对硬件资源的浪费。虽说Mac支持Windows，但对于我而言，Windows只剩下游戏值得流连忘返，而我的工作环境现在只有Ubuntu。在熟悉OS X系统的过程中，Ubuntu应该还是主要的工作场所，所以虚拟机还是必不可少的。之前由于研究的不够仔细，认为VMware fusion无法支持在不同平台下运行着的虚拟机，这是不对的。要通过`文件->打开`的方式运行，通过`导入->选择现有虚拟机`的方式是无法成功的。在这样的情况下，选择Virtual Box还是VMware fusion就纯看各自心情了。我选择VMware fusion，一方面是接触VMware比较早，毕竟“初恋”是难忘的;另一方面是它对Windows和Linux的支持更到位些。优势如下：
* 完美支持OS X EI Capitan和Windows 10,并对它们进行了优化。[对我意义不大]
* 在Mac下虚拟运行Mac OS X EI Capitan[可以独立母系统开发Mac应用程序]
* 高性能的3D图形加速处理能力[使得在虚拟机里面玩游戏有了点可能]

安装过程很简单，直接从[官网][vmware_download]下载VMWare Fusion 8 Pro，之后通过激活码`FY7N2-6RGD2-081XZ-UYWQC-ZPKCA`激活即可。


Virtual Box的安装也很简单，也是从[官网][virtual_download]下载Virtual Box for mac，因为它是开源的，所以不用激活啥的。
> **Tips: vdi扩容**  
> 默认情况下，Mac里的VirtualBox会给虚拟机分配8G的磁盘空间，但这是远远不能满足我们的工作需要的，所以当安装虚拟机时不幸分配过小的磁盘空间，可以通过下面简单的方式给虚拟机扩容
>
> ```sh
> # 20480的单位是MB，所以这里扩容到20G
> VBoxManage modifyhd xxx.vdi -resize 20480
> ```


## 参考文献
1. [Mac之妙，秒在它能帮你做到的一切][mac_app]
2. [WMWare Fusion 8 pro下载][vmware_download]
2. [WMWare Fusion 8 Pro简介][vmware]
3. [homebrew官网][homebrew]
4. [Virtual Box下载][virtual_download]

[mac_app]:  http://www.apple.com/cn/osx/apps/
[vmware]:   http://www.iplaysoft.com/vmware-fusion.html
[vmware_download]:  http://www.vmware.com/products/fusion/
[homebrew]: http://brew.sh
[virtual_download]: https://www.virtualbox.org/wiki/Downloads
