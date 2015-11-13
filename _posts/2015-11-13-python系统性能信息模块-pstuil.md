---
layout: post
title:   python系统性能信息模块-pstuil
description: "python系统性能信息模块-pstuil"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [运维,Python]
duoshuo: true
---
psutil模块能够轻松获取系统能够运行的进程和系统利用率（包括CPU、内存、磁盘、网络等）信息。主要用于系统监控，分析和限制系统资源及进程的管理。

它实现了很多同等命令行工具提供的功能，如ps、top、df等。

<!-- more -->
## psutil的安装与基本使用
楼主本人使用的系统是osx 10.11.1。使用的python版本是系统自带的2.7.10.

#### 下载软件包
psutil的下载网址为:[下载网址][1]。然后选择`psutil-3.2.2.tar.gz`进行下载。

具体安装步骤：

> 1. tar -zxvf psutil-3.2.2.tar.gz
> 2. cd psutil-3.2.2
> 3. sudo python setup.py install

#### psutil的基本使用
首先需要进行模块的导入，然后就可以进行使用了，具体事例如下：
	import psutil
	print psutil.virtual_memory()






[1]:	https://pypi.python.org/simple/psutil/