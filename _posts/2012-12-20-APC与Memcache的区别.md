---
layout: post
title: "APC与Memcache的区别"
description: "搜集和汇总了一些APC和Memcache的区别"
category: 缓存
tags: [APC, Memcache]
---
搜集和汇总了一些APC和Memcache的区别

APC和Memcache都是基于内存的缓存方案，最大的区别在于APC用于单机缓存，而Memcache可以应用于分布式，跨服务器缓存。

APC不能用户频繁写，主要测试读方面的性能，这点上是Memcache望尘莫及的。

APC的性能会随着数据库量的增加而下降，这点Memcache会更占优势（因为可以增加服务器达到共享更多的内存）。

单机内存缓存够用的话，APC的性能是最好的。因为Memcache还是需要维护通信进程，如果内网多台服务区假设Memcache，影响不大，但外网（跨域）的话，性能会耗费到与客户端的TCP连接通讯上。

APC是mmap，而Memcache使用的是纯内存。

Memcache本身的设计就是为了分布式应用，大规模内存缓存，集群，易扩展等。

缓存的对象也不同，APC可以缓存：
1. opcodes（和eAccelerator一样）
2. key-value缓存 （用户缓存）
而Memcache只有key-value缓存

其实，纯粹的使用这些缓存类工具是比较简单的，无非就是把一部分常用的数据存储到内存中，降低硬盘的IO消耗，更复杂，需要关注的是：
1. 对哪些数据使用缓存
2. 缓存数据时采用什么样的架构
3. 缓存周期的控制

{% include JB/setup %}
