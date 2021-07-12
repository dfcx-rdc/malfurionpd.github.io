---
title: "Java Concurrency Art Notes"
date: 2021-06-24T09:31:28+08:00
draft: true
---



+++

title = "Java并发编程艺术 笔记"
description = "Java并发编程艺术 笔记"
author = "adeng"
tags = [
    "java",
    "concurrency",
]
date = "2021-06-24"
categories = [
    "Java", "Concurrency"
]

image = "WX20210421-201335@2x.png"

+++



## 第1章 并发编程挑战

### 1.1 上下文切换

CPU分配给线程的时间片一般是几十毫秒(ms)

不可忽视线程有创建和上下文切换的开销



>线程切换具体带来哪些开销？时间大概是？
>
>参考 [进程/线程上下文切换会用掉你多少CPU？](https://zhuanlan.zhihu.com/p/79772089) 大约是**2.7-5.48us**



减少上下文切换的方法有：

* 无锁并发编程：锁会引起线程切换
* CAS算法：不需要加锁
* 使用最少的线程
* 协程



>锁的内存语义？
>
>



### 1.2 死锁

避免死锁的方式：

* 避免一个线程获取多个锁
* 避免一个线程在锁内占用多个资源
* 使用定时锁
* 数据库锁，加解锁在一个连接里



### 1.3 资源限制的挑战





## 第2章 Java并发机制底层原理

依赖于JVM实现和CPU指令



### 2.1 volatile

保证共享变量的多线程"可见性"，volatile 是轻量级的 synchronized，不会引起线程切换



Java 语言规范第 3 版中对 volatile 的定义如下：Java 编程语言允许线程访问共享变

量，为了确保共享变量能被准确和一致地更新，线程应该确保通过排他锁单独获得这个

变量。Java 语言提供了 volatile，在某些情况下比锁要更加方便。如果一个字段被声明成

volatile，Java 线程内存模型确保所有线程看到这个变量的值是一致的。



> 内存屏障



> cache line
>
> [CPU Cache与缓存行](https://blog.csdn.net/u010983881/article/details/82704733)
>
> [Cache与内存的映射](https://zhuanlan.zhihu.com/p/242749870)



有 volatile 变量修饰的共享变量进行写操作的时候会多出第二行汇编代码

`0x01a3de1d: movb $0×0,0×1104800(%esi);0x01a3de24: lock addl $0×0,(%esp); `

Lock 前缀的指令在多核处理器下会引发了两件事情：

* 将当前处理器缓存行的数据写回到系统内存。

* 这个写回内存的操作会使在其他 CPU 里缓存了该内存地址的数据无效。



### 2.2 synchronized

 synchronized 实现同步的基础：Java 中的每一个对象都可以作为锁。具体表现为以下 3 种形式。

⚫ 对于普通同步方法，锁是当前实例对象。

⚫ 对于静态同步方法，锁是当前类的 Class 对象。

⚫ 对于同步方法块，锁是 Synchonized 括号里配置的对象。



Monitor 对象

代码块  monitorenter monitorexit 指令



java对象 Mark Word 锁状态

锁可以升级不可降级



偏向锁



轻量级锁



重量级锁



### 2.3 原子操作的实现原理



CAS

CPU pipeline

Memory order violation: 一般是假共享引起的



处理器保证单核从内存读取写入1个字节是原子的

单处理器对缓存行 16/32/64 位操作是原子的

处理器提供锁总线和锁缓存两种机制保证复杂内存操作的原子性



## 第3章 Java内存模型

在并发编程中，需要处理两个关键问题：**线程之间如何通信及线程之间如何同步**

在命令式编程中，线程之间的通信机制有两种：共享内存和消息传递。

Java 的并发采用的是共享内存模型，Java 线程之间的通信总是隐式进行，整个通信过程对程序员完全透明。

















## 第4章 Java并发编程基础

interrupt? 



正因为suspend()、resume()和stop()方法带来的副作用，这些方法才被标 注为不建议使用的过期方法























