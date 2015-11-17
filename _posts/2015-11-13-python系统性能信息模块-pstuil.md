---
layout: post
title:   python系统性能信息模块-psutil
description: "python系统性能信息模块-psutil"
category: project
avatarimg: "/img/touxiang.jpg"
tags : [运维,Python]
duoshuo: true
---
psutil模块能够轻松获取系统能够运行的进程和系统利用率（包括CPU、内存、磁盘、网络等）信息。主要用于系统监控，分析和限制系统资源及进程的管理。

它实现了很多同等命令行工具提供的功能，如ps、top、df等。

<!-- more -->
## 一. psutil的安装与基本使用
楼主本人使用的系统是osx 10.11.1。使用的python版本是系统自带的2.7.10.

#### 下载软件包
psutil的下载网址为:[下载网址][1]。然后选择`psutil-3.2.2.tar.gz`进行下载。

具体安装步骤：

```
1. tar -zxvf psutil-3.2.2.tar.gz
2. cd psutil-3.2.2
3. sudo python setup.py install
```
#### psutil的基本使用
首先需要进行模块的导入，然后就可以进行使用了，具体事例如下：

```
import psutil  
print psutil.virtual_memory()
```

## 二. 系统性能信息
psutil模块已经分装了系统性能信息的方法，主要分为以下几个方面：
#### CPU

```
# 获取CPU完整信息  
print psutil.cpu_times()  

# 获取单项数据信息,如user的CPU时间比  
print psutil.cpu_times().user  

# 获取cpu的逻辑个数  
print psutil.cpu_count()  

# 获取cpu的物理个数  
print psutil.cpu_count(logical=False)
```

#### 内存

```
#获取内存全部信息
print psutil.virtual_memory()

#获取内存总数
print psutil.virtual_memory().total

#获取空闲内存属
print psutil.virtual_memory().free

#获取SWAP分区信息
print psutil.swap_memory()

```

#### 磁盘

```
#获取磁盘的完整信息
print psutil.disk_partitions()

#获取分区的使用情况
print psutil.disk_usage('/')

#获取硬盘总的IO个数
print psutil.disk_io_counters()

#获取单个分区IO个数
print psutil.disk_io_counters(perdisk=True)
```

#### 网络

```
#获取网络总的IO信息
print psutil.net_io_counters()

#获取每个网络接口的IO信息
print psutil.net_io_counters(pernic=True)

```

####其他系统信息（登陆用户，开机时间）

```
获取当前登陆系统的用户信息
print psutil.users()

#获取开机时间,以linux时间戳的格式返回
import datetime
print datetime.datetime.fromtimestamp(psutil.boot_time()).strftime("%Y-%m-%d %H:%M:%S")
```

##三. 系统进程管理方法
获取当前系统的进程信息，可以得知程序的运行状态，包括进程的启动时间、查看或设置CPU亲和度、内存使用率、IO信息、socket链接、线程数等，通过这些信息可以很好的看出进程的状态，以便进行优化。

####进程信息
获取全部进程的信息，或者根据一个进程ID得到进程的process对象，然后获取该进程的一些信息。

```
#获取所有进程的PID
print psutil.pids()

#实例化一个process对象,参数为一个进程PID
p=psutil.Process(1788)
print p.name() #进程名
print p.exe()  #进程路径
print p.cwd() #进程工作目录绝对路径
print p.status() #进程的状态
print p.create_time() #进程创建的时间
print p.uids() #进程uid信息
print p.gids() #进程gid信息
print p.cpu_times() #进程CPU时间信息
print p.cpu_affinity() #进程cpu亲和度
print p.memory_percent() #进程内存利用率
print p.memory_info() #进程内存rss,vms信息
print p.io_counters() #进程IO信息
print p.connections() #打开进程socket的namedutples列表
print p.num_threads() #进程开启的线程数
```
####Popen类的使用
psutil提供的Popen类的作用是获取用户启动的应用程序进程信息，以便跟踪程序进程的运行状态。

```
#通过psutil的Popen方法启动的应用程序,可以进行跟踪
from subprocess import PIPE
p=psutil.Popen(["/usr/bin/python","-c","print('hello')"],stdout=PIPE)
print p.name()
print p.username()
print p.cpu_times()

```

##四. 参考文档
1. [psutil的github地址][2]
2. [psutil的文档说明][3]






[1]:	https://pypi.python.org/simple/psutil/
[2]:  https://github.com/xwzpp/psutil
[3]:  http://pythonhosted.org/psutil/