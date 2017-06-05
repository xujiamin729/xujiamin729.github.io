---
layout: post
title: 活用python虚拟环境virtualenv
categories:
- TECHNOLOGY
tags:
- Python
- Web
permalink: virtualenv
comments: true
date: 2017-01-30 08:54:03
---
程序猿的开发历程是悠久的，但是开发技术的版本更新是日新月异的，所有这样的现象很常见：N年前开发的应用程序是基于Python2.7的，但是现在的Python版本已经到3.x了，而3.x对2.7的兼容性并不是100%的 ，所以问题来了--是不运行基于Python2.7的应用程序还是运行基于Python3.x的应用程序，而对于程序猿而言，2.7的开发程序是儿子，3.x的开发程序也是儿子哇，能使二者之间兼得的神器就是virtualenv。
<!-- more -->

virtualenv是一个创建隔绝的Python环境的工具。它会创建一个包含所有必要的可执行文件的文件夹，用来使用Python工程所需要的包。换句话说，我们可以用virtualenv给各个项目创建各自的Python环境，各个的环境之间安装的包相互独立，互不影响。通过激活`avtive`相应的Python环境来使用相应的Python环境。这里为了方便管理不同的Python环境，我们使用virtualenvwrapper来对Python虚拟环境进行管理。

## 安装和配置
virtualenv和virtualenvwrapper的安装很简单，一条命令即可：
```bash
pip install virtualenv  # 安装virtualenv
pip install virtualenvwrapper # 安装virtualenvwrapper
```

virtualenv是不需要配置的，它的使用直接是在项目文件夹里执行命令`virtualenv proEnv`，就会在当前项目目录下生成proEnv的目录，目录下会包含bin/，include/，lib/，local/这四个文件夹和一个pip-selfcheck.json文件。当该虚拟环境被激活后`source proEnv/bin/activate`，所有执行的pip安装程序都会安装在当前虚拟环境文件夹proEnv中。不过这样就导致下面的问题：
1. 不方便管理--激活，消活`deactivate`，环境切换等
2. 无法重用--存放在指定项目目录下
而virtualenvwrapper能完美解决这些问题。

virtualenvwrapper的配置如下：
```bash
# 1.在~/.bashrc文件结尾添加下面
source $HOME/.local/bin/virtualenvwrapper.#!/bin/sh

# 2. 重新加载配置
source $HOME/.bashrc
```

## 使用说明
1. 创建环境
```bash
# 在$HOME/.virtualenvs/目录下创建项目python环境
mkvirtualenv proEnv [-p python3.5]
```
2. 列举所有环境
```bash
lsvirtualenv
```
2. 切换环境
```bash
workon proEnv
```
3. 退出环境
```bash
deactivate
```
2. 删除环境
```bash
revirtualenv proEnv
```
