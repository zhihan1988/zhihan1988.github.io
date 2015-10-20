---
layout: post
title: ConcurrentHashMap Collections.synchronizedMap,Hashtable
---

##Map

* Hashtable是最早出现的（JDK1.0）的集合类，由于其所有方法都是同步的。此时，无竞争的同步会导致可观的性能代价。已废弃。

* HashMap（JDK1.2）是Hashtable的继承者，它通过提供一个不同步的基类和一个同步的包装器Collections.synchronizedMap，解决了线程安全性问题。

通过将基本的功能从线程安全性中分离开来，Collections.synchronizedMap允许需要同步的用户可以拥有同步，而不需要同步的用户则不必为同步付出代价。

Hashtable和synchronizedMap所采取的获得同步的简单方法（同步Hashtable中或者同步的Map包装器对象中的每个方法）有两个主要的不足。
首先，这种方法对于可伸缩性是一种障碍，因为一次只能有一个线程可以访问hash表。同时，这样仍不足以提供真正的线程安全性，许多公用的混合操作仍然需要额外的同步。
例如迭代或者put-if-absent（空则放入），需要外部的同步，以避免数据争用。（在 containsKey()方法返回到put()方法被调用这段时间内，
可能会有另一个线程也插入一个带有相同键的值。如果您想确保只有一次插入，您需要用一个对Map进行同步的同步块将这一对语句包装起来。）

* ConcurrentHashMap是JDK5.0中出现的，它提供比Hashtable或者synchronizedMap更高程度的并发性。
为不同的hashbucket（桶）使用多个写锁和使用JMM的不确定性来最小化锁被保持的时间——或者根本避免获取锁。
ConcurrentHashMap摒弃了单一的map范围的锁，取而代之的是由32个锁组成的集合，其中每个锁负责保护hashbucket的一个子集。
锁主要由变化性操作（put()和remove()）使用。具有32 个独立的锁意味着最多可以有32个线程可以同时修改map。

# 参考：

http://blog.csdn.net/yangfanend/article/details/7165742

##其它相关

由于难以保证并发的list拥有高吞吐量，所以util.concurrent包中没有提供其默认的实现

常用队列：并发队列ConcurrentLinkedQueue和阻塞队列LinkedBlockingQueue
