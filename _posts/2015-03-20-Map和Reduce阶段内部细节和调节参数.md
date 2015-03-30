---
layout: post
title:  Map和Reduce阶段内部细节和调节参数
description: "Map和Reduce阶段内部细节和调节参数"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [Hadoop,Mapreduce]
duoshuo: true
---

##一、实验内容
本节介绍Map和Reduce阶段内部细节和调节参数.

<!-- more -->

##二、Map阶段内部细节和调节参数
+ Map计算阶段
1. 如果Reduce number设置为0, Map阶段会直接将结果写入HDFS中。
2. 一般情况下，map包括以下几个阶段：
a. read阶段
  从一个或者多个输入目录中读取输入文件，通过RecordReader，从InputSplit中解析出一个个的&lt; key,value&gt;。
b. map阶段
  执行用户编写的map函数，产生新的&lt; key,value&gt;
c. collect阶段
  OutputCollection.collect函数一般在map函数内部调用，接受新的&lt; key,value&gt;，然后它的内部会调用Partitioner对数据分组，最后数据&lt; key,value,partition&gt;会被写入缓冲区（一般是环形缓冲区)MapOutputBuffer中。
d. spill阶段（包含combiner)
  如果缓冲区写满到一定程度，就会进入spill阶段往本地磁盘上写临时文件。
  首先会将需要spill的数据按照partition排序，每个partition的数据又按照key进行排序。
  然后按照partition的增序写到本地磁盘临时output/spillN.out， N表示spill的次数。如果自定义了combiner，就在这个阶段被调用用来对数据再做一次聚集操作。
e. merge阶段
 将所有临时文件合并成一个文件，供reduce阶段使用。

+ MapOutputBuffer
对于每一个Map，都有一个环形内存buffer用来缓存中间结果，这不仅可以缓存，而且还可以用来排序，被称为MapOutputBuffer, 设置这个buffer大小的配置是
io.sort.mb
默认值是100MB.
一般当buffer被使用到一定比例，就会将Map的中间结果往磁盘上写，这个比例的配置是：
io.sort.spill.percent
默认值是80%或者0.8.
在内存中排序缓存的过程叫做sort，而当超过上面的比例在磁盘上写入中间结果的过程称之为spill.
如果能够追踪到sort和spill的状态，就可以通过调整上面两个参数对Map进行优化。
MapOutputBuffer内部有二级索引，第一级是对partition在二级索引中的位置建立索引，第二级是对partition内部的key,value在缓存中的位置建立索引。
这两级索引所占用的内存大小在整个缓存大小的比例由一个参数来控制：
io.sort.record.percent，默认是0.05.
+ Merge
Map的输出结果在combine阶段，最后会将多个spill临时文件合并成一个文件
每次并行merge多少个spill文件，有一个配置参数：io.sort.factor。这个参数名称特别奇怪，很容易理解成是collect或者spill阶段的调优。
默认为100, 如果文件很多，影响到了merge阶段完成的速度，可以适当调大以减少磁盘I/O。
+ 压缩
设置mapred.output.compress为true或者false，可以控制map的输出结果文件变为压缩或者不压缩。
同时可以指定压缩格式，用参数mapred.output.compression.codec，可选值为：zipCodec，LzoCodec，BZip2Codec，LzmaCodec  
选择压缩主要的时机是当磁盘I/O成了瓶颈，而不是CPU计算成瓶颈时。
压缩格式的选择也是在压缩时间，CPU利用率和磁盘空间三者间做平衡。

其他参数参考官方文档：
https://hadoop.apache.org/docs/r1.0.4/mapred-default.html

##三、Reduce阶段内部细节和调节参数
+ Reduce计算分为若干阶段
1. copy(或者叫shuffle)阶段和merge阶段并行
之前Map产生的结果被存放在本地磁盘上，这时需要从reduce节点将数据从map节点复制过来。放得下进内存，比较大的则写到本地磁盘。
同时，有两个线程对已经获得的内存中和磁盘上的数据进行merge操作。
具体细节是：
通过RPC调用询问task tracker已经完成的map task列表，shuffle（洗牌）是对所有的task tracker host的洗牌操作，这样可以打乱copy数据的顺序，防止出现网络热点（大量进程读取一个task tracker节点的数据）。
可以复制的任务被存放在scheduledCopies中。
一旦有了要复制到数据，会启动多个MapOutputCopier线程，通过HTTP GET请求复制数据，如果数据较大，存入磁盘，否则存入缓存。
对于缓存中，有线程InMemoryFSMerge线程负责merge，对文件，有LocalFSMerger线程负责merge。
因此观察jobtracker会看到map操作还没有完全结束，reduce操作已经开始了，就是进入了copy阶段。
2. sort阶段和调用reducer的reduce函数的并行
sort对Map阶段传来的&lt; key,value&gt; 数据针对key执行归并排序，产生&lt; key, values&gt;
用户编写的reduce将上面的&lt; key, values&gt;传递进ruduce函数处理
并行的算法提高了程序性能，具体算法以后再探讨。
3. write
将结果写到HDFS上。
+ Reduce的调优参数
mapred.reduce.parallel.copies 默认是5，表示有多少个并发线程去从task tracker节点复制数据
io.sort.factor 又出现了，默认10,仍然指的是并行合并文件的数目
mapred.job.shuffle.merge.percent 默认是0.66, 超过66%，就会将开始合并，然后往磁盘上写数据
mapred.inmem.merge.threshold 默认是1000，超过这个临界值，就会将开始合并，然后往磁盘上写数据

## 三、结合

MapReduce中Map阶段主要可分为read阶段、map阶段、collect阶段、spill阶段、merge阶段，Reduce阶段主要可分为copy阶段和merge阶段并行、sort阶段和调用reducer的reduce函数的并行、write阶段，我们可以通过修改一些参数来进行调优。
