---
layout: post
title:  CentOS6.5 安装git
description: "CentOS6.5 安装git"
category: project
avatarimg: "/img/touxiang.png"
tags : [blog,git]
duoshuo: true
---
##引言
Git是目前世界上最先进的分布式版本控制系统，它能够对你的代码进行版本管理与控制，使你不再需要担心代码版本过多而造成发布时版本的混乱。

本文是在CentOS6.5上安装git，使得在linux上也可以使用git进行代码的版本控制。

<!-- more -->

##yum安装git
在CentOS6.5上不需要下载git源码进行编译，而直接只需要通过yum来下载安装git。	
安装命令如下：
```
$ yum install git
```

##查看git版本
为了查看git是否安装成功，我们可以打印出git的版本号以便查看。   
打印命令如下：
```
$ git --version
git version 1.7.1
```

##配置git
配置你的用户名和电子邮件：
```
$ git config --global user.name "your name"
$ git config --global user.email "your email"
```

##拷贝远程库
可以拷贝你github上的库到本地进行修改。	
拷贝命令如下：
```
例如你需要拷贝用户名为：baidu下的example项目
$ git clone https://github.com/baidu/example
```

##提交本地库
当把远程库考到本地后进行修改后，需要提交到远程库中，此时需要提交命令。	
提交命令如下：
```
$ git add .
$ git commit -a -m "your message"
$ git push
```
**提交错误**处理：
>git push 出错
>```
error: The requested URL returned error: 403 Forbidden while accessing https://github.com/wangz/future.git/info/refs  
```
>解决方案：	
 修改.git下面的config文件

>修改以下代码：
>```
[remote "origin"]  
    url = https://github.com/wangz/example.git  
>```
>为：
>```
[remote "origin"]  
    url = https://wangz@github.com/wangz/example.git  
>```

>再次git push，弹出框输入密码，即可提交

##参考文献
[廖雪峰的git教程] [1]
[CentOS 安装git] [2]

[1]: http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
[2]: http://blog.csdn.net/harith/article/details/17691839



