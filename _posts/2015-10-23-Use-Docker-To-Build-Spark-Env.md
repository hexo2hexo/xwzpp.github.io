---
layout: post
title:   利用Docker搭载本地的spark环境
description: "利用Docker搭载本地的spark环境"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [Docker,Spark]
duoshuo: true
---
最近换了新电脑，需要配置一下本地的spark环境，为了方便一次配置，到处运行，本文采用docker的容器机制来搭建本地的spark环境。

本人涉及docker不深，如有错误，希望大家多多包涵指教！么么哒，大家！

<!-- more -->

## 一.下载docker并安装
首先根据自己电脑的信息下载对应的docker，我的电脑是mac,os的版本为10.10，所以我选择下载[docker toolbox](https://www.docker.com/docker-toolbox)进行docker的安装。（**window的用户记得需要是64位的哦**）.

补充：上面的docker-toolbox下载链接为国外链接，速度很慢，所以本人采用DaoCloud提供的国内镜像进行下载，下载链接为：<https://get.daocloud.io/toolbox/>

下载之后，安装非常简单，直接傻瓜式操作就可以了。然后运行，如果出现下面这个界面说明已经安装成功。
![](/img/use-docker-to-build-spark-env/1.png)

##二.下载spark镜像

