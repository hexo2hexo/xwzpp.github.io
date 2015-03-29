---
layout: post
title:  MapReduce快速入门
description: "MapReduce快速入门"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [apue,Hadoop]
duoshuo: true
---

##一、MapReduce介绍
MapReduce是一种编程模型，用于大规模数据集（大于1TB）的并行运算。概念&#34;Map（映射）&#34;和&#34;Reduce（归约）&#34;，和他们的主要思想，都是从函数式编程语言里借来的，还有从矢量编程语言里借来的特性。他极大地方便了编程人员在不会分布式并行编程的情况下，将自己的程序运行在分布式系统上。 当前的软件实现是指定一个Map（映射）函数，用来把一组键值对映射成一组新的键值对，指定并发的Reduce（归约）函数，用来保证所有映射的键值对中的每一个共享相同的键组。

<!-- more -->

##二、搭建MapReduce工程
使用Eclipse创建一个名为MapReduce1的Java Project，在MapReduce1下创建一个名为lib的文件夹，放入hadoop-core-1.2.1.jar（在主文件夹下的Downloads/hadoop-1.2.1文件夹下），并把它添加到Build Path，最后在src下创建一个com.shiyanlou.mapreduce的包。

![](http://anything-about-doc.qiniudn.com/mapreduce/1.png)

##三、MapReduce基本流程
MapReduce的基本流程是，框架会使用FileInputFormat读取文件，默认会根据文件大小的进行记录拆分，这里拆分器叫做InputSplitter。通过InputSplitter将文件拆成若干块，后面也就有若干个mapper与之对应。

InputSplitter里面使用RecordReader对文件块的记录进行读取，生成key/value的pair，调用mapper的map函数去处理。

当然这些流程中有些可以定制，比如InputSplitter的算法可以修改，RecordReader也是可以定制。

而且还有一个非常有效的方法，可以避免mapper将过多的数据传递给reducer。

比如有个例子都是1, 其实可以先用一个HashMap对key做分组，有则value加1, 无则添加到HashMap中。

最后将分组统计后的key/value数据通过context.write方法发送给reducer，能够大大提高效率。

##四、编写简单mapper
现在想从日志中提取数据，部分日志文件如下：

	2014-05-10 13:36:40,140307000287,536dbacc4700aab274729cca,login
	2014-05-10 13:37:46,140310000378,536dbae74700aab274729ccb,login
	2014-05-10 13:39:20,140310000382,536dbb284700aab274729ccd,login
	2014-05-10 13:39:31,140331001080,536dbb864700aab274729ccf,login
	2014-05-10 13:39:45,140331001105,536dbba04700aab274729cd4,login
	2014-05-10 13:39:45,140328000969,536dbba04700aab274729ce4,login
	2014-05-10 13:39:45,140408001251,536dbba04700aab274729cd8,login
	2014-05-10 13:39:45,140328000991,536dbba04700aab274729ce9,login
	2014-05-10 13:39:45,140324000633,536dbba14700aab274729cf5,login
	2014-05-10 13:39:45,140331001077,536dbba04700aab274729cdd,login
	2014-05-10 13:39:45,140408001242,536dbba04700aab274729cd7,login
	2014-05-10 13:39:45,140327000941,536dbba14700aab274729cf1,login
	2014-05-10 13:39:45,140408001265,536dbba04700aab274729ce5,login
	2014-05-10 13:39:45,140324000673,536dbba04700aab274729cd3,login
	2014-05-10 13:39:45,140331001066,536dbba04700aab274729cd5,login
	2014-05-10 13:39:45,140408001292,536dbba14700aab274729cee,login
	2014-05-10 13:39:45,140328000966,536dbba14700aab274729cec,login
	2014-05-10 13:39:45,140312000501,536dbba04700aab274729ce1,login
	2014-05-10 13:39:45,140306000216,536dbba14700aab274729d02,login
	2014-05-10 13:39:45,140327000856,536dbba04700aab274729ce2,login
	2014-05-10 13:39:46,140328000985,536dbba14700aab274729cf7,login
	2014-05-10 13:39:46,140306000245,536dbba14700aab274729d0d,login
	2014-05-10 13:39:46,140326000797,536dbba14700aab274729cf6,login
	2014-05-10 13:39:46,140328000993,536dbba14700aab274729d12,login
	2014-05-10 13:39:46,140331001115,536dbba14700aab274729d10,login
	2014-05-10 13:39:46,140325000744,536dbba04700aab274729ce0,login
	2014-05-10 13:39:46,140328000982,536dbba14700aab274729d0a,login
	2014-05-10 13:39:46,140331001063,536dbba04700aab274729ce3,login
	2014-05-10 13:39:46,140331001067,536dbba14700aab274729d1c,login
	2014-05-10 13:39:46,140401001157,536dbba04700aab274729ce8,login
	2014-05-10 13:39:46,140408001216,536dbba14700aab274729cef,login
	2014-05-10 13:39:46,140401001174,536dbba14700aab274729d27,login
	2014-05-10 13:39:46,140306000215,536dbba04700aab274729cde,login
	2014-05-10 13:39:46,140331001064,536dbba04700aab274729cdc,login
	2014-05-10 13:39:46,140326000825,536dbba04700aab274729cd9,login
	2014-05-10 13:39:46,140408001294,536dbba14700aab274729d0f,login


希望将login前面的设备ID取出来，进行数量的统计，最后得到结果。
例如：

	536dbba04700aab274729cdc	1
	536dbba04700aab274729cdd	91
	536dbba04700aab274729cde	152


我们可以创建一个LogMapper类，该类负责做数据的Map，前两个模板参数用于KeyIn和ValueIn, 后两个模板参数用于KeyOut和ValueOut，都是代表类型。

假定一个&lt; KeyIn， ValueIn&gt;组成一个pair，输入的很多pair在一个组里面, 这些pair被一定的算法Map之后，会变成很多组pair。

官方文档：http://hadoop.apache.org/docs/r2.4.1/api/org/apache/hadoop/mapreduce/Mapper.html

	Maps input key/value pairs to a set of intermediate key/value pairs.


注意，这里的Mapper类用的包是mapreduce，以前有一个老的叫mapred。
这里介绍了两者的区别：

http://stackoverflow.com/questions/7598422/is-it-better-to-use-the-mapred-or-the-mapreduce-package-to-create-a-hadoop-job

有两个类LongWritable和IntWritable，用于帮助创建可以Long和Int类型的变量。它们能够帮助将Long和Int的值序列化成字节流，因此都有两个关键方法读入和写出：
![](http://anything-about-doc.qiniudn.com/mapreduce%2F1.jpg)
这个和Hadoop内部RPC调用时采用的序列化算法有关。
在com.shiyanlou.mapreduce包下新建一个名为LogMapper的类，代码为：
{% highlight java %}
	package com.shiyanlou.mapreduce;
	
	import java.io.IOException;
	
	import org.apache.hadoop.io.IntWritable;
	import org.apache.hadoop.io.Text;
	import org.apache.hadoop.mapreduce.Mapper;
	
	public class LogMapper extends Mapper&lt;Object, Text, Text, IntWritable&gt; {
		private final static IntWritable ONE = new IntWritable(1);
	
		public void map(Object key, Text value, Context context)
				throws IOException, InterruptedException {
			String[] line = value.toString().split(&#34;,&#34;);
			if (line.length == 4) {
				String dId = line[2];
				context.write(new Text(dId), ONE);
			}
		}
	}
{ % endhighlight %}


这个Mapper的子类覆盖了map函数，将字符串用,号拆开后，取出第三个元素作为设备ID, 然后作为key写入context对象。
这里value设置为1, 因为后面reduce阶段会简单的求和。

Context类文档参考： http://hadoop.apache.org/docs/r1.1.1/api/org/apache/hadoop/mapreduce/Mapper.Context.html

write方法不是一般概念的hasmap添加key,value，而是生成一个新的pair对象，里面包含了key和value。 如果多个key相同，也会产生多个pair对象，交给reduce阶段处理。

##六、编写简单reducer
Reduce就是做加和统计，在com.shiyanlou.mapreduce包下新建一个名为LogReducer的类，代码：
{% highlight java %}
	package com.shiyanlou.mapreduce;
	
	import java.io.IOException;
	
	import org.apache.hadoop.io.IntWritable;
	import org.apache.hadoop.mapreduce.Reducer;
	
	public class LogReducer&lt;Key&gt; extends
			Reducer&lt;Key, IntWritable, Key, IntWritable&gt; {
		private IntWritable result = new IntWritable();
	
		public void reduce(Key key, Iterable&lt;IntWritable&gt; values, Context context)
				throws IOException, InterruptedException {
			int sum = 0;
			for (IntWritable val : values) {
				sum += val.get();
			}
			result.set(sum);
			context.write(key, result);
		}
	}
{ % endhighlight %}

这里框架保证在调用reduce方法之前，相同的key的value已经被放在values中，从而组成一个pair &lt; key, values&gt;，这些pair之间也已经用key做了排序。

参考文档：https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/mapreduce/Reducer.html

迭代遍历values，取出所有的value，都是1, 简单加和。
然后结果写入到context中。 注意，这里的context是Reducer包的Context。

最后，在com.shiyanlou.mapreduce包下新建一个名为LogJob的类，将初始环境设置好。
{% highlight java %}
	package com.shiyanlou.mapreduce;
	
	import org.apache.hadoop.conf.Configuration;
	import org.apache.hadoop.fs.Path;
	import org.apache.hadoop.io.IntWritable;
	import org.apache.hadoop.io.Text;
	import org.apache.hadoop.mapreduce.Job;
	import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
	import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
	
	public class LogJob {
	
		public static void main(String[] args) throws Exception {
			Configuration conf = new Configuration();
			Job job = Job.getInstance(conf, &#34;sum_did_from_log_file&#34;);
			job.setJarByClass(LogJob.class);
	
			job.setMapperClass(LogMapper.class);
			job.setCombinerClass(LogReducer.class);
			job.setReducerClass(LogReducer.class);
	
			job.setOutputKeyClass(Text.class);
			job.setOutputValueClass(IntWritable.class);
	
			FileInputFormat.addInputPath(job, new Path(args[0]));
			FileOutputFormat.setOutputPath(job, new Path(args[1]));
	
			System.exit(job.waitForCompletion(true) ? 0 : 1);
		}
	}
{% endhighlight %}

##七、MapReduce例子程序运行
在Eclipse中将MapReduce1工程打成jar包，取名为MapReduce1.jar，放到主文件夹下。

![](http://anything-about-doc.qiniudn.com/mapreduce/2.png)

接下来进入主文件夹的Downloads/hadoop-1.2.1/bin下，右键打开命令行，首先格式化HDFS：

	$ ./hadoop namenode -format


然后启动Hadoop所有进程：

	$ ./start-all.sh


gitclone下来源代码，在主文件夹新建一个input文件夹，把源代码中的log文件放进去，再把input文件夹上传到HDFS：

	$ ./hadoop dfs -put ~/input input/


同时还要确保output目录不存在，该目录会被MapReduce程序创建，用于存放输出结果：

	$ ./hadoop dfs -rmr output


运行程序，观察输出结果：

	$ ./hadoop jar ~/MapReduce1.jar com.shiyanlou.mapreduce.LogJob input output


现在将output目录都复制到本地磁盘，查看结果：

	$ ./hadoop dfs -get output/ ~/output


然后进入本地output目录查看：

	$ cd ~/output
	$ ll -alh
	$ gedit part-r-00000


打开part-r-00000文件，可以看到结果如下：

	536dbacc4700aab274729cca	91
	536dbae74700aab274729ccb	91
	536dbb284700aab274729ccd	91
	536dbb864700aab274729ccf	91
	536dbba04700aab274729cd3	91
	536dbba04700aab274729cd4	91
	536dbba04700aab274729cd5	91
	536dbba04700aab274729cd7	91
	536dbba04700aab274729cd8	91
	536dbba04700aab274729cd9	1
	536dbba04700aab274729cdc	1
	536dbba04700aab274729cdd	91
	536dbba04700aab274729cde	152
	536dbba04700aab274729ce0	87
	536dbba04700aab274729ce1	87
	536dbba04700aab274729ce2	87
	536dbba04700aab274729ce3	87
	536dbba04700aab274729ce4	91
	536dbba04700aab274729ce5	91
	536dbba04700aab274729ce8	152
	536dbba04700aab274729ce9	91
	536dbba14700aab274729cec	87
	536dbba14700aab274729cee	87
	536dbba14700aab274729cef	138
	536dbba14700aab274729cf1	91
	536dbba14700aab274729cf5	91
	536dbba14700aab274729cf6	87
	536dbba14700aab274729cf7	87
	536dbba14700aab274729d02	87
	536dbba14700aab274729d0a	87
	536dbba14700aab274729d0d	87
	536dbba14700aab274729d0f	1
	536dbba14700aab274729d10	87
	536dbba14700aab274729d12	87
	536dbba14700aab274729d1c	152
	536dbba14700aab274729d27	152


## 八、小结
前面介绍了如何编写一个简单的日志提取程序，读取HDFS input目录下的日志文件，然后提取数据后，最终输出到output目录下。

现在梳理一下主要过程，然后提出新的改进目标。

+ 可比较的序列化
第一个是序列化，这是各种编程技术中常用的。MapReduce的特别之处在于由于key用来排序，所有它既要支持序列化和反序列化，同时也要支持比较大小的操作。因此通常使用的都是接口WritableComparable&lt; T&gt;，这个接口分别从Writable接口和java.lang.Comparable&lt; T&gt;接口继承。前者负责序列化，实现的就是类似流(stream)的功能，后者负责比较。
+ MapReduce计算流程
这里只是概括的介绍主要步骤：
1. 通过**InputFormat**读取HDFS目录的日志文件的所有行，进行内容分块。然后每个块都会对应一个mapper
2. 调用每个**Mapper**的map函数， 将内容块的数据按照行变成&lt; key, value&gt;格式，作为参数传递. map函数的代码由程序员自己实现，通常key是数据，value是整数，便于做统计。这样，也就将参数&lt; key, value&gt;改成了另一种符合业务逻辑的&lt; key, value&gt;, 通过Context.write方法写出去，随后会被框架交给Reducer
3. **Partitioner**目前这个程序中没有实现自己的类，只是简单使用了Reducer，后面会增加这部分的说明
4. 框架会根据key进行分组，组成&lt; key, values&gt;对， 调用**Reducer**的reduce函数，函数接受到Mapper传递来的&lt; key, values&gt;后再做统计
5. 输出成什么样的格式文件由**OutputFormat**来控制。
注意上面的几个粗体字，就是5大MapReduce组件。每个组件都是我们可以继承的类，然后MapReduce框架通过多态的方式来回调我们的子类实现的方法。
+ MapReduce Job的配置
有了上面的实现，还需要配置Job，并且在hadoop命令行中提交。
配置的话，直接new一个Job类，调用set方法进行相应的设置即可。 Job的父类是JobContext。
就在这里可以设置上面的5大组件类，用自己的类来替换。还可以设置Reducer的数量。