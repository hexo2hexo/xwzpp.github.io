---
layout: post
title:  CentOS下配置"Unix环境高级编程第三版"中的apue.h
description: "CentOS下配置<<Unix环境高级编程第三版>>中的apue.h"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [apue,CentOS]
duoshuo: true
---
##引言
最近在看<<Unix环境高级编程第三版>>，其中代码中都包含了apue.h头文件。因此如果想用这个头文件，需要自己配置。

<!-- more -->

##下载apue.3e解压
下载地址为：[Unix环境高级编程第三版][1]

##拷贝apue.h到库目录

	cp  apue.3e/include/apue.h  /usr/include

##编程实例
为了方便编译自己写的代码，可以使用make工具进行简化。但是我们需要编写makefile文件。   
其格式如下：

	//生成main的可执行文件，其中有main.o文件，并需要调用/usr/local/src/error.o库文件
	LIBS = /usr/local/src/error.o
	OBJS = main.o
	main:${OBJS}
		gcc -o main ${OBJS} ${LIBS}
	clean:
		rm -f main ${OBJS}

然后编译时，只需要执行`make`即可。

[1]:http://www.apuebook.com/ 


