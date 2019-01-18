---
title: kafka
date: 2018-07-06 11:40:08
categories:
tags:
---

## kafka专业术语

* Producer：负责发布消息到Kafka broker 
* Consumer：消费消息。每个consumer属于一个特定的consumer group（可为每个consumer指定group name，若不指定group name则属于默认的group）。使用consumer high level API时，同一topic的一条消息只能被同一个consumer group内的一个consumer消费，但多个consumer group可同时消费这一消息。 
* Broker：消息中间件处理结点，一个Kafka节点就是一个broker，多个broker可以组成一个Kafka集群。 
* Topic：一类消息主题，Kafka集群能够同时负责多个topic的分发。 
* Partition：topic物理上的分组，一个topic可以分为多个partition，每个partition是一个有序的队列。 
* Segment：partition物理上由多个segment组成。 
* offset：每个partition都由一系列有序的、不可变的消息组成，这些消息被连续的追加到partition中。partition中的每个消息都有一个连续的序列号叫做offset，用于partition唯一标识一条消息 。

在Kafka文件存储中，同一个topic下有多个不同partition，每个partition为一个目录，partiton命名规则为topic名称+有序序号，第一个partiton序号从0开始，序号最大值为partitions数量减1。 

![1534415966036](C:\Users\zhangchi\Pictures\Saved Pictures\1534415966036.png)

一个topic 可以配置多个partition，Producer发送消息到broker时，会根据Paritition机制选择将其存储到哪一个Partition。如果Partition机制设置合理，所有消息可以均匀分布到不同的Partition里，这样就实现了负载均衡。如果一个Topic对应一个文件，那这个文件所在的机器I/O将会成为这个Topic的性能瓶颈，而有了Partition后，不同的消息可以并行写入不同broker的不同Partition里，极大的提高了吞吐率。

consumer接受数据的时候是按照group来接受，`kafka确保每个partition只能同一个group中的同一个consumer消费，如果想要重复消费，那么需要其他的组来消费。`Zookeerper中保存这每个topic下的每个partition在每个group中消费的offset  新版kafka把这个offsert保存到了一个consumer_offsert的topic下这个consumer_offsert 有50个分区，通过将group的id哈希值%50的值来确定要保存到那一个分区.  这样也是为了考虑到zookeeper不擅长大量读写的原因。 

所以，如果要一个group用几个consumer来同时读取的话，需要多线程来读取，一个线程相当于一个consumer实例。当consumer的数量大于分区的数量的时候，有的consumer线程会读取不到数据。  假设一个topic test 被groupA消费了，现在启动另外一个新的groupB来消费test，默认test-groupB的offset不是0，而是没有新建立，除非当test有数据的时候，groupB会收到该数据，该条数据也是第一条数据，groupB的offset也是刚初始化的ofsert, 除非用显式的用–from-beginnging 来获取从0开始数据 。

![img](https://images2015.cnblogs.com/blog/1122015/201705/1122015-20170524175935107-335784290.png) 