---
layout: post
title: "Netty笔记"
tag: Netty 
---   
# Netty笔记

----

## Netty核心组件  
- Channel
- 回调
- Future
- 事件和ChannelHandler

### Channel  
Channel是Java NIO的一个基本构造。  
它代表一个到实体（类似文件或者网络Socket）的开放连接，如读操作和写操作。  

### 回调
用户事件通知。    

### Future
用户事件通知。  

### 事件和ChannelHandler    
- 入站事件：
    1. 连接已被激活或者连接失活
    2. 数据读取
    3. 用户事件
    4. 错误事件
- 出站事件：
    1. 打开或者关闭到远程节点的连接
    2. 将数据写到或者冲刷到套接字

每个事件都将分发给ChannelHandler类中的某个用户实现的方法。
```
入站事件->入站处理器->入站事件->入站处理器->入站事件->

<-出站事件<-出站处理器<-出站事件<-出站处理器<-出站事件
```

----

## Netty组件设计
### Channel, Eventloop和ChannelFuture
- Channel: Socket
- EventLoop: 控制流，多线程控制，并发
- ChannelFuture: 异步通知

### Channel接口
封装了基本的I/O操作(bind(), connect(), read(), write())。
- EmbeddedChannel；
- LocalServerChannel；
- NioDatagramChannel；
- NioSctpChannel；
- NioSocketChannel。

传输API的核心是Channel接口，它被用于所有的I/O操作。  
```
 java.lang.Comparable                          AttributeMap
         |___________________________________________|
                               |
                            Channel
                               |
    +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
    |                +                      +                 |
    |                +                      +                 |
ServerChannel    ChannelPipeline     ChannelConfig      AbstractChannel
```  
每个Channel都将会被分配一个ChannelPipeline和ChannelConfig。ChannelConfig包含了该Channel的所有配置设置，并且支持热更新。

