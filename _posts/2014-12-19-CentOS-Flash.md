---
layout: post
title:  CentOS6.5使用YUM安装Adobe Flash Player
description: "CentOS6.5使用YUM安装Adobe Flash Player"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [Linux,CentOS]
duoshuo: true
---
##引言
CentOS自带的火狐浏览器没有预装Flash，因此这里需要自己安装。

<!-- more -->

##i386系统
	
	wget http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm
	rpm -ivh adobe-release-i386-1.0-1.noarch.rpm
	rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
	yum install firefox.i386 flash-plugin

##x86_64系统
	
	wget http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
	rpm -ivh adobe-release-x86_64-1.0-1.noarch.rpm
	rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
	yum install firefox.x86_64 flash-plugin

##更新Flash player
	
	yum update flash-plugin
