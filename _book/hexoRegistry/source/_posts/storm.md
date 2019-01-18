---
title: storm
date: 2018-06-12 19:35:06
categories: BigData
tags: storm
---

# Storm

## 1、基本概念
在storm的集群中有两种节点：
* Nimbus:主节点（Mater Node）
  Nimbus负责在集群中分发代码，分配工作给机器，并且监控状态。
* Supervisor:工作节点(Worker Node)
  每个工作节点上运行一个supervisor进程，supervisor会监听nimbus分配给那台机器的工作，根据需要启动或者关闭具体的worker进程。

每个worker进程执行一个具体的Topology，worker进程中的执行线程称为Executor,可以有一个或者多个。每个executor中又包含一个或者多个Task。Task是storm中最小的处理单元。

| 组件       | 概念                                                         |      |
| ---------- | ------------------------------------------------------------ | ---- |
| Nimbus     | 负责资源分配和任务调度                                       |      |
| Supervisor | 负责接收Nimbus分配的任务，启动和停止属于自己管理的Worker进程 |      |
| Worker     | 执行具体处理组件逻辑的进程,即执行Topology                    |      |
| Topology   | 一个实时计算应用程序逻辑被封装到Topology对象中，Topology拓扑会一直运行知道显示地杀死它 |      |
| Executor   | Storm0.8版本以后，Executor为Worker进程中的具体的物理线程，同一个Spout/Bolt的Task可能会共享一个物理线程，一个Executor中只能运行隶属于同一个Spout/Bolt的Task |      |
| Spout      | 在Topology中产生源数据流的组件。通常Spout获取数据源的数据（如Kafka、MQ等读取数据），然后调用nextTuple()函数，发射数据供Bolt消费。 |      |
| Bolt       | 在Topology中接收spout发射的数据后执行处理的组件。Bolt可以执行过滤、函数操作、合并、写数据库等任何操作。Bolt在接收到消息后会调用execute()函数，用户可以在其中执行自己想要的操作 |      |
| Tuple      | 消息传递的基本单元，即元组。                                 |      |
| Task       | 每一个Spout/Bolt具体要做的工作，也是各个节点之间进行分组的单位 |      |
| Stream     | 源源不断传递的Tuple组成的Stream                              |      |
| Stream分组 | 即消息的分区(partition)方法。storm提供若干种实用的分组方式，包括Shuffle、Fields、All、Global、None、Direct和Local or Shuffle等 |      |

