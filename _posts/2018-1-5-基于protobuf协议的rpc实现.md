---
layout: post
title: 基于protobuf协议的rpc实现(python)
date: 2018-1-5
tag: 开发语言
---


### 需求背景介绍
直播云服务端的推流模块relay的流信息相关会上报manager，manager是对relay的信息管理，我们在测试的过程中会经常需要查询某个流是否推到了relay上或者要查询relay节点的相关信息，需要后台看日志或者调用命令比较麻烦基于这个需求可以做个工具供测试和开发人员使用，relay和manager之间的调用死选择的rpc协议而数据传输是基于谷歌的protobuf,那么什么是rpc，什么是protobuf呢，两者这件的关系又是怎么样的呢？

### rpc定义
rpc其实就是远程调用，我们日常接触的系统都是由不同服务器上的不同服务组合而成，比如我们的relay和manager,一个部署在A，一个部署在B，假如A要调用B的函数方法，由于不在一个服务器上那么久需要通过网络来传递数据，而基于rpc框架帮你完成了底层TPC的socket的连接和传输过程，只需要调用就可以了，省去很多处理连接的相关步骤，常见的rpc框架我们肯定听过在java web应用中常见的rpc框架比如：dubbo(阿里),Thrift（facebook）,netty等

### protobuf和grpc
**要完成rpc通信需要两种协议：对象序列化协议 和 调用控制协议**

 - protobuf就是对象序列化协议,是大名鼎鼎的谷歌公司开源的协议具有比xml可读性更强，可以使用代码生成器来读这个数据结构很方便，下面会介绍的如何生成，使用protobuf需要定义个.proto的文件，以下我们的业务的部分message的数据结构定义的样子，而且如果你想变更数据结构只需要替换一下定义文件再生成一遍就好非常快捷方便易扩展，同时支持JAVA,C++,PHP,PYTHON等语言，（manager_monitor.proto）
![这里写图片描述](http://img.blog.csdn.net/20180105150915310?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYTExZW5fMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

 - grpc是说白了就是封装了底层的socket及传输的rpc框架，具体原理有兴趣同学可以参考官网：http://www.grpc.io/，同样支持java,python,c++等语言，通过grpc我们可以在.proto的文件中定义相关的相关的服务可以通过不同语言去实现客户端的调用，下面是我们的项目中的service的定义（manager_monitor.proto）
![这里写图片描述](http://img.blog.csdn.net/20180105151030871?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYTExZW5fMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### protobuf&grpc环境搭建
 定义好了数据结构了就要开始搭建环境客户端调用了，首先去protobuf官网址https://github.com/google/protobuf/releases下载最新版本，解压之后
 **./configure --prefix=/usr/local/protobuf
 make 
 make check 
 make install** 
根据以上步骤安装就好，这里我遇到的坑说一下（新的protobuf里含有c++11以上的api所以我们系统自带的gcc and g++编译版本可能过低需要修改gcc 和g++的版本到4.8以上）
安装成功后在/protobuf-3.1.0/bin 会生成一个可执行命令"protoc"后续用来生成rpc代码使用
     grpc下载直接git clonehttps://github.com/grpc/grpc.git  
    具体安装方式可以详见官网的提示即可很简单的http://www.grpc.io/docs/quickstart/python.html 安装完成后   
在其/grpc/examples/python 目录下有python的教程，这里我用的是python，当然也支持c、java、php等语言各位对号入座就可以，官方提供了helloword、multiplex、route quide这几个demo用来供用户学习grpc使用，这几个demo涵盖了rpc返回各种流式数据的解析用例
所有的环境已经准备就绪，这时我把我上面的manager_monitor.proto放到grpc下的protos文件夹下在grpc 提供的demo helloword 下执行命令: python -m grpc_tools.protoc -I../../protos --python_out=. --grpc_python_out=. ../../protos/helloworld.proto
 就会生成manager_monitor_pb2.py 和 manager_monitor_pb2_grpc.py这个两个文件，rpc的文件封装了底层的传输层相关东西，另一个文件则生成了符合其规则的数据结构文件，一切就绪之后就可以实现服务端定义的接口写客户端去调用了
根据官网提供的demo 比葫芦画瓢实现我们自己的业务就可以了

### 具体客户端调用
![这里写图片描述](http://img.blog.csdn.net/20180105151041206?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYTExZW5fMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
**是不是很简单，这样我们就可以得到了上面manager_monitor.proto中第一个定义的service接口中GetNodeList的数据了
在结合flask框架，对自己的业务在做一下封装和具体数据解析传递，一个简单实用的查询工具就出来了，其他需要查询relay信息的测试、开发、运维同学不用安装比较麻烦的的环境用这个工具就可以辅助排查问题了**
![这里写图片描述](http://img.blog.csdn.net/20180105151059118?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYTExZW5fMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
谢谢~ 有理解不对的地方，还请见谅~~


