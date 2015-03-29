---
layout: post
title:  使用HashPartitioner来调节Reducer的计算负载
description: "使用HashPartitioner来调节Reducer的计算负载"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [Hadoop,Mapreduce]
duoshuo: true
---

##一、实验内容
本节介绍如何使用HashPartitioner将Mapper的输出按照key进行分组后交给Reducer来处理。合理的分组策略将使得每个Reducer获得的计算负载差距不大，从而整体reduce的性能更加均衡。

<!-- more -->

Reducer的数量由HashPartitioner函数getPartition返回值来确定。
{% highlight java %}
public int getPartition(K2 key, V2 value, int numReduceTasks) {  
    return (key.hashCode() & Integer.MAX_VALUE) & numReduceTasks;  
}  
{% endhighlight %}

上面的代码表示根据key的hash code 除以2的31次方后取余数，用该余数再次除以reducer的数量，再取余数。得到的结果才是这个key对应的partition的编号。
原因是 Integer.MAX_VALUE是2的31次方-1, 一个数如果和一个2的N次方-1的数 按位与 就 等价于 这个数对2的N次方取余数。

参考文档：

http://blog.csdn.net/csfreebird/article/details/7355282

所有计算出来属于同一个partition的key，以及它的value都会被发送到对应的reducer去做处理。

所以结论如下：

partitioner不会改变reducer的数量，而会决定哪些<key,value>进入哪个组，从而改变reducer处理的数据的量

在MapReduce4的基础上，仅仅修改了LogJob.java的一行代码：
{% highlight java %}
job.setPartitionerClass(HashPartitioner.class);   
{% endhighlight %}

其实如果不设置，默认Hadoop用的就是HashPartitioner。

## 二、小结

MapReduce中可以使用HashPartitioner中的getPartition来调节Reducer的计算负载，Hadoop默认使用的就是HashPartitioner。
