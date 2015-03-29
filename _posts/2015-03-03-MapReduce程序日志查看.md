---
layout: post
title:  MapReduce程序日志查看
description: "MapReduce程序日志查看"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [apue,Hadoop]
duoshuo: true
---


##一、实验内容
首先，如果需要打印日志，不需要用log4j这些东西，直接用System.out.println即可，这些输出到stdout的日志信息可以在jobtracker站点最终找到。

其次，如果在main函数启动的时候用System.out.println打印的日志，直接在控制台就可以看到。

再其次，jobtracker站点很重要。

	http://localhost:50030


注意，在这里看到Map 100%不一定正确，有时候会卡在Map阶段并没有完成，而此时居然显示Map 100%，所以要一层层的点进去，直到看到日志为止。

另外，在cluster summary表格中可以看到map/reduce slots的情况，方便了解集群计算资源。可以写个脚本定时收集slots信息，方便分析出集群高峰和空闲时间段。

<!-- more -->

##二、执行流程

![](http://anything-about-doc.qiniudn.com/mapreduce%2F2.jpg)

##三、执行原理

![](http://anything-about-doc.qiniudn.com/mapreduce%2F3.jpg)

## 四、小结

我们可以访问http://localhost:50030查看运行详情。