假设我们现在有一个Storm集群，一台nimbus和4台supervisor，默认情况下，一个supervisor可以启动4个worker。假设客户端提交了一个Topology需要4个worker来执行，
![storm1](http://oy48q6kwm.bkt.clouddn.com/455bcbd79be710f1c6d0f571dc0895c8.png)
从上图可以看出并不是一个supervisor分配一个worker.这是因为nimbus是针对topology的任务分配，是针对worker来的。我们指定了topology需要4个woreker，nimbus会从已有的16个worker中选择四个worker，并不会平均分配。**这里需要注意的是一个worker同时只能运行一个topology**。如果此时再有另外一个topology提交，不管指定使用几个worker来执行，都会从剩下的12个worker中选择。

Nimbus和Supervisor之间的通信是依赖zookeeper完成的，并且nimbus和supervisor都是快速失败(fail-fast)和无状态的，所有的状态要么在zookeeper里面，要么在本地磁盘上。这也就意味着我们可以使用kill -9来杀死numbus和supervisor进程，然后再重启继续工作。
![storm2](http://oy48q6kwm.bkt.clouddn.com/f084adefc384f6d9b0941dba2f16855f.png)

> 小贴士：Storm中有一些术语(不是全部)，是按照气象术语来命名的。例如Storm是暴风雨，spout是龙卷风的意思，bolt是雷电的意思，nimbus是雨云的意思。

## 2、Storm组件
### Topology（拓扑）
一个topology中必须同时存在spout和bolt，而spout和bolt的数量可以是任意个。要提醒的是：Topology的组件目前只有Spout和Bolt，没有其他组件。所以以后提到一个Topology的组件的时候，其实也就是指的是Spout或者Bolt。
### Stream（流）
我们已经知道Spout是从外部数据源中获取数据，以一定的格式将数据传递给Bolt处理。从Spout中源源不断的给Bolt传递数据，形成的这个数据通道我们称之为Stream。
### Tuple
tuple是stream中的最小组成单元，也叫元组。

最简单的一个topology模型。图中虚线的每一个小节点"-"就可以看作是一个tuple。
![storm3](http://oy48q6kwm.bkt.clouddn.com/7142214dfcdee38b524d9d87a1639f0c.png)
spout可以将数据传递给多个bolt，bolt还能将数据传递给下一级bolt。这样的原因是，有的时候，我们对于数据的分析必须是一步一步的，后一步的分析必须建立在之前分析的基础上。
![storm5](http://oy48q6kwm.bkt.clouddn.com/c6089a48f023c71a6133a55d9eb4f0a2.png)
Stream都是由Tuple组成的，而Tuple是有数据格式的，**在同一个流中,Tuple的数据格式应该都是一样的；不同流中的数据格式可能相同，也可能不同.**

一个spout可以发射给多个bolt数据，同样一个bolt也可以接收多个spout发射的数据。
![复杂的topology](http://oy48q6kwm.bkt.clouddn.com/1158d324029134c0e9cc15d3865b9e57.png)
在storm中，spout和bolt、bolt与bolt之间的数据流向，将整合topology串起来了行程了一个DAG(有向无环图)。**DAG的意思就是数据流是有方向的，但不能形成一个环状。如果形成了一个环状，那么意味着Bolt中的数据还可能传给Spout，spout又要传递给Bolt。这就形成了一个死循环，Stream中的一个数据(Tuple)永远也没办法处理完。下图中的两条红线都是不允许的。
![storm有向无环图](http://oy48q6kwm.bkt.clouddn.com/afbe75105d45b4468dffa0ae8af34d5d.png)


## 3、安装
### 下载安装包上传至服务器http://storm.apache.org/downloads.html
### 分配好资源
ui:172.16.10.22
nimbus:172.16.10.22
supervisor1:172.16.10.23
supervisor2:172.16.10.24
```shell
cd /tools
tar -xzvf apache-storm-1.1.0.tar.gz
cd /tools/apache-storm-1.1.0/conf
vim storm.yml
```
>\# Licensed to the Apache Software Foundation (ASF) under one
>\# or more contributor license agreements.  See the NOTICE file
>\# distributed with this work for additional information
>\# regarding copyright ownership.  The ASF licenses this file
>\# to you under the Apache License, Version 2.0 (the
>\# "License"); you may not use this file except in compliance
>\# with the License.  You may obtain a copy of the License at
>\#
>\# http://www.apache.org/licenses/LICENSE-2.0
>\#
>\# Unless required by applicable law or agreed to in writing, software
>\# distributed under the License is distributed on an "AS IS" BASIS,
>\# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
>\# See the License for the specific language governing permissions and
>\# limitations under the License.
>
>\#\#\#\#\#\#\#\#\#\#\# These MUST be filled in for a storm configuration
>storm.zookeeper.servers:
>&nbsp;&nbsp;&nbsp;&nbsp;\- "172.16.1.43"
>&nbsp;&nbsp;&nbsp;&nbsp;\- "172.16.1.62"
>&nbsp;&nbsp;&nbsp;&nbsp;\- "172.16.1.64"
>
>\#     - "server2"
>nimbus.seeds: ["172.16.10.22"]
>supervisor.slots.ports:
>&nbsp;&nbsp;&nbsp;&nbsp;\- 6700
>&nbsp;&nbsp;&nbsp;&nbsp;\- 6701
>&nbsp;&nbsp;&nbsp;&nbsp;\- 6702
>&nbsp;&nbsp;&nbsp;&nbsp;\- 6703
>
>\#
>\# \#\#\#\#\# These may optionally be filled in:
>\#
>\#\# List of custom serializations
>\# topology.kryo.register:
>\#     - org.mycompany.MyType
>\#     - org.mycompany.MyType2: org.mycompany.MyType2Serializer
>\#
>\#\# List of custom kryo decorators
>\# topology.kryo.decorators:
>\#     - org.mycompany.MyDecorator
>\#
>\#\# Locations of the drpc servers
>\# drpc.servers:
>\#     - "server1"
>\#     - "server2"
>
>\#\# Metrics Consumers
>\#\# max.retain.metric.tuples
>\#\# - task queue will be unbounded when max.retain.metric.tuples is equal or less than 0.
>\#\# whitelist / blacklist
>\#\# - when none of configuration for metric filter are specified, it'll be treated as 'pass all'.
>\#\# - you need to specify either whitelist or blacklist, or none of them. You can't specify both of them.
>\#\# - you can specify multiple whitelist / blacklist with regular expression
>\#\# expandMapType: expand metric with map type as value to multiple metrics
>\#\# - set to true when you would like to apply filter to expanded metrics
>\#\# - default value is false which is backward compatible value
>\#\# metricNameSeparator: separator between origin metric name and key of entry from map
>\#\# - only effective when expandMapType is set to true
>\# topology.metrics.consumer.register:
>\#   - class: "org.apache.storm.metric.LoggingMetricsConsumer"
>\#     max.retain.metric.tuples: 100
>\#     parallelism.hint: 1
>\#   - class: "org.mycompany.MyMetricsConsumer"
>\#     max.retain.metric.tuples: 100
>\#     whitelist:
>\#       - "execute.*"
>\#       - "^__complete-latency$"
>\#     parallelism.hint: 1
>\#     argument:
>\#       - endpoint: "metrics-collector.mycompany.org"
>\#     expandMapType: true
>\#     metricNameSeparator: "."
>
>\#\# Cluster Metrics Consumers
>\# storm.cluster.metrics.consumer.register:
>\#   - class: "org.apache.storm.metric.LoggingClusterMetricsConsumer"
>\#   - class: "org.mycompany.MyMetricsConsumer"
>\#     argument:
>\#       - endpoint: "metrics-collector.mycompany.org"
>\#
>\# storm.cluster.metrics.consumer.publish.interval.secs: 60
>
>storm.local.dir: "/data/storm/data"
>ui.port: 9001

172.16.10.22、172.16.10.23、172.16.10.24每个节点的配置保持一直，另外需在给两个supervisor节点加上JMX监控。需要在storm.yaml文件中加入
>supervisor.childopts: -verbose:gc -XX:+PrintGCTimeStamps -XX:+PrintGCDetails -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.port=9998


### 启动服务
172.16.10.22
* nohup /tools/apache-storm-1.1.0/bin/storm ui >/dev/null 2>&1 &
* nohup /tools/apache-storm-1.1.0/bin/storm nimbus >/dev/null 2>&1 &
* nohup /tools/apache-storm-1.1.0/bin/storm logviewer >/dev/null 2>&1 &


![nimbus](http://oy48q6kwm.bkt.clouddn.com/e1e783cdcd9be99de0af4488d1e17878.png) 

core是UI进程、nimbus、logviewer进程已经都起来了。

172.16.10.23
* nohup /tools/apache-storm-1.1.0/bin/storm supervisor >/dev/null 2>&1 &
* nohup /tools/apache-storm-1.1.0/bin/storm logviewer >/dev/null 2>&1 &

![supervisor](http://oy48q6kwm.bkt.clouddn.com/23cba149f511602b134dfc95fa5afac7.png)
supervisor进程已经启动。

172.16.10.24
* nohup /tools/apache-storm-1.1.0/bin/storm supervisor >/dev/null 2>&1 &
* nohup /tools/apache-storm-1.1.0/bin/storm logviewer >/dev/null 2>&1 &

![supervisor2](http://oy48q6kwm.bkt.clouddn.com/23cba149f511602b134dfc95fa5afac7.png)
supervisor进程已经启动。

## 4、开发
### 本地模式
在maven工程的pom.xml中引入storm依赖包。
```xml
<dependencies>
    <!-- https://mvnrepository.com/artifact/org.apache.storm/storm-core -->
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>1.2.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```
创建topology
```java
package com.nucc.channel.govern.demo.storm.topology;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.OutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichBolt;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;

/**
 * @description: 拓扑
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/5 22:48
 * @version: 1.0.0
 */
public class StormTopology {
    /**
     * 获取数据源
     */
    public static class Spout extends BaseRichSpout {

        private Map conf;
        private TopologyContext topologyContext;
        private SpoutOutputCollector spoutOutputCollector;

        /**
         * 初始化方法，用于创建数据源。
         *
         * @param map                  配置属性
         * @param topologyContext      拓扑上下文
         * @param spoutOutputCollector 发射器
         */
        @Override
        public void open(Map map, TopologyContext topologyContext, SpoutOutputCollector spoutOutputCollector) {
            this.conf = map;
            this.spoutOutputCollector = spoutOutputCollector;
            this.topologyContext = topologyContext;
        }

        int num = 0;
        /**
         * 死循环方法，不断被调用处理元组。
         */
        @Override
        public void nextTuple() {
            this.spoutOutputCollector.emit(new Values(num++));
            //每隔一秒睡眠一次方便控制台观察输出
            Utils.sleep(1000);
        }

        /**
         * 声明发射字段
         * @param outputFieldsDeclarer
         */
        @Override
        public void declareOutputFields(OutputFieldsDeclarer outputFieldsDeclarer) {

            //fields中的参数与emit()中的Values()一一对应
            outputFieldsDeclarer.declare(new Fields("num"));
        }
    }


    public static class Bolt extends BaseRichBolt{

        private Map config;
        private TopologyContext topologyContext;
        private OutputCollector outputCollector;
        @Override
        public void prepare(Map map, TopologyContext topologyContext, OutputCollector outputCollector) {
            this.config = map;
            this.outputCollector = outputCollector;
            this.topologyContext = topologyContext;
        }

        int sum = 0;
        /**
         * 只要spout中有数据产生，execute就会被不断调用。
         * @param tuple
         */
        @Override
        public void execute(Tuple tuple) {
            Integer num = tuple.getIntegerByField("num");
            sum += num;
            System.out.println(sum);
        }

        /**
         * 如果不需要向外发射tuple，该方法就不需要实现。
         * @param outputFieldsDeclarer
         */
        @Override
        public void declareOutputFields(OutputFieldsDeclarer outputFieldsDeclarer) {

        }
    }
}

```

创建执行方法
```java
package com.nucc.channel.govern.demo.storm.topology;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.topology.TopologyBuilder;

/**
 * @description: 执行storm
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/5 23:18
 * @version: 1.0.0
 */
public class Run {
    public static void main(String[] args) {
        //创建一个topology
        TopologyBuilder topologyBuilder = new TopologyBuilder();
        topologyBuilder.setSpout("spoutName", new StormTopology.Spout());
        topologyBuilder.setBolt("boltName", new StormTopology.Bolt()).shuffleGrouping("spoutName");

        //创建一个本地集群
        LocalCluster localCluster = new LocalCluster();
        String topologyName = new StormTopology().getClass().getSimpleName();
        Config config = new Config();
        localCluster.submitTopology(topologyName, config, topologyBuilder.createTopology());
    }
}

```
直接运行回报IRichSpout类找不到异常。
```java
java.lang.NoClassDefFoundError: org/apache/storm/topology/IRichSpout
	at java.lang.Class.getDeclaredMethods0(Native Method)
	at java.lang.Class.privateGetDeclaredMethods(Class.java:2701)
	at java.lang.Class.privateGetMethodRecursive(Class.java:3048)
	at java.lang.Class.getMethod0(Class.java:3018)
	at java.lang.Class.getMethod(Class.java:1784)
	at sun.launcher.LauncherHelper.validateMainClass(LauncherHelper.java:544)
	at sun.launcher.LauncherHelper.checkAndLoadMain(LauncherHelper.java:526)
Caused by: java.lang.ClassNotFoundException: org.apache.storm.topology.IRichSpout
	at java.net.URLClassLoader.findClass(URLClassLoader.java:381)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:335)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	... 7 more
Error: A JNI error has occurred, please check your installation and try again
Exception in thread "main"
```
需要把pom.xml中的scope注释掉

```xml
 <!--<scope>provided</scope>-->
```

运行结果为:
![storm输出结果](http://oy48q6kwm.bkt.clouddn.com/175f384b5f5abc26b816b032a715e025.png)

### 集群模式运行

## 5、配置属性

```java
        TopologyBuilder topologyBuilder = new TopologyBuilder();
        org.apache.storm.generated.StormTopology topology = topologyBuilder.createTopology();

        Config config = new Config();
        config.setNumWorkers(10);
        config.setMaxSpoutPending(5000);
        StormSubmitter.submitTopology("TopologyName",config,topology);
```

## 6、整合kafka

###6.1、Spouts

提供核心的 Storm 和Trident 的spout实现，用来从Apache Kafka 版本消费数据. 支持 [Trident](https://blog.csdn.net/liuxinghao/article/details/68944280) 和 core Storm 的spout.对于这两种spout实现，我们使用BorkerHosts接口来跟踪Kafka broker host partition 映射关系，用KafkaConfig来控制Kafka 相关参数. 

### 6.2、BrokerHosts

为了初始化kafka spout/emitter，第一你需要构造一个 BrokerHosts 标记接口的实例。当前，我们支持以下两种实现方式. 

* ZkHosts:

  如果你想要动态的跟踪kafka broker partition映射关系，你应该使用ZkHosts。这个类使用Kafka Zookeeper实体跟踪brokerHost -> 分区映射。你可以调用下面的方法得到一个实例`java public ZkHosts(String brokerZkStr, String brokerZkPath) public ZkHosts(String brokerZkStr) `ZkStr字符串个事是ip:port（例如：localhost:2181），brokerZkPath是存储所有topic和partition信息的zk根路径，默认情况下kafka使用/brokers路径。

  默认情况下，broker-partition 映射关系60s秒从Zookeeper刷新一次.如果你想要改变这个时间，你需要设置 host.refreshFreqSecs 配置. 

* StaticHosts:

  这是一种可替代的实现，broker->partition 信息是静态的.要构造这个类的实例，你需要先构造一个 GlobalPartitionInformation 的实例. 

  ```java
  Broker brokerForPartition0 = new Broker("localhost");//localhost:9092
  Broker brokerForPartition1 = new Broker("localhost", 9092);//localhost:9092 but we specified the port explicitly
  Broker brokerForPartition2 = new Broker("localhost:9092");//localhost:9092 specified as one string.
  GlobalPartitionInformation partitionInfo = new GlobalPartitionInformation();
  partitionInfo.addPartition(0, brokerForPartition0);//mapping from partition 0 to brokerForPartition0
  partitionInfo.addPartition(1, brokerForPartition1);//mapping from partition 1 to brokerForPartition1
  partitionInfo.addPartition(2, brokerForPartition2);//mapping from partition 2 to brokerForPartition2
  StaticHosts hosts = new StaticHosts(partitionInfo);
  ```


### 6.3、KafkaConfig

  构造一个KafkaSpout的实例，第二件事情就是要实例化KafkaConfig。 `public KafkaConfig(BrokerHosts hosts, String topic) ` `public KafkaConfig(BrokerHosts hosts, String topic, String clientId) ` ,hosts可以通过多个BrokerHosts接口实现.topic 就是Kafka topic 的名称.可选择的ClientId就是当前消费的offset存储的zk的路径. 

  Spoutconfig是KafkaConfig的扩展，它支持Zookeeper 连接信息的其他字段，并且可以控制KafkaSpout的行为.Zkroot就是用来存储消费者offset信息的根路径.id是唯一的用来标识spout.  ` public SpoutConfig(BrokerHosts hosts, String topic, String zkRoot, String id); ` `public SpoutConfig(BrokerHosts hosts, String topic, String id); ` 除此之外，SpoutConfig包含下面这些字段，用来控制KafkaSpout的行为 

  ```java
  //设置将当前Kafka偏移量保存到ZooKeeper的频率 
  public long stateUpdateIntervalMs = 2000;
  
  //重试失败消息的策略,使用ExponentialBackoffMsgRetryManager重试管理器。
  public String failedMsgRetryManagerClass = ExponentialBackoffMsgRetryManager.class.getName();
  //Exponential(指数函数)回退重试策略，在bolt调用OutputCollector.fail()之后，会调用ExponentialBackoffMsgRetryManager()尝试重新获取消息，前提是只有在使用了ExponentialBackoffMsgRetryManager 管理器的时候才会生效。
  //连续重试之间的初试延迟
  public long retryInitialDelayMs = 0;
  public double retryDelayMultiplier = 1.0;
  //连续重试之间的最大延迟
  public long retryDelayMaxMs = 60 * 1000;
  //如果retryLimit小于零，则将无限重试失败的消息。
  public int retryLimit = -1;   
  ```

  TridentKafkaConfig是KafkaConfig的另外一个扩展. TridentKafkaEmitter只接受TridentKafkaConfig作为参数.

  KafkaConfig类也有一些公共变量来控制你的应用程序的行为。以下是默认值：

  ```java
  //kafka consumer 每次请求获取数据量的大小，默认1024 * 1024 = 1048576 = 1M
  public int fetchSizeBytes = 1024 * 1024;
  //Consumer连接kafka server超时时间
  public int socketTimeoutMs = 10000;
  //当服务器没有新消息时，消费者等待时间
  public int fetchMaxWait = 10000;
  //Consumer端缓存大小
  public int bufferSizeBytes = 1024 * 1024;
  //从Kafka中取出的byte[]，该如何反序列化
  public MultiScheme scheme = new RawMultiScheme();
  //和startOffsetTime，一起用，默认情况下，为false，一旦startOffsetTime被设置，就要置为true。如果将forceFromStart(旧版本是ignoreZkOffsets）设置为true，则每次拓扑重新启动时，都会从开头读取消息。如果为false，则：第一次启动，从开头读取，之后的重启均是从offset中读取。
  public boolean forceFromStart = false;
  // -2 从kafka头开始  -1 是从最新的开始 0 =无 从ZK开始
  public long startOffsetTime = kafka.api.OffsetRequest.EarliestTime();
  // 每次kafka会读取一批offset存放在list中，当zk offset比当前本地保存的commitOffse相减大于这个值时，重新设置commitOffset为当前zk offset，代码见PartitionManager
  public long maxOffsetBehind = Long.MAX_VALUE;
  //如果所请求的offset对应的消息在Kafka中不存在，是否使用startOffsetTime
  public boolean useStartOffsetTimeIfOffsetOutOfRange = true;
  //多长时间统计一次metrics(度量)
  public int metricsTimeBucketSizeInSecs = 60;
  
  ```

  **MultiScheme：**是一个用来规定 ByteBuffer 如何在Kafka 消费，并转换成一个 storm tuple.并且会控制 output field的命名 。默认的 `RawMultiScheme` 接受 `ByteBuffer` 参数，并返回一个 tuple.就是将ByteBuffer 转换成 `byte[]`.outPutField 的名称是 “bytes”。还有可替换的的实现，像 `SchemeAsMultiScheme` 和 `KeyValueSchemeAsMultiScheme`，他们会将 `ByteBuffer` 转换成 `String`.

  当然还有个`SchemeAsMultiScheme` 的扩展类，`MessageMetadataSchemeAsMultiScheme`，MessageMetadataSchemeAsMultiScheme有一个额外的反序列化方法，会接受ByteBuffer 信息，还会伴随着`Partition` 和 `offset` 信息.


###6.4、Failed message retry

  FailedMsgRetryManager是一个定义失败消息的重试策略的接口。默认实现是ExponentialBackoffMsgRetryManager，它在连续重试之间以指数延迟重试。要使用自定义实现，请将SpoutConfig.failedMsgRetryManagerClass设置为完整的实现类名称。 下面是接口： 

  ```java
  // Spout initialization can go here. This can be called multiple times during lifecycle of a worker. 
  void prepare(SpoutConfig spoutConfig, Map stormConf);
  
  // Message corresponding to offset has failed. This method is called only if retryFurther returns true for offset.
  void failed(Long offset);
  
  // Message corresponding to offset has been acked.  
  void acked(Long offset);
  
  // Message corresponding to the offset, has been re-emitted and under transit.
  void retryStarted(Long offset);
  
  /**
   * The offset of message, which is to be re-emitted. Spout will fetch messages starting from this offset
   * and resend them, except completed messages.
   */
  Long nextFailedMessageToRetry();
  
  /**
   * @return True if the message corresponding to the offset should be emitted NOW. False otherwise.
   */
  boolean shouldReEmitMsg(Long offset);
  
  /**
   * Spout will clean up the state for this offset if false is returned. If retryFurther is set to true,
   * spout will called failed(offset) in next call and acked(offset) otherwise 
   */
  boolean retryFurther(Long offset);
  
  /**
   * Clear any offsets before kafkaOffset. These offsets are no longer available in kafka.
   */
  Set<Long> clearOffsetsBefore(Long kafkaOffset);
  ```

  >#### Version incompatibility在1.0之前的Storm版本中，MultiScheme方法接受一个 `byte []` 而不是 `ByteBuffer`。 MultScheme和相关的方案apis在版本1.0中被更改为接受ByteBuffer而不是byte []。这意味着，在1.0版及更高版本之前，1.0版的kafka spouts将无法使用。在Storm 1.0及更高版本中运行拓扑时，必须确保storm-kafka版本至少为1.0。1.0之前的 topology jar 必须重新和storm-kafka 1.0版本构建，以便在Storm 1.0及更高版本的群集中运行。

  ```java
  javaBrokerHosts hosts = new ZkHosts(zkConnString);
  SpoutConfig spoutConfig = new SpoutConfig(hosts, topicName, "/" + topicName, UUID.randomUUID().toString());
  spoutConfig.scheme = new SchemeAsMultiScheme(new StringScheme());
  KafkaSpout kafkaSpout = new KafkaSpout(spoutConfig);
  ```

  #### Trident Spout

  ```java
  TridentTopology topology = new TridentTopology();
  BrokerHosts zk = new ZkHosts("localhost");
  TridentKafkaConfig spoutConf = new TridentKafkaConfig(zk, "test-topic");
  spoutConf.scheme = new SchemeAsMultiScheme(new StringScheme());
  OpaqueTridentKafkaSpout spout = new OpaqueTridentKafkaSpout(spoutConf);
  ```

  

### 6.5、偏移量处理

	KafkaSpout如何存储Kafka主题的偏移量并在发生故障时恢复，如上面的KafkaConfig属性所示，您可以通过设置 `KafkaConfig.startOffsetTime` 来控制从Kafka topic 的哪个端口开始读取，如下所示： 

* kafka.api.OffsetRequest.EarliestTime()：从topic 初始位置读取消息 (例如，从最老的那个消息开始) 
* kafka.api.OffsetRequest.LatestTime()：从topic尾部开始读取消息 (例如，新写入topic的信息) 
* 一个Unix时间戳，从当前 epoch 开始.（例如，可以通过System.currentTimeMillis(）），具体的可以查看Kafka FAQ中的 [How do I accurately get offsets of messages for a certain timestamp using OffsetRequest?](https://cwiki.apache.org/confluence/display/KAFKA/FAQ#FAQ-HowdoIaccuratelygetoffsetsofmessagesforacertaintimestampusingOffsetRequest?) .

     当topology（拓扑）运行Kafka Spout ，并跟踪读取和发送的offset，并将状态信息存储到zk path `SpoutConfig.zkRoot+ "/" + SpoutConfig.id`.在故障的情况下，它会从ZooKeeper的最后一次写入偏移中恢复。 

> **Important:** 新部署topology（拓扑）时，请确保`SpoutConfig.zkRoot`和`SpoutConfig.id`的设置未被修改， 否则spout将无法从ZooKeeper中读取以前的消费者状态信息（即偏移量）导致意外的行为和/或数据丢失，具体取决于您的用例。 

这意味着当topology（拓扑）运行一旦设置`KafkaConfig.startOffsetTime`将不会对 topology（拓扑）的后续运行产生影响， 因为现在 topology（拓扑）将依赖于ZooKeeper中的消费者状态信息（偏移量）来确定从哪里开始（更多准确地：简历）阅读。 如果要强制该端口忽略存储在ZooKeeper中的任何消费者状态信息，则应将参数`KafkaConfig.forceFromStart`设置为true。如果为`true`， 则如上所述，spout 将始终从`KafkaConfig.startOffsetTime`定义的偏移量开始读取。 

##7、Bolts

*bolts*是一个Storm集群中的关键组件 ，它把元组作为输入，然后产生新的元组作为输出。实现一个*bolt*时，通常需要实现**IRichBolt**接口。*Bolts*对象由客户端机器创建，序列化为拓扑，并提交给集群中的主机。然后集群启动工人进程反序列化*bolt*，调用**prepare**，最后开始处理元组。 要创建一个bolt对象，它通过构造器参数初始化成员属性，*bolt*被提交到集群时，这些属性值会随着一起序列化。 

```java
package com.nucc.channel.govern.storm;

import lombok.extern.slf4j.Slf4j;
import org.apache.storm.task.OutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;

import java.util.Arrays;
import java.util.Map;
@Slf4j
public class MyBolt extends BaseRichBolt {

    private Map config;
    private TopologyContext topologyContext;
    private OutputCollector outputCollector;

    /**
     * 初始化环境
     * @param stormConf
     * @param context
     * @param collector
     */
    @Override
    public void prepare(Map stormConf, TopologyContext context, OutputCollector collector) {
        this.config = stormConf;
        this.outputCollector = collector;
        this.topologyContext = context;
    }

    /**
     * 只要spout中有数据产生，execute就会被不断调用。
     * @param input
     */
    @Override
    public void execute(Tuple input) {
        String logLine = input.getString(0);
        try {
            outputCollector.emit(Arrays.asList("label", parser.parse(logLine)));
        } catch (Exception ex) {
            log.error("Failing parse and ignore audit log {} ", logLine, ex);
        } finally {
            outputCollector.ack(input);
        }
    }

    /**
     *  为bolt声明输出模式
     * 如果不需要向外发射tuple，该方法就不需要实现。
     * @param declarer
     */
    @Override
    public void declareOutputFields(OutputFieldsDeclarer declarer) {
        declarer.declare(new Fields("label", "message"));
    }
}

```

拓扑是一个树型结构，消息（元组）穿过其中一条或多条分支。树上的每个节点都会调用**ack(tuple)**或**fail(tuple)**，Storm因此知道一条消息是否失败了，并通知那个/那些制造了这些消息的*spout(s)*。既然一个Storm拓扑运行在高度并行化的环境里，跟踪始发*spout*实例的最好方法就是在消息元组内包含一个始发spout引用。这一技巧称做**锚定**。

锚定发生在调用**collector.emit()**时。正如前面提到的，Storm可以沿着元组追踪到始发*spout*。**collector.ack(tuple)**和**collector.fail(tuple)**会告知spout每条消息都发生了什么。当树上的每条消息都已被处理了，Storm就认为来自*spout*的元组被全面的处理了。如果一个元组没有在设置的超时时间内完成对消息树的处理，就认为这个元组处理失败。默认超时时间为30秒。 

### 7.1、多数据流

一个*bolt*可以使用**emit(streamId, tuple)**把元组分发到多个流，其中参数**streamId**是一个用来标识流的字符串。然后，你可以在**TopologyBuilder**决定由哪个流订阅它。 

### 7.2、多锚定

为了用*bolt*连接或聚合数据流，你需要借助内存缓冲元组。为了在这一场景下确保消息完成，你不得不把流锚定到多个元组上。可以向**emit**方法传入一个元组列表来达成目的。 

```java
...
List anchors = new ArrayList();
anchors.add(tuple1);
anchors.add(tuple2);
collector.emit(anchors, values);
...
```

通过这种方式，bolt在任意时刻调用**ack**或**fail**方法，都会通知消息树，而且由于流锚定了多个元组，所有相关的*spout*都会收到通知。 

### 7.3、使用IBasicBolt自动确认

你可能已经注意到了，在许多情况下都需要消息确认。简单起见，Storm提供了另一个用来实现*bolt*的接口，**IBasicBolt**。对于该接口的实现类的对象，会在执行**execute**方法之后自动调用**ack**方法。 

```java
class SplitSentence extends BaseBasicBolt {
    public void execute(Tuple tuple, BasicOutputCollector collector) {
        String sentence = tuple.getString(0);
        for(String word : sentence.split(" ")) {
            collector.emit(new Values(word));
        }
}

    public void declareOutputFields(OutputFieldsDeclarer declarer) {
        declarer.declare(new Fields("word"));
    }
}
```

**NOTE:**分发消息的BasicOutputCollector自动锚定到作为参数传入的元组。 

## 8、Tuple传递模式

所谓的grouping策略就是在Spout与Bolt、Bolt与Bolt之间传递Tuple的方式。总共有七种方式： 

* shuffleGrouping ：随机分组。Task中的数据随机分批，可以保证同一级Bolt上的每个Task处理的Tuple数量一致。他能实现较好的负载均衡恒。

   ![1534484566974](C:\Users\zhangchi\Pictures\Saved Pictures\1534484566974.png)

* fieldsGrouping ：按照字段分组，在这里即是同一个单词只能发送给一个Bolt 。根据Tuple中的某一个Filed或者多个Filed的值来划分。比如Stream根据user-id的值来分组，具有相同user-id值的Tuple会被分到相同的Task中(具有不同user-id值的Tuple可能会被分发到其他Task中。比如user-id为1的Tuple都会分发给Task1，user-id为2的Tuple可能在Task1上也可能在Task2上，但是同时只能在一个Task上)。

   ![1534486378370](C:\Users\zhangchi\AppData\Local\Temp\1534486378370.png)

* allGrouping ：广播发送，所有的Tuple会分发到所有的Task上。

   ![1534486615053](C:\Users\zhangchi\Pictures\Saved Pictures\1534486615053.png) 

* globalGrouping ：全局分组，整个Stream会选择一个Task作为分发的目的地，通常会将Tuple分配到task id值最低的task里面 

   ![1534486864083](C:\Users\zhangchi\AppData\Local\Temp\1534486864083.png)

* noneGrouping：随机分派，Stream不关心将Tuple分发到哪个Task上，目前等同于Shuffle分组。

* directGrouping：直接分组，指定Tuple与Bolt的对应发送关系 。也就是产生数据的spout/bolt自己明确决定这个Tupl被BOlt的哪些Task所消费。如果使用Direct分组，需要使用OutputCollector的emitDirect()方法来实现。

* Local or shuffle Grouping：如果目标Bolt中的一个或者多个Task和当前生产数据的Task再同一个worker进程中，那么就走内部的线程间通信，将Tuple直接发给在当前Worker进程中的目的Task。否则，同Shuffle分组。

* customGrouping：自定义group