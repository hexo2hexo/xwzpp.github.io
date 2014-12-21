---
layout: post
title:  CentOS-Sublime2安装
description: "CentOS Sublime2安装"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [CentOS,sublime2]
duoshuo: true
---

##引言
Sublime编辑器据说也是一种神级编辑器，所以今天就安装试了试，果然非常不错。

<!-- more -->

##安装

1.从官网下载相应操作系统的下的[安装包][1]，这里下的是`linux`下的安装包
2.解压安装包，并将其放在`/opt/`下：    

	tar -jxvf Sublime Text 2.0.1.tar.bz2 -C /opt/

3.链接`sublime`的启动文件到`/usr/bin`，以便可以在终端使用`sublime`启动：   

	ln -s /opt/Sublime\ Text\ 2/sublime_text /usr/bin/sublime
				   
4.建立桌面快捷方式，使用`sublime`新建`sublime.desktop`：   
	
	sublime /usr/share/applications/sublime.desktop
  
并在其中加入下面内容：      

	[Desktop Entry]
	Version=1.0
  	Name=Sublime Text 2
 	# Only KDE 4 seems to use GenericName, so we reuse the KDE strings.
  	# From Ubuntu's language-pack-kde-XX-base packages, version 9.04-20090413.
  	GenericName=Text Editor

  	Exec=sublime
  	Terminal=false
  	Icon=/opt/Sublime Text 2/Icon/48x48/sublime_text.png
  	Type=Application
  	Categories=TextEditor;IDE;Development
  	X-Ayatana-Desktop-Shortcuts=NewWindow

  	[NewWindow Shortcut Group]
  	Name=New Window
  	Exec=sublime -n
	TargetEnvironment=Unity

##Package Control组建安装
1.按Ctrl+`调出`console`       
2.粘贴以下代码到底部命令行并回车：         

	import urllib2,os;pf='Package Control.sublime-package';ipp=sublime.installed_packages_path();os.makedirs(ipp) if not os.path.exists(ipp) else None;open(os.path.join(ipp,pf),'wb').write(urllib2.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read())

3.重启`Sublime Text 2`     
4.如果在`Perferences->package settings`中看到`package control`这一项，则安装成功。   

##插件安装
1.按下`Ctrl+Shift+P`调出命令面板     
2.输入`install`调出 `Install Package` 选项并回车，然后在列表中选中要安装的插件。     

[1]:http://www.sublimetext.com/2
