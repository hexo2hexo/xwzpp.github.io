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
本文选取的镜像是dockerhub上的[sequenceiq/spark](https://hub.docker.com/r/sequenceiq/spark/)镜像，由于国内的原因，直接从dockerhub上下载速度很慢，因此我选择daocloud进行加速。

具体加速配置请参考：<https://dashboard.daocloud.io/mirror>

配置完成后，就可以使用`dao pull`进行镜像的拉去，速度还是不错滴，推荐大家试试。

###1.拉取spark镜像
首先如果是安装的docker toolbox,则首先输入 
   
```
docker-machine ssh default
```

进入终端。而boot2docker可以使用 

```
boot2docker ssh
```
进入之后直接输入

```
dao pull sequenceiq/spark:1.3.1
```
进行spark镜像的拉取。（**这次已经采用了daocloud进行了加速，所以才哟过dao命令进行拉取**）

------
#####注意点：
**在此处存在一个问题，楼主由于学校网络差的缘故，导致从daocloud上也拉取不了该镜像。因此楼主购买了一台阿里云服务器来拉取该镜像，在云主机中将该镜像通过`docker save`打包成一个tar文件，然后再SSH上去，将该tar文件拉取到本地，然后通过`docker load`进行加载。**

###2.运行spark容器
具体可以参考以下网址：<https://github.com/sequenceiq/docker-spark>     
上面写的非常清楚，按照步骤就可以得到spark的容器。

输入`docker images`可以查看本地的及docker镜像。     
![docker images](/img/use-docker-to-build-spark-env/2.png)

输入`docker ps`可以查看本地运行的docker容器。     
![docker images](/img/use-docker-to-build-spark-env/3.png)

###3.测试pi程序
由于spark容器已经运行起来了，我们可以测试下pi是否可以计算。    
该镜像中spark的运行模式为两种，分别为`yarn-client`和`yarn-cluster`,具体的运行命令依旧参考上述网址[^1]。

---
####注意点：
**如果你采用的是boot2docker,请确保分配给虚拟机的内存大于2G。同时，为了方便通过本地的UI查看任务的运行情况，请在运行容器时，暴露8088和8042两个端口。**

###4.总结
采用docker进行本地spark环境的搭建，可以做到只需构建一次spark镜像，就可以到处运行的效果，这样不需要每次系统更换，都需要重新配置spark环境，直接利用docker启动即可，非常方便。


[^1]: https://github.com/sequenceiq/docker-spark.