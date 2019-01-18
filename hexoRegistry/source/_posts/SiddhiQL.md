---
title: SiddhiQL
date: 2018-03-31 18:04:35
tags: SiddhiQL
categories: BigData
---

&ensp;&ensp;













Siddhi是一个java库，它从数据流中侦听事件，检测通过Streaming SQL语言描述的复杂条件，并触发操作。它执行流处理和复杂事件处理。



##Overview





![](https://raw.githubusercontent.com/wso2/siddhi/master/docs/images/siddhi-overview.png?raw=true)

###Siddhi 支持以下内容

* 数据预处理
* 根据阈值生成警报
* 在短窗口或长时间段内聚合计算
* 支持多数据流操作
* 在发现缺失和错误事件时关联数据,触发相关动作
* 与数据库交互数据流
* 检测时间事件模式
* 跟踪（某些空间或时间）
* 分析趋势（上升，下降，转弯，底部）
* 使用现有和在线机器学习模型进行实时预测
* 还有更多...有关更多信息，请参阅[Patterns of Streaming Realtime Analytics](https://www.kdnuggets.com/2015/08/patterns-streaming-realtime-analytics.html)

### 入门

按照入门指南 [Siddhi Quick Start Guide](https://wso2.github.io/siddhi/documentation/siddhi-quckstart-4.0/)几分钟之内即可使用siddhi

### 为什么要用Siddhi

* 它很快。[UBER](http://wso2.com/library/conference/2017/2/wso2con-usa-2017-scalable-real-time-complex-event-processing-at-uber?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17)每天使用它来处理200亿个事件（每秒300,000个事件）
* 它很小（<2MB），轻量级可嵌入Android和RaspberryPi。
* 它有超过40个[Siddhi扩展](https://wso2.github.io/siddhi/extensions/)
* 它被60多家公司使用，其中包括许多财富500强企业的生产环境。以下是一些例子：
  * WSO2使用Siddhi用于以下目的：
    * To provide stream processing capabilities in their products such as [WSO2 Stream Processor](http://wso2.com/analytics?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17).
    * As the **edge analytics** library of [WSO2 IoT Server](http://wso2.com/iot?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17).
    * As the core of [WSO2 API Manager](http://wso2.com/api-management?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17)'s throttling.
    * As the core of [WSO2 products'](http://wso2.com/platform?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17) analytics.
  * UBER使用Siddhi进行欺诈分析。
  * [Apache Eagle](http://eagle.apache.org/docs/index.html)使用Siddhi作为策略引擎。
* 基于Siddhi的解决方案已于2014年，2015年，2016年，2017年在[ACM DEBS Grand Challenge Stream Processing](https://dl.acm.org/results.cfm?query=(%252Bgrand%20%252Bchallenge%20%252Bwso2)&within=owners.owner=HOSTED&filtered=&dte=&bfr=)竞赛中入围决赛。
* Siddhi一直是许多学术研究项目的基础，有超过[60个引用](https://scholar.google.com/scholar?cites=5113376427716987836&as_sdt=2005&sciodt=0,5&hl=en)。



### 使用IntelliJ IDEA开发Siddhi

安装[IDEA插件](https://wso2.github.io/siddhi-plugin-idea/)以获得以下功能：

* Siddhi查询编辑器，语法高亮，基本自动完成
* Siddhi Runner和Debugger支持测试Siddhi应用程序



### 尝试使用siddhi流处理器

[WSO2 Stream Processor](https://wso2.com/analytics-and-stream-processing/?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17)是Siddhi的服务器版本，也是在Apache Software License v2.0下发布的。在 [The Forrester Wave: Big Data Streaming Analytics, Q1 2016](https://go.forrester.com/blogs/16-04-16-15_true_streaming_analytics_platforms_for_real_time_everything/)([Report](https://www.forrester.com/report/The+Forrester+Wave+Big+Data+Streaming+Analytics+Q1+2016/-/E-RES129023)) 和 [Cool Vendors in Internet of Things Analytics, 2016](https://www.gartner.com/doc/3314217/cool-vendors-internet-things-analytics)中它都是一个强有力的表现者。

如果您使用WSO2流处理器，则可以使用Siddhi功能以及以下附加功能：

* Siddhi查询编辑器工具，具有语法突出显示和高级自动完成支持。
* Siddhi Runner和Debugger工具
* 事件模拟器工具
* 运行Siddhi作为具有高可用性和可伸缩性的服务器。
* 监控对Siddhi的支持
* 实时仪表板
* 业务用户友好的查询生成和部署

使用Siddhi构建了特定于域的解决方案，包括欺诈检测，股票市场监控，位置分析，邻近营销，上下文推荐，广告优化，运营分析和检测图表模式。有关更多信息，请通过http://wso2.com/support/与我们联系。



### Siddhi Versions

Find the released Siddhi libraries [here](http://maven.wso2.org/nexus/content/groups/wso2-public/org/wso2/siddhi/).



- **Active development version of Siddhi** : **v4.0.0** *built on Java 8.*

  [Siddhi Query Guide](https://wso2.github.io/siddhi/documentation/siddhi-4.0/) for Siddhi v4.x.x

  [Architecture](https://wso2.github.io/siddhi/documentation/siddhi-architecture/) of Siddhi v4.x.x

- **Latest Stable Release of Siddhi** : **v3.0.5** *built on Java 7.*

  [Siddhi Query Guide](https://docs.wso2.com/display/DAS310/Siddhi+Query+Language) for Siddhi v3.x.x

### 最新的API文档

Latest API Docs is [4.2.26](https://wso2.github.io/siddhi/api/4.2.26).



### Jenkins构建状态

| Siddhi Branch | Jenkins Build Status                                         |
| ------------- | ------------------------------------------------------------ |
| master        | [![Build Status](https://wso2.org/jenkins/view/wso2-dependencies/job/siddhi/job/siddhi/badge/icon)](https://wso2.org/jenkins/view/wso2-dependencies/job/siddhi/job/siddhi) |



### How to Contribute

- Report issues at [GitHub Issue Tracker](https://github.com/wso2/siddhi/issues).
- Feel free to try out the [Siddhi source code](https://github.com/wso2/siddhi) and send your contributions as pull requests to the [master branch](https://github.com/wso2/siddhi/tree/master).

### Contact us

- Post your questions with the ["Siddhi"](http://stackoverflow.com/search?q=siddhi) tag in [Stackoverflow](http://stackoverflow.com/search?q=siddhi).
- For more details and support contact us via [http://wso2.com/support/](http://wso2.com/support?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17)



### Support

- We are committed to ensuring support for Siddhi (with its [extensions](https://wso2.github.io/siddhi/extensions/)) and [WSO2 Stream Processor](http://wso2.com/analytics?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17)from development to production.
- Our unique approach ensures that all support leverages our open development methodology and is provided by the very same engineers who build the technology.
- For more details and to take advantage of this unique opportunity, contact us via [http://wso2.com/support/](http://wso2.com/support?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17).

Siddhi was joint research project initiated by [WSO2](http://wso2.com/) and [University of Moratuwa](http://www.mrt.ac.lk/web/), Sri Lanka.





## Siddhi特性



* 事件检索
  * 从不同的数据源支持各种消息格式
* 映射事件
  * 处理各种数据格式映射事件流
  * 映射到多个数据流格式出版
* 流处理
  * filter
    * 基于条件过滤流
  * window
    * 支持滑动和批处理(暴跌)和许多其他类型的窗口
  * Aggregation(聚合)
    * 支持长时间数据流聚合和规定窗口聚合
    * 支持Avg、Sum、Min、Max等函数
    * 支持`Group by` 分组和`having` 条件删选
  * 增量摘要
    * 支持处理和检索长时间运行的摘要
  * Table(表)
    * 用于存储事件以供将来处理并按需检索它们
    * 支持内存，RDBM，Solr，mongoDb等存储
  * Join(关联)
    * 根据条件加入两个流
    * 根据条件将流与表或增量摘要联系起来
    * 支持左联、右联、外联、内联
  * Pattern
    * 标识流之间的事件发生模式
    * 识别不发生的事件
    * 支持事件模式发生与逻辑条件和时间限制的重复匹配
  * Sequence(序列处理)
    * 从流中标识连续的事件序列
    * 支持零到多，一对多和零到一个条件
  * Parttions(分区)
    * 对查询进行分组，并基于关键字和值范围进行隔离并行处理
  * Scripting
    * 支持在Siddhi查询中编写JavaScript，Scala和R等脚本
  * 处理基于事件时间
    * 整个执行由事件时间驱动
* Publishing Events(事件发布)
  * 使用各种消息格式的各种数据源
  * 支持负载平衡和故障转移数据发布
* Snapshot and restore(快照和还原)
  * 支持长期执行的定期状态持久性和恢复功能



## 入门指南

Siddhi是一个100％开源的Java库，针对高性能进行了彻底优化.它对实时数据流执行流处理和复杂事件处理。Siddhi被许多公司使用，包括Uber和eBay（通过Apache Eagle）。优步每天使用Siddhi处理超过200亿个事件进行欺诈分析，而Siddhi则在Apache Eagle中用作策略执行引擎。

本快速入门指南包含以下六个部分：

1. 流处理和复杂事件处理概述 - 关于Siddhi的域名
2. Siddhi概述 - 解释基本架构
3. 首次使用Siddhi  - 如何设置软件
4. Siddhi'Hello World！' - 您的第一个Siddhi应用程序
5. 模拟事件 - 使用模拟事件测试查询
6. 流处理—时间事件处理

### 1、流处理和复杂事件处理(CEP)概述

在开始使用Siddhi之前，让我们首先简要地讨论流处理和复杂事件处理，以便我们能够识别可以使用Siddhi的用例。首先让我们通过一个例子来理解一个事件是什么。如果我们将通过ATM执行的事务视为数据流，则从ATM进行的一次取款可以视为事件。这个事件包含的数据量、时间、帐号等许多此类交易形式流。

![](https://wso2.github.io/siddhi/images/quickstart/event-stream.png?raw=true)

***Forrester*** 定义了流媒体分析: 流的定义

> 提供分析操作符来编排数据流、计算分析和检测来自多个不同实时数据源的事件数据模式的软件，允许开发人员构建实时感知、思考和行动的应用程序。

***Gartner’s IT Glossary*** 定义了CEP的概念

> CEP是一种计算，在这种计算中，有关事件的传入数据被提炼成更有用、更高级的“复杂”事件数据，从而能够洞察发生了什么。
>
>
>
> CEP是事件驱动的，因为计算是由事件数据的接收触发的。CEP可用于要求高、持续智能的应用程序，以增强态势感知和支持实时决策。

![](https://wso2.github.io/siddhi/images/quickstart/siddhi-basic.png?raw=true)

基本上,Siddhi实时接收数据event-by-event和处理他们产生有意义的信息。

Siddhi可以用在以下场景

* 欺诈行为分析
* 监控
* 异常捕获
* 情绪(观点)分析
* 处理客户的行为
* ...等等

### 2、Siddhi概要





![](https://wso2.github.io/siddhi/images/siddhi-overview.png?raw=true)

如上所示,Siddhi可以概括为:

* 接受来自许多不同类型的事件输入来源
* 处理它们产生的洞察数据(条件匹配到的数据)
* 将它们发布到许多类型的接收器中。

要使用Siddhi，您需要将处理逻辑编写为Siddhi流SQL语言中的Siddhi应用程序。在编写和启动Siddhi应用程序之后，

1. 将数据逐个作为事件
2. 处理每个事件数据
3. 根据目前完成的处理生成新的高级事件
4. 发送新生成的事件作为输出流。



### 3、第一次使用Siddhi

在本节中,我们将使用WSO2流处理器(称为SP在本指南)一个服务器版本的Siddhi,一个复杂的编辑器和一个GUI(称为“流处理器工作室”),您可以编写您的查询和模拟事件数据流。

**Step 1** — Install [Oracle Java SE Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html) version 1.8. 
**Step 2** — [Set the JAVA_HOME](https://docs.oracle.com/cd/E19182-01/820-7851/inst_cli_jdk_javahome_t/) environment variable. 
**Step 3** — Download the latest [WSO2 Stream Processor](http://wso2.com/analytics?utm_source=gitanalytics&utm_campaign=gitanalytics_Jul17). 
**Step 4** — Extract the downloaded zip and navigate to `<SP_HOME>/bin`. (`SP_HOME` refers to the extracted folder) 

**Step 5** — Issue the following command in the command prompt (Windows) / terminal (Linux)

> For Windows: editor.bat
>
> For Linux: ./editor.sh

关于WSO2流处理器的更多细节,请参阅[Quick Start Guide](https://docs.wso2.com/display/SP400/Quick+Start+Guide).成功启动流处理器Studio后，Linux中的终端如下图所示:

![](https://wso2.github.io/siddhi/images/quickstart/after-starting-sp.png?raw=true)

启动WSO2流处理器后，通过访问浏览器中的以下链接访问流处理器Studio。

> http://localhost:9390/editor

![](https://wso2.github.io/siddhi/images/quickstart/sp-studio.png?raw=true)



### 4、第一个siddhi程序‘Hello World!’

Siddhi流SQL是一种丰富、简洁、易于学习的SQL语言。让我们首先了解如何查找进入数据流的值的总数，并在每个事件中输出当前正在运行的总价值。Siddhi有许多内建的功能和扩展，可用于复杂分析，但首先让我们使用一个简单的功能。您可以在[Siddhi查询指南](https://wso2.github.io/siddhi/documentation/siddhi-4.0/)中找到关于Siddhi语法及其功能的更多信息。

让我们考虑这样一个场景，我们将货物箱装载到船上。我们需要跟踪增加的货物的总重量。在装货时测量货物箱的重量被认为是一个事件。

![](https://wso2.github.io/siddhi/images/quickstart/loading-ship.jpeg?raw=true)

我们可以写一个Siddhi程序对应上述场景4个部分。

**Part 1 —** 给我们的Siddhi应用一个合适的名字。这是Siddhi的例行程序。在本例中，我们将应用程序命名为HelloWorldApp

> @App:name("HelloWorldApp")

**Part 2 —**定义输入流。流需要有一个定义每个传入事件应该包含的数据的名称和模式。事件数据属性表示为名称和类型对。在这个例子中:

* 输入流的名称——“CargoStream”（这只包含一个数据属性）
* 数据在每一个事件的名称——“weight”
* "weight"为int类型数据

> define stream CargoStream (weight int);

**Part 3 —** 定义输出流。它的信息与前面的定义相同，还有一个额外的totalWeight属性，其中包含到目前为止计算的总权重。在这里,我们需要添加一个“sink”日志OutputStream这样我们可以观察到输出值。 (Sink是Siddhi将流发布到外部系统的方式。这个特定的日志类型sink只记录流事件。要了解更多关于sink的信息，请参阅[sink](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#sink))

> @sink(type='log',prefix='LOGGER')
> define stream OutputStream(weight int,totalWeight long);

**Part 4 —** Siddhi查询脚本，需要定义一下几个要素：

1. 定义查询名称 — *“HelloWorldQuery”*
2. 决定处理哪一个数据流— *“CargoStream”*
3. 我们在输出流中需要哪些数据— *“weight”*, *“totalWeight”*
4. 如何计算输出 - 通过计算权重之和
5. 应该使用输出填充哪个流— *“OutputStream”*

> @info(name='HelloWorldQuery')
> from CargoStream
> select weight,sum(weight) as totalWeight
> insert into OutputStream;

![](https://wso2.github.io/siddhi/images/quickstart/hello-query.png?raw=true)



### 5、事件模拟

Stream Processor Studio具有内置支持来模拟事件。您可以通过Stream Processor Studio左侧的“Event Simulator”面板进行操作。您应该在运行事件模拟之前通过浏览到文件 - >保存来保存HelloWorldApp。然后单击“事件模拟器”并按如下所示进行配置。

![](https://wso2.github.io/siddhi/images/quickstart/event-simulation.png?raw=true)



**Step 1 —Configurations:**

* Siddhi App Name — *“HelloWorldApp”*
* Stream Name — *“CargoStream”*
* Timestamp — (Leave it blank)
* weight — 2 (or some integer)

**Step 2 — Click “Run” mode and then click “Start”**

这启动了Siddhi应用程序。如果Siddhi应用程序成功启动，则会在Stream Processor Studio控制台中打印以下消息：*“HelloWorldApp.siddhi Started Successfully!”*

**Step 3 — Click “Send” and observe the terminal** 

你在哪里开始WSO2 Stream Processor Studio。您可以看到包含“outputData = [2,2]”的日志。再次单击“发送”并观察“outputData = [2,4]”的日志。您可以更改重量的值并将其发送以查看权重总和的更新方式。

![](https://wso2.github.io/siddhi/images/quickstart/log.png?raw=true) 

好样的！您已成功完成Siddhi Hello World的创建！

### 6、流处理—时间事件处理

本节演示如何使用Siddhi执行时间窗口处理。到目前为止，我们一直在执行处理，只在内存中运行总和值。在此过程中没有存储任何事件。[窗口处理](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#window)是一种允许我们在给定时间段内将一些事件存储在内存中的方法，以便我们可以执行诸如计算其中的平均值，最大值等操作。

让我们想象一下，当我们将货箱装入船上时，我们需要跟踪最近装载的箱子的平均重量，以便我们可以平衡船上的重量。为此，我们试着找出每个事件最后三个方框的平均权重。

![](https://wso2.github.io/siddhi/images/quickstart/siddhi-windows.png?raw=true)

对于窗口处理，我们需要修改我们的查询，如下所示：

> @App:name("HelloWOrldApp")
> @App:description("Description of the plan")
>
> -- Please refer to https://docs.wso2.com/display/SP400/Quick+Start+Guide on getting started with SP editor. 
>
> define stream CargoStream (weight int);
>
> @sink(type='log',prefix='LOGGER')
> define stream OutputStream(weight int,totalWeight long,averageWeight double);
>
> @info(name='HelloWorldQuery')
> from CargoStream#window.length(3)
> select weight,sum(weight) as totalWeight,avg(weight) as averageWeight
> insert into OutputStream;

* `avg(weight) as averageWeight` -这里，我们指定最后3个事件应该保存在内存中进行处理。
* `avg(weight) as averageWeight` - 这里，我们计算窗口中存储的事件的平均值，并将平均值产生为“averageWeight”（注意：现在总和也根据最后三个事件计算totalWeight）。

我们还需要修改“OutputStream”定义以适应新的“averageWeight”。

> define stream OutputStream(weight int,totalWeight long,averageWeight double);

更新的Siddhi应用程序应如下所示：

![](https://wso2.github.io/siddhi/images/quickstart/window-processing-app.png?raw=true) 



现在，您可以使用事件模拟器发送事件并观察日志以查看最近三次货物事件的权重总和和平均值。值得注意的是，定义的长度窗口仅在内存中保留3个事件。当第4个事件到达时，窗口中的第一个事件将从内存中删除。这可确保内存使用量不会超出特定限制。在Siddhi还有其他实现来减少内存消耗有关更多信息，请参阅[Siddhi Architecture](https://wso2.github.io/siddhi/documentation/siddhi-architecture/).

要了解有关Siddhi功能的更多信息，请参阅 [Siddhi Query Guide](https://wso2.github.io/siddhi/documentation/siddhi-4.0/).请随意尝试Siddhi和事件模拟，以更好地理解Siddhi。如果您有任何疑问，请使用“[Siddhi](http://stackoverflow.com/search?q=siddhi)”标签将它们发布到Stackoverflow。



## Documentation

### 用户指南

#### 在[WSO2流处理器](https://github.com/wso2/product-sp)中使用Siddhi

* 您可以在最新的WSO2流处理器中使用Siddhi，它是WSO2 Analytics产品的一部分，具有编辑器，调试器和仿真支持。
* 默认情况下，所有Siddhi扩展都随WSO2流处理器一起提供。
* 有关更多信息，请参阅“[WSO2 SP快速入门指南](https://docs.wso2.com/display/SP400/Quick+Start+Guide)”。

#### 使用Siddhi作为Java库

* 要将Siddhi作为java库嵌入到您的项目中并获得一个工作示例，请遵循以下步骤：

      **Step 1:** 创建Java项目

使用Maven创建Java项目，并在其pom.xml文件中包含以下依赖项

```xml
   <dependency>
     <groupId>org.wso2.siddhi</groupId>
     <artifactId>siddhi-core</artifactId>
     <version>4.x.x</version>
   </dependency>
   <dependency>
     <groupId>org.wso2.siddhi</groupId>
     <artifactId>siddhi-query-api</artifactId>
     <version>4.x.x</version>
   </dependency>
   <dependency>
     <groupId>org.wso2.siddhi</groupId>
     <artifactId>siddhi-query-compiler</artifactId>
     <version>4.x.x</version>
   </dependency>
   <dependency>
     <groupId>org.wso2.siddhi</groupId>
     <artifactId>siddhi-annotations</artifactId>
     <version>4.x.x</version>
   </dependency>  
```

**注意：**您可以使用您喜欢的任何方法创建Java项目。可以从[此处下载](http://maven.wso2.org/nexus/content/groups/wso2-public/org/wso2/siddhi/)所需的依赖项。*在Maven项目中创建一个新的Java类。

      **Step 2:** 创建Siddhi应用

Siddhi应用程序是一个自包含的执行实体，用于定义如何捕获，处理和发送数据。

* 通过定义流定义来创建一个Siddhi应用程序，例如定义传入事件的格式的stockeventstream，以及如下定义Siddhi查询。

```java
    String siddhiApp = "define stream StockEventStream (symbol string, price float, volume long); " +
            " " +
            "@info(name = 'query1') " +
            "from StockEventStream#window.time(5 sec)  " +
            "select symbol, sum(price) as price, sum(volume) as volume " +
            "group by symbol " +
            "insert into AggregateStockStream ;";
```



此Siddhi查询按符号对事件进行分组，并计算聚合，例如最后5秒时间窗口的价格总和和总和。然后，它将结果插入名为AggregateStockStream的流中。

       **Step 3:** 创建Siddhi 运行程序

这一步涉及到创建一个Siddhi应用程序的运行器。

```java
    SiddhiManager siddhiManager = new SiddhiManager();
    SiddhiAppRuntime siddhiAppRuntime = siddhiManager.createSiddhiAppRuntime(siddhiApp);
```



Siddhi Manager解析Siddhi应用程序并为您提供Siddhi应用程序运行时。此Siddhi应用程序运行时可用于添加回调和输入处理程序，以便您可以以编程方式调用Siddhi应用程序。

      **Seep4:** 注册回调函数

您可以将回调函数注册到Siddhi应用程序运行时，以便在处理事件后接收结果。有两种类型的回调：

* 查询回调：这订阅了一个查询。
* 流回调：这订阅了一个事件流。在此示例中，Stream回调被添加到AggregateStockStream以捕获已处理的事件。

```java
siddhiAppRuntime.addCallback("AggregateStockStream", new StreamCallback() {
            @Override
            public void receive(Event[] events) {
                EventPrinter.print(events);
            }
        });
```



这里，一旦生成结果，它们就会被发送到此回调的receive方法。在此回调中添加了一个事件打印机，用于打印传入事件以进行演示。

      **Seep5:** 发送事件

为了以编程方式从流中发送事件，您需要获取它的输入处理程序，如下所示：

```java
InputHandler inputHandler = siddhiAppRuntime.getInputHandler("AggregateStockStream");
```

使用以下代码启动Siddhi应用程序运行时，发送事件并关闭Siddhi：

```java
siddhiAppRuntime.start();
inputHandler.send(new Object[]{"IBM", 100f, 100L});
Thread.sleep(1000);
inputHandler.send(new Object[]{"IBM", 200f, 300L});
inputHandler.send(new Object[]{"WSO2", 60f, 200L});
Thread.sleep(1000);
inputHandler.send(new Object[]{"WSO2", 70f, 400L});
inputHandler.send(new Object[]{"GOOG", 50f, 30L});
Thread.sleep(1000);
inputHandler.send(new Object[]{"IBM", 200f, 400L});
Thread.sleep(2000);
inputHandler.send(new Object[]{"WSO2", 70f, 50L});
Thread.sleep(2000);
inputHandler.send(new Object[]{"WSO2", 80f, 400L});
inputHandler.send(new Object[]{"GOOG", 60f, 30L});
Thread.sleep(1000);

siddhiAppRuntime.shutdown();
siddhiManager.shutdown();
```

![](http://www.zhangchi.ink:8080/img/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20181103110651.png) 

发送事件后，您可以看到事件打印机记录的输出。在此处查找此示例的可执行[Java代码](https://github.com/wso2/siddhi/blob/master/modules/siddhi-samples/quick-start-samples/src/main/java/org/wso2/siddhi/sample/TimeWindowSample.java)，有关更多代码示例，请参阅Siddhi的[快速入门](https://github.com/wso2/siddhi/tree/master/modules/siddhi-samples/quick-start-samples)示例。



#### 系统配置要求

1. 最小内存 -  500 MB（基于存储的内存数据进行处理）
2. 处理器 -  Pentium 800MHz或至少等效
3. Java SE Development Kit 1.8（1.7版本为3.x版）
4. 要从Source发行版构建Siddhi，您必须拥有JDK 1.8版本（1.7版本为3.x版本）或更高版本以及Maven 3.0.4或更高版本

### Siddhi Streaming SQL Guide 4.0

####介绍

Siddhi Streaming SQL设计用于以流方式处理事件流，检测复杂事件发生，并实时通知事件发生。

#### 应用

可以使用Siddhi Streaming SQL编写流处理和复杂事件处理规则，它们可以作为`SiddhiApp`放在一个文件中。

**目的**

每个Siddhi应用程序都是一个独立的处理单元，允许您独立于系统中的其他Siddhi应用程序部署和执行查询。下图描述了事件流如何与Siddhi应用程序的一些关键Siddhi Streaming SQL元素一起使用。

![](https://wso2.github.io/siddhi/images/event-flow.png?raw=true) 

下表提供了Siddhi Streaming SQL语言中几个关键元素的简要说明。

| 关键元素              | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| Stream                | 一组按时间顺序排列的事件，具有惟一可识别的名称，以及一组具有定义其模式的特定数据类型的已定义属性。 |
| Event                 | 事件仅与一个流相关联，并且该流的所有事件都具有一组相同的属性，这些属性被分配了特定类型（或相同的模式）。事件包含根据模式的时间戳和一组属性值。 |
| Table                 | 使用定义的模式存储的数据的结构化表示。存储的数据可由`In-Memory`，`RDBM`，`MongoDB`等支持，以便在运行时访问和操作。 |
| Query                 | 通过组合现有流和/或表以流方式处理事件并将事件生成到输出流或表的逻辑构造。查询使用一个或多个输入流，以及零个或一个表。然后，它以流方式处理这些事件，并将输出事件发布到流或表以供进一步处理或生成通知。 |
| Source                | 以事件形式从外部源（例如TCP，Kafka，HTTP等）使用数据的合同，然后将每个事件（可以是XML，JSON，二进制等格式）转换为Siddhi事件，以及将其传递给Stream进行处理。 |
| Sink                  | 接收到达流的事件，将它们映射到预定义的数据格式(如XML、JSON、二进制等)，并将它们发布到外部端点(如电子邮件、TCP、Kafka、HTTP等)的契约。 |
| Input Handler         | 一种以编程方式将事件注入流的机制。                           |
| Stream/Query Callback | 一种以编程方式使用流和查询中的输出事件的机制                 |
| Partition             | 一个逻辑容器，用于隔离基于分区键的查询处理。这里，为每个分区键生成一个单独的查询实例以实现隔离。 |
| Inner Stream          | 一个可定位的流，在分区内连接已分配的查询，保持隔离。         |

**语法**

Siddhi SQL的一个元素可以作为Siddhi应用程序中的脚本组合在一起。这里每个构造必须用分号（;）分隔，如下面的语法所示。

```
<siddhi app>  : 
        <app annotation> * 
        ( <stream definition> | <table definition> | ... ) + 
        ( <query> | <partition> ) +
        ;
```

示例Siddhi名为Temperature-Analytics的应用程序使用名为TempStream的流和名为5minAvgQuery的查询进行定义以进行处理。

```
@app:name('Temperature-Analytics')

define stream TempStream (deviceID long, roomNo int, temp double);

@name('5minAvgQuery')
from TempStream#window.time(5 min)
select roomNo, avg(temp) as avgTemp
  group by roomNo
insert into OutputStream;
```

#### Stream

流是按时间排序的逻辑系列事件。它的模式是通过流定义定义的。流定义包含唯一名称和一组属性，这些属性在流中具有特定类型和唯一可识别名称。选择接收到特定流中的所有事件具有相同的模式（即，以相同的顺序具有相同的属性）。

**目的**

通过定义模式，它将公共事件类型统一在一起。这使它们能够通过查询以流的方式使用其定义的属性进行处理，并允许接收和源将事件映射到/从各种数据格式。

**语法**

定义新流的语法如下所示。

```
define stream <stream name> (<attribute name> <attribute type>, <attribute name> <attribute type>, ... );
```

在流定义中配置以下参数。

| Parameter        | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `stream name`    | 创建的流的名称。（建议在`PascalCase`中定义流名称。）         |
| `attribute name` | 流的模式由其具有惟一可识别属性名的属性定义。 (It is recommended to define attribute names in `camelCase`.) |
| `attribute type` | 模式中定义的每个属性的类型。  This can be `STRING`, `INT`, `LONG`, `DOUBLE`, `FLOAT`, `BOOL` or `OBJECT`. |

要以异步和多线程方式创建流处理事件，请使用@Async注释，如[线程和异步配置](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#threading-and-asynchronous)部分所示。

例如：

```
define stream TempStream (deviceID long, roomNo int, temp double);
```

以上创建了一个名为`TempStream`的流，其中包含以下属性。

- `deviceID` of type `long`
- `roomNo` of type `int`
- `temp` of type `double`

#####Source 数据源

源通过多种传输和各种数据格式接收事件，并将它们引导到流中进行处理。源配置允许您定义映射，以便将每个传入事件从其本机数据格式转换为Siddhi事件。当未提供对此类映射的自定义时，Siddhi假定到达事件基于流定义和所选消息格式遵循预定义格式。

**目的**

Source允许Siddhi使用来自外部系统的事件，并映射事件以遵守相关的流。

**语法**

要配置通过源使用事件的流，请通过添加带有所需参数值的`@source`注释将源配置添加到流定义。源语法如下：

```
@source(type='source_type', static.option.key1='static_option_value1', static.option.keyN='static_option_valueN',
    @map(type='map_type', static.option_key1='static_option_value1', static.option.keyN='static_option_valueN',
        @attributes( attributeN='attribute_mapping_N', attribute1='attribute_mapping_1')
    )
)
define stream StreamName (attribute1 Type1, attributeN TypeN);
```

此语法包括以下注释。@source的type参数定义接收事件的源类型。要配置的其他参数取决于所选的源类型，某些参数是可选的。有关参数的详细信息，请参阅相关源的文档。以下是当前支持的源类型列表：

* [HTTP](https://wso2-extensions.github.io/siddhi-io-http/)
* [kafka](https://wso2-extensions.github.io/siddhi-io-kafka/)

- [TCP](https://wso2-extensions.github.io/siddhi-io-tcp/)
- [In-memory](https://wso2.github.io/siddhi/api/latest/#inmemory-source)
- [WSO2Event](https://wso2-extensions.github.io/siddhi-io-wso2event/)
- [Email](https://wso2-extensions.github.io/siddhi-io-email/)
- [JMS](https://wso2-extensions.github.io/siddhi-io-jms/)
- [File](https://wso2-extensions.github.io/siddhi-io-file/)
- [RabbitMQ](https://wso2-extensions.github.io/siddhi-io-rabbitmq/)
- [MQTT](https://wso2-extensions.github.io/siddhi-io-mqtt/)
- [WebSocket](https://wso2-extensions.github.io/siddhi-io-websocket/)
- [Twitter](https://wso2-extensions.github.io/siddhi-io-twitter/)
- [Amazon SQS](https://wso2-extensions.github.io/siddhi-io-sqs/)



##### Source 映射

每个`@source`配置都有一个由`@map`注释表示的映射，它将传入的消息格式转换为Siddhi事件。`@map`的type参数定义了用于映射数据的映射类型。要配置的其他参数取决于所选的映射器。其中一些参数是可选的。有关参数的详细信息，请参阅相关映射器的文档。

>如果未提供`@map`注释，则使用`@map（type ='passThrough'）`作为默认值。当源使用Siddhi事件时以及不需要任何映射时，可以使用此默认映射器类型。



**Map Attributes**

`@attributes`是一个可选的注释，与`@map`一起用于定义自定义映射。如果未提供`@attributes`，则每个映射器都假定传入事件遵循其自己的默认数据格式。通过添加`@attributes`注释，您可以配置映射器以选择性地从传入消息中提取数据，并将它们分配给属性。您可以通过两种方式配置map attributes。

1. 将属性定义为键并将内容映射为以下格式的值: `@attributes( attributeN='mapping_N', attribute1='mapping_1')`
2. 按照与流定义中定义属性的顺序相同的顺序定义所有属性的映射内容:`@attributes( 'mapping_1', 'mapping_N')`

**支持的映射类型**

以下是当前支持的源映射类型的列表：

- [WSO2Event](https://wso2-extensions.github.io/siddhi-map-wso2event/)
- [XML](https://wso2-extensions.github.io/siddhi-map-xml/)
- [TEXT](https://wso2-extensions.github.io/siddhi-map-text/)
- [JSON](https://wso2-extensions.github.io/siddhi-map-json/)
- [Binary](https://wso2-extensions.github.io/siddhi-map-binary/)
- [Key Value](https://wso2-extensions.github.io/siddhi-map-keyvalue/)
- [CSV](https://wso2-extensions.github.io/siddhi-map-csv/)

例子：此查询通过HTTP源以JSON数据格式接收事件，并将它们定向到InputStream流进行处理。这里，HTTP源配置为在foo上下文上接收8080port上所有网络接口上的事件，并通过基本身份验证进行保护。

> @source(type='http', receiver.url='http://0.0.0.0:8080/foo', basic.auth.enabled='true', @map(type='json'))
> define stream InputStream (name string, age int, country string);

#### 接收器 Sink

接收器通过多种传输将来自流的事件以各种数据格式发布到外部端点。接收器配置允许您定义映射以将Siddhi事件转换为所需的输出数据格式（例如JSON，TEXT，XML等）。当未提供对此类映射的自定义时，Siddhi会根据流定义和所选数据格式将事件转换为其默认格式以发布事件。

**目的**

Sinks提供了一种以首选数据格式将Siddhi事件发布到外部系统的方法。

**语法**

要配置流以通过接收器发布事件，请通过添加带有所需参数值的`@sink`注释将接收器配置添加到流定义。接收器语法如下：

```
@sink(type='sink_type', static_option_key1='static_option_value1', dynamic_option_key1='{{dynamic_option_value1}}',
    @map(type='map_type', static_option_key1='static_option_value1', dynamic_option_key1='{{dynamic_option_value1}}',
        @payload('payload_mapping')
    )
)
define stream StreamName (attribute1 Type1, attributeN TypeN);
```

> 分类为动态的接收器和接收器映射器属性具有从其关联流中吸收属性值的能力。在配置属性值时，可以使用双花括号中的属性名称来完成此操作。
>
> 一些有效的动态属性值是:
>
> - attribute1
> - This is attribute1
> - attribute1 > attributeN
>
> 这里双花括号中的属性名称将在执行期间被事件值替换。

此语法包括以下注释。@sink注释的type参数定义发布事件的接收器类型。要配置的其他参数取决于所选的接收器类型。其中一些参数是可选的，一些参数可以具有动态值。有关参数的详细信息，请参阅相关接收器的文档。有关参数的详细信息，请参阅相关接收器的文档。

- [HTTP](https://wso2-extensions.github.io/siddhi-io-http/)
- [Kafka](https://wso2-extensions.github.io/siddhi-io-kafka/)
- [TCP](https://wso2-extensions.github.io/siddhi-io-tcp/)
- [In-memory](https://wso2.github.io/siddhi/api/latest/#inmemory-sink)
- [WSO2Event](https://wso2-extensions.github.io/siddhi-io-wso2event/)
- [Email](https://wso2-extensions.github.io/siddhi-io-email/)
- [JMS](https://wso2-extensions.github.io/siddhi-io-jms/)
- [File](https://wso2-extensions.github.io/siddhi-io-file/)
- [RabbitMQ](https://wso2-extensions.github.io/siddhi-io-rabbitmq/)
- [MQTT](https://wso2-extensions.github.io/siddhi-io-mqtt/)
- [WebSocket](https://wso2-extensions.github.io/siddhi-io-websocket/)
- [Amazon SQS](https://wso2-extensions.github.io/siddhi-io-sqs/)

#####分布式接收器 Distributed Sink

分布式接收器使用负载平衡和分区策略将事件从定义的流发布到多个目标端点。任何普通的接收器都可以用作分布式接收器。分布式接收器配置允许您定义公共映射以转换其所有目标端点的Siddhi事件，允许您定义分发策略（例如，`roundRobin`，`partitioned`）以及每个特定端点目标的配置。

**目的**

分布式接收器提供了一种以首选数据格式将Siddhi事件发布到多个目标端点的方法。

**语法**

要配置流以通过分布式接收器发布事件，请通过添加`@sink`注释将接收器配置添加到流定义，并添加`@sink`注释内所有目标端点的公共配置参数以及`@distribution`和`@destination`注释提供分发策略和端点特定配置。分布式接收器语法如下：

1. RoundRobin分布式接收器：以循环方式将事件发布到定义的目标。

   > @sink(type='sink_type', common_option_key1='common_option_value1', common_option_key2='{{common_option_value1}}',
   > ​    @map(type='map_type', option_key1='option_value1', option_key2='{{option_value1}}',
   > ​        @payload('payload_mapping')
   > ​    )
   > ​    @distribution(strategy='roundRobin',
   > ​        @destination(specific_option_key1='specific_option_value1'),
   > ​        @destination(specific_option_key1='specific_option_value2')))
   > )
   > define stream StreamName (attribute1 Type1, attributeN TypeN);

2. 分区分布式接收器：通过基于事件分区键的哈希码进行分区，将事件发布到定义的目标。

   > @sink(type='sink_type', common_option_key1='common_option_value1', common_option_key2='{{common_option_value1}}',
   > ​    @map(type='map_type', option_key1='option_value1', option_key2='{{option_value1}}',
   > ​        @payload('payload_mapping')
   > ​    )
   > ​    @distribution(strategy='partitioned', partitionKey='partition_key',
   > ​        @destination(specific_option_key1='specific_option_value1'),
   > ​        @destination(specific_option_key1='specific_option_value2')))
   > )
   > define stream StreamName (attribute1 Type1, attributeN TypeN);

#####Sink Mapper

每个`@sink`注释都有一个由`@map`注释表示的映射，该映射将Siddhi事件转换为传出消息格式。`@map`注释的`type`参数定义事件映射的映射类型。要配置的其他参数取决于所选的映射器。其中一些参数是可选的，一些参数具有动态值。有关参数的详细信息，请参阅相关映射类型的文档。

> 如果未提供`@map`注释，则默认使用`@map（type ='passThrough'）`。当接收器以Siddhi事件格式发布时，或者当它不需要任何映射时，可以使用此方法。

**有效的负载映射 Map Payload**

`@payload`是一个可选的注释，与`@map`注释一起用于定义自定义映射。如果未提供`@payload`批注，则每个映射器将传出事件映射到其自己的默认数据格式。通过定义`@payload`注释，您可以配置映射器以使用您选择的属性名称生成输出有效负载，使用动态属性，通过有选择地分配首选格式的属性。有两种方法可以配置`@payload`注释。

1. 某些映射器（如XML，JSON和Test）仅使用以下格式接受一个输出有效内容：`@payload( 'This is a test message from {{user}}.' )`
2. 一些映射器这样的键值接受一系列映射值定义如下：`@payload( key1='mapping_1', key2='user : {{user}}')`

**支持的映射类型**

以下是当前支持的接收器映射类型的列表：

- [WSO2Event](https://wso2-extensions.github.io/siddhi-map-wso2event/)
- [XML](https://wso2-extensions.github.io/siddhi-map-xml/)
- [TEXT](https://wso2-extensions.github.io/siddhi-map-text/)
- [JSON](https://wso2-extensions.github.io/siddhi-map-json/)
- [Binary](https://wso2-extensions.github.io/siddhi-map-binary/)
- [Key Value](https://wso2-extensions.github.io/siddhi-map-keyvalue/)
- [CSV](https://wso2-extensions.github.io/siddhi-map-csv/)

例如：以下查询将OutputStream流中的事件发布到HTTP端点。这里，事件被映射到默认的JSON有效负载，并使用POST方法和Accept标头发送到http：// localhost：8005 / endpoint，并通过基本身份验证进行保护，其中admin是用户名和密码。

> @sink(type='http', publisher.url='http://localhost:8005/endpoint', method='POST', headers='Accept-Date:20/02/2017', 
>   basic.auth.username='admin', basic.auth.password='admin', basic.auth.enabled='true',
>   @map(type='json'))
> define stream OutputStream (name string, ang int, country string);

以下查询使用分区策略将OutputStream流中的事件发布到多个HTTP端点。这里事件基于分区键国家发送到http：// localhost：8005 / endpoint1或http：// localhost：8006 / endpoint2。它使用默认的JSON映射，POST方法，并在发布到两个端点时使用admin作为用户名和密码。

> @sink(type='http', method='POST', basic.auth.username='admin', basic.auth.password='admin', 
>   basic.auth.enabled='true', @map(type='json'),
>   @distribution(strategy='partitioned', partitionKey='country',
> ​     @destination(publisher.url='http://localhost:8005/endpoint1'),
> ​     @destination(publisher.url='http://localhost:8006/endpoint2')))
> define stream OutputStream (name string, ang int, country string);

####Query

每个Siddhi查询可以使用一个或多个流，0-1表，以流方式处理事件，然后生成输出事件到流或对表执行CRUD操作。

**目的**

通过查询，您可以按照到达的顺序逐个处理传入事件，从而执行复杂的事件处理和流处理操作。

**语法**

所有查询都包含输入和输出部分。有些还包含投影部分。所有三个部分的简单查询如下。

```
from <input stream> 
select <attribute name>, <attribute name>, ...
insert into <output stream/table>
```

例如Siddhi应用程序中包含的此查询使用来自`TempStream`流（已定义）的事件，并将房间温度和房间号输出到`RoomTempStream`流。

```
define stream TempStream (deviceID long, roomNo int, temp double);

from TempStream 
select roomNo, temp
insert into RoomTempStream;
```

> 推断流：
>
> 这里，RoomTempStream是一个推断的Stream，这意味着它可以用作任何其他定义的流，而无需显式定义其流定义。RoomTempStream的定义是从生成流的第一个查询推断出来的。

#####Query Projection

siddhiql支持以下查询投影。

<table style="width:100%">
    <tr>
        <th>Action</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>选择投影所需要的对象</td>
        <td>这涉及仅从输入流中选择一些属性以插入到输出流中.
            <br><br>
            E.g., 以下查询仅从`TempStream`流中选择`roomNo`和`temp`属性。.
            <pre style="align:left">from TempStream<br>select roomNo, temp<br>insert into RoomTempStream;</pre>
        </td>
    </tr>
    <tr>
        <td>选择投影的所有属性</td>
        <td>选择要插入到输出流中的输入流中的所有属性。这可以通过使用星号（*）或省略`select`语句来完成。.
            <br><br>
            E.g., 以下两个查询都选择了`NewTempStream`流中的所有属性。.
            <pre>from TempStream<br>select *<br>insert into NewTempStream;</pre>
            or
            <pre>from TempStream<br>insert into NewTempStream;</pre>
        </td>
    </tr>
    <tr>
        <td>重命名属性</td>
        <td>这将从输入流中选择属性，并将它们插入到具有不同名称的输出流中.
            <br><br>
            E.g.,此查询将`roomNo`重命名为`roomNumber`，将`temp`重命名为`temperature`.
            <pre>from TempStream <br>select roomNo as roomNumber, temp as temperature<br>insert into RoomTempStream;</pre>
        </td>
    </tr>
    <tr>
        <td>引入恒定值</td>
        <td>这通过使用`as`将其赋值给属性来添加常量值.
            <br></br>
            E.g., 此查询指定'C'用作`scale`属性的常量值. 
            <pre>from TempStream<br>select roomNo, temp, 'C' as scale<br>insert into RoomTempStream;</pre>
        </td>
    </tr>
    <tr>
        <td>使用数学和逻辑表达式</td>
        <td>这将使用下面给出的优先顺序中的数学和逻辑表达式的属性，并使用`as`将它们分配给输出属性。
            <br><br>
            <b>Operator precedence</b><br>
            <table style="width:100%">
                <tr>
                    <th>Operator</th>
                    <th>Distribution</th>
                    <th>Example</th>
                </tr>
                <tr>
                    <td>
                        ()
                    </td>
                    <td>
                        范围
                    </td>
                    <td>
                        <pre>(cost + tax) * 0.05</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                         IS NULL
                    </td>
                    <td>
                        Null check
                    </td>
                    <td>
                        <pre>deviceID is null</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                        NOT
                    </td>
                    <td>
                        逻辑否
                    </td>
                    <td>
                        <pre>not (price > 10)</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                         *   /   %  
                    </td>
                    <td>
                        乘法, 除法, 取模
                    </td>
                    <td>
                        <pre>temp * 9/5 + 32</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                        +   -  
                    </td>
                    <td>
                        加法, 减法
                    </td>
                    <td>
                        <pre>temp * 9/5 - 32</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                        <   <=   >   >=
                    </td>
                    <td>
                        Comparators: less-than, greater-than-equal, greater-than, less-than-equal
                    </td>
                    <td>
                        <pre>totalCost >= price * quantity</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                        ==   !=  
                    </td>
                    <td>
                        Comparisons: equal, not equal
                    </td>
                    <td>
                        <pre>totalCost !=  price * quantity</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                        IN
                    </td>
                    <td>
                        Contains in table
                    </td>
                    <td>
                        <pre>roomNo in ServerRoomsTable</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                        AND
                    </td>
                    <td>
                        Logical AND
                    </td>
                    <td>
                        <pre>temp < 40 and (humidity < 40 or humidity >= 60)</pre>
                    </td>
                </tr>
                <tr>
                    <td>
                        OR
                    </td>
                    <td>
                        Logical OR
                    </td>
                    <td>
                        <pre>temp < 40 or (humidity < 40 and humidity >= 60)</pre>
                    </td>
                </tr>
            </table>
            E.g., 将摄氏温度转换为华氏温度，并将房间号在10到15之间的房间识别为服务器房间.
            <pre>from TempStream<br>select roomNo, temp * 9/5 + 32 as temp, 'F' as scale, roomNo > 10 and roomNo < 15 as isServerRoom<br>insert into RoomTempStream;</pre>       
    </tr>

##### Function

函数消耗零个，一个或多个参数，并始终生成结果值。它可以在任何可以使用属性的位置使用。

**目的**

函数封装了复杂的执行逻辑，使Siddhi应用程序简单易懂。

**函数参数**

函数参数可以是属性，常量值，其他函数的结果，数学或逻辑表达式的结果或时间参数。函数参数取决于被调用的函数。

Time是一个特殊参数，可以使用整数时间值，后跟单位为`<int>` `<unit>`来定义。以下是支持的单位类型。执行时，`time`将以毫秒为单位的值返回为`long`值。

| Unit         | Syntax                      |
| ------------ | --------------------------- |
| Year         | year \| years               |
| Month        | month \| months             |
| Week         | week \| weeks               |
| Day          | day \| days                 |
| Hour         | hour \| hours               |
| Minutes      | minute \| minutes \| min    |
| Seconds      | second \| seconds \| sec    |
| Milliseconds | millisecond \| milliseconds |

E.g.通过1小时25分钟到test（）函数。

```
test(1 hour 25 min)
```

> 函数，数学表达式和逻辑表达式可以以嵌套方式使用。

以下是Siddhi附带的一些内置函数，更多函数引用执行[扩展](https://wso2.github.io/siddhi/extensions/)。

- [eventTimestamp](https://wso2.github.io/siddhi/api/latest/#eventtimestamp-function)
- [log](https://wso2.github.io/siddhi/api/latest/#log-stream-processor)
- [UUID](https://wso2.github.io/siddhi/api/latest/#uuid-function)
- [default](https://wso2.github.io/siddhi/api/latest/#default-function)
- [cast](https://wso2.github.io/siddhi/api/latest/#cast-function)
- [convert](https://wso2.github.io/siddhi/api/latest/#convert-function)
- [ifThenElse](https://wso2.github.io/siddhi/api/latest/#ifthenelse-function)
- [minimum](https://wso2.github.io/siddhi/api/latest/#minimum-function)
- [maximum](https://wso2.github.io/siddhi/api/latest/#maximum-function)
- [coalesce](https://wso2.github.io/siddhi/api/latest/#coalesce-function)
- [instanceOfBoolean](https://wso2.github.io/siddhi/api/latest/#instanceofboolean-function)
- [instanceOfDouble](https://wso2.github.io/siddhi/api/latest/#instanceofdouble-function)
- [instanceOfFloat](https://wso2.github.io/siddhi/api/latest/#instanceoffloat-function)
- [instanceOfInteger](https://wso2.github.io/siddhi/api/latest/#instanceofinteger-function)
- [instanceOfLong](https://wso2.github.io/siddhi/api/latest/#instanceoflong-function)
- [instanceOfString](https://wso2.github.io/siddhi/api/latest/#instanceofstring-function)

E.g.以下配置将`roomNo`转换为`string`，并使用`convert`和`UUID`函数为每个事件添加`messageID`。

```
from TempStream
select convert(roomNo, 'string') as roomNo, temp, UUID() as messageID
insert into RoomTempStream;
```

##### Filter

过滤器包含在查询中，以根据指定条件过滤来自输入流的信息。

**目的**

过滤器允许您将与特定条件匹配的事件分离为输出，或进行进一步处理。

**语法**

过滤条件应在输入流名称旁边的方括号中定义，如下所示。

```
from <input stream>[<filter condition>]
select <attribute name>, <attribute name>, ...
insert into <output stream>
```

E.g 此查询过滤房间号在100-210范围内并且`TempStream`流的温度大于40度，并将结果插入到`HighTempStream`流中。

```
from TempStream[(roomNo >= 100 and roomNo < 210) and temp > 40]
select roomNo, temp
insert into HighTempStream;
```

##### Window

Windows允许您根据输入流中的特定条件捕获事件子集以进行计算。每个输入流最多只能有一个窗口。

**目的**

基于持续时间，事件数量等来处理流中的事件子集。窗口可以以滑动或翻滚（批量）方式操作。

**语法**

应该在相关流旁边插入`#window`前缀以使用窗口。

```
from <input stream>#window.<window name>(<parameter>, <parameter>, ... )
select <attribute name>, <attribute name>, ...
insert <event type> into <output stream>
```

> 可以在窗口之前和/或之后应用过滤条件

E.g 如果要识别最近10个事件中的最高温度，则需要定义10个事件的长度窗口。该窗口以滑动模式操作，其中当按顺序接收12个事件的列表时，计算以下3个子集。

| Subset | Event Range |
| ------ | ----------- |
| 1      | 1-10        |
| 2      | 2-11        |
| 3      | 3-12        |

以下查询从`TempStream`流中查找最近10个事件的最高温度，并将结果插入`MaxTempStream`流。

```
from TempStream#window.length(10)
select max(temp) as maxTemp
insert into MaxTempStream;
```

如果定义每10个事件中的最高温度读数，则需要定义10个事件的`lengthBatch`窗口。该窗口作为批/翻滚模式运行，其中当按顺序接收30个事件的列表时，计算以下3个子集。

| Subset | Event Range |
| ------ | ----------- |
| 1      | 1-10        |
| 2      | 11-20       |
| 3      | 21-30       |

以下查询从`TempStream`流中查找每10个事件中的最高温度，并将结果插入`MaxTempStream`流。

```
from TempStream#window.lengthBatch(10)
select max(temp) as maxTemp
insert into MaxTempStream;
```

> 可以通过`time`窗口和timeBatch窗口以及其他时间基于时间来完成类似的操作。诸如`＃window.time`（10分钟）之类的代码段考虑以最后10分钟以滑动方式到达的事件，`＃window.timeBatch`（2分钟）考虑以翻滚方式每2分钟到达的事件。

以下是Siddhi附带的一些内置窗口。有关更多窗口类型，请参阅执行[extensions](https://wso2.github.io/siddhi/extensions/)。

- [time](https://wso2.github.io/siddhi/api/latest/#time-window)
- [timeBatch](https://wso2.github.io/siddhi/api/latest/#timebatch-window)
- [timeLength](https://wso2.github.io/siddhi/api/latest/#timelength-window)
- [length](https://wso2.github.io/siddhi/api/latest/#length-window)
- [lengthBatch](https://wso2.github.io/siddhi/api/latest/#lengthbatch-window)
- [sort](https://wso2.github.io/siddhi/api/latest/#sort-window)
- [frequent](https://wso2.github.io/siddhi/api/latest/#frequent-window)
- [lossyFrequent](https://wso2.github.io/siddhi/api/latest/#lossyfrequent-window)
- [cron](https://wso2.github.io/siddhi/api/latest/#cron-window)
- [externalTime](https://wso2.github.io/siddhi/api/latest/#externaltime-window)
- [externalTimeBatch](https://wso2.github.io/siddhi/api/latest/#externaltimebatch-window)
- [delay](https://wso2.github.io/siddhi/api/latest/#delay-window)

**输出事件类型**

查询的投影取决于输出事件类型，比如当前事件类型和过期事件类型。默认情况下，所有查询都生成当前事件，只有使用windows的查询在事件从窗口过期时才生成过期事件。您可以指定查询的输出是仅为当前事件、仅为过期事件还是同时为当前事件和过期事件。

==注意！==控制输出事件类型不会改变查询中的执行，也不会影响查询执行的准确性。以下关键字可与输出流一起使用以操作输出。

| Output event types | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| 当前事件           | 当传入事件到达以由查询处理时输出事件。当没有指定特定的输出事件类型时，这是默认值。 |
| 过期事件           | 当事件从窗口到期时输出事件。                                 |
| `all events`       | 当传入事件到达以由查询处理时输出事件当事件从窗口到期时。     |

可以在`insert`和`into`之间使用`output`事件类型关键字，如以下示例所示。

E.g 此查询将流中的所有事件延迟1分钟。

```
from TempStream#window.time(1 min)
select *
insert expired events into DelayedTempStream
```

##### 聚合函数

聚合函数在查询中执行聚合计算。当一个窗口被定义时，聚合被限制在该窗口中。如果没有提供窗口，则从Siddhi应用程序开始执行聚合。

**语法**

```
from <input stream>#window.<window name>(<parameter>, <parameter>, ... )
select <aggregate function>(<parameter>, <parameter>, ... ) as <attribute name>, <attribute2 name>, ...
insert into <output stream>;
```

**聚合参数**

聚合参数可以是属性，常量值，其他函数或聚合的结果，数学或逻辑表达式的结果或时间参数。查询中配置的聚合参数取决于被调用的聚合函数。

E.g 以下查询计算`TempStream`流的`temp`属性的平均值。此计算以滑动方式在最后10分钟完成，结果作为`avgTemp`输出到`AvgTempStream`输出流。

```
from TempStream#window.time(10 min)
select avg(temp) as avgTemp, roomNo, deviceID
insert into AvgTempStream;
```

以下是Siddhi附带的一些内置聚合函数，有关更多聚合函数，请参阅[执行扩展](https://wso2.github.io/siddhi/extensions/)。

- [avg](http://wso2.github.io/siddhi/api/latest/#avg-aggregate-function)
- [sum](http://wso2.github.io/siddhi/api/latest/#sum-aggregate-function)
- [max](http://wso2.github.io/siddhi/api/latest/#max-aggregate-function)
- [min](http://wso2.github.io/siddhi/api/latest/#min-aggregate-function)
- [count](http://wso2.github.io/siddhi/api/latest/#count-aggregate-function)
- [distinctCount](http://wso2.github.io/siddhi/api/latest/#distinctcount-aggregate-function)
- [maxForever](http://wso2.github.io/siddhi/api/latest/#maxforever-aggregate-function)
- [minForever](http://wso2.github.io/siddhi/api/latest/#minforever-aggregate-function)
- [stdDev](http://wso2.github.io/siddhi/api/latest/#stddev-aggregate-function)

##### Group By 分组

Group By允许您根据指定的属性对聚合进行分组。

**语法**

Group By聚合函数的语法如下：

```
from <input stream>#window.<window name>(...)
select <aggregate function>( <parameter>, <parameter>, ...) as <attribute1 name>, <attribute2 name>, ...
group by <attribute1 name>, <attribute2 name> ...
insert into <output stream>;
```

E.g 以下查询计算每个`roomNo`和`deviceID`组合的平均温度，用于在10分钟的滑动时间窗口到达`TempStream`流的事件。

```
from TempStream#window.time(10 min)
select avg(temp) as avgTemp, roomNo, deviceID
group by roomNo, deviceID
insert into AvgTempStream;
```

##### Having

允许您在处理select语句后使用`having`过滤事件。

**目的**

这允许您过滤聚合输出。

**语法**

Having子句的语法如下：

```
from <input stream>#window.<window name>( ... )
select <aggregate function>( <parameter>, <parameter>, ...) as <attribute1 name>, <attribute2 name>, ...
group by <attribute1 name>, <attribute2 name> ...
having <condition>
insert into <output stream>;
```

E.g 以下查询计算过去10分钟内每个房间的平均温度，并在超过30度时发出警报。

```
from TempStream#window.time(10 min)
select avg(temp) as avgTemp, roomNo
group by roomNo
having avgTemp > 30
insert into AlertStream;
```

##### Order By

Order By允许您根据指定的属性对聚合结果进行升序和/或降序排序。默认情况下，排序将按升序进行。用户可以使用`desc`关键字按降序排列。

**语法**

```
from <input stream>#window.<window name>( ... )
select <aggregate function>( <parameter>, <parameter>, ...) as <attribute1 name>, <attribute2 name>, ...
group by <attribute1 name>, <attribute2 name> ...
having <condition>
order by <attribute1 name> (asc | desc)?, <attribute2 name> (<ascend/descend>)?, ...
insert into <output stream>;
```

E.g 以下查询每10分钟计算每个`roomNo`和`deviceID`组合的平均温度，并通过按房间的`avgTemp`的升序排序它们，然后按`roomNo`的降序排序。

```
from TempStream#window.timeBatch(10 min)
select avg(temp) as avgTemp, roomNo, deviceID
group by roomNo, deviceID
order by avgTemp, roomNo desc
insert into AvgTempStream;
```

##### Limit & Offset

当事件作为批处理发出时，offset允许您偏移输出事件批处理的起始位置，而limit允许您从定义的偏移量限制批处理中的事件数量。有了这个，用户可以指定需要发出哪组事件。

**语法**

```
from <input stream>#window.<window name>( ... )
select <aggregate function>( <parameter>, <parameter>, ...) as <attribute1 name>, <attribute2 name>, ...
group by <attribute1 name>, <attribute2 name> ...
having <condition>
order by <attribute1 name> (asc | desc)?, <attribute2 name> (<ascend/descend>)?, ...
limit <positive interger>?
offset <positive interger>?
insert into <output stream>;
```

这里限制和偏移都是可选的，其中默认情况下，限制输出所有事件，默认情况下偏移设置为0。

E.g 以下查询计算每个`roomNo`和`deviceID`组合的平均温度，用于每10分钟到达`TempStream`流的事件，并发出两个具有最高平均温度的事件。

```
from TempStream#window.timeBatch(10 min)
select avg(temp) as avgTemp, roomNo, deviceID
group by roomNo, deviceID
order by avgTemp desc
limit 2
insert into HighestAvgTempStream;
```

以下查询计算每个`roomNo`和`deviceID`组合的平均温度，用于每10分钟到达`TempStream`流的事件，并根据其平均温度按降序排序时发出第三，第四和第五个事件。

```
from TempStream#window.timeBatch(10 min)
select avg(temp) as avgTemp, roomNo, deviceID
group by roomNo, deviceID
order by avgTemp desc
limit 3
offset 2
insert into HighestAvgTempStream;
```

##### Join (Stream)

join允许您根据指定的条件实时获取两个流的组合结果。

**目的**

流是无状态的。因此，为了连接两个流，它们需要连接到一个窗口，以便有一个可以用于连接的事件池。join还接受条件，以连接来自每个流的适当事件。在连接过程中，每个流的每个传入事件都根据给定的条件与另一个流窗口中的所有事件进行匹配，并为所有匹配的事件对生成输出事件。

> 连接也可以通过[存储数据](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#join-table)、[聚合](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#join-aggregation)或外部定义的[窗口](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#join-window)来执行。

**语法**

```
from <input stream>#window.<window name>(<parameter>, ... ) {unidirectional} {as <reference>}
         join <input stream>#window.<window name>(<parameter>,  ... ) {unidirectional} {as <reference>}
    on <join condition>
select <attribute name>, <attribute name>, ...
insert into <output stream>
```

这里，<join condition>允许您匹配两个流的属性。

**单向连接操作**

默认情况下，到达任何一个流的事件都可能触发连接进程。但是，如果您想控制连接执行，您可以像语法中描述的那样，在连接定义中的流旁边添加`unidirectional`关键字，以便使流能够触发连接操作。在这里，到达其他流的事件只会更新该流的窗口，而该流不会触发连接操作。

> 单向关键字`unidirectional `不能同时应用于两个输入流，因为默认行为已经允许两个流触发连接操作。

E.g 假设调节器的温度每分钟更新一次。以下是Siddhi应用程序，如果房间温度超过30度的所有房间尚未开启温度调节器，则可以控制温度调节器。

```
define stream TempStream(deviceID long, roomNo int, temp double);
define stream RegulatorStream(deviceID long, roomNo int, isOn bool);

from TempStream[temp > 30.0]#window.time(1 min) as T
  join RegulatorStream[isOn == false]#window.length(1) as R
  on T.roomNo == R.roomNo
select T.roomNo, R.deviceID, 'start' as action
insert into RegulatorActionStream;
```

**支持的连接类型**

以下是join子句支持的操作。

* Inner join (join)：这是连接操作的默认行为。join用作连接两个流的关键字。只有当两个流中都有匹配的事件时，才会生成输出。

* Left outer join：左外连接操作允许您根据条件连接两个要合并的流。`left outer join`用作连接两个流的关键字。在这里，它通过为右流的属性设置null值返回所有左流的事件，即使右流中没有匹配的事件。

  E.g 以下查询为`StockStream`流中的所有事件生成输出事件，而不管`TwitterStream`流中是否存在匹配的符号。

  ```
  from StockStream#window.time(1 min) as S
    left outer join TwitterStream#window.length(1) as T
    on S.symbol== T.symbol
  select S.symbol as symbol, T.tweet, S.price
  insert into outputStream ;   
  ```

* Right outer join：这类似于左外连接。右外部连接用作连接两个流的关键字。它返回右边流的所有事件，即使左边流中没有匹配的事件。

* Full outer join：完整的外部连接结合了左外部连接和右外部连接的结果。`完全外部连接`用作两个流的连接的关键字。在这里，为每个传入事件生成输出事件，即使另一个流中没有匹配的事件。

  E.g 以下查询为每个流的所有传入事件生成输出事件，而不管其他流中的符号属性是否匹配。

  ```
  from StockStream#window.time(1 min) as S
    full outer join TwitterStream#window.length(1) as T
    on S.symbol== T.symbol
  select S.symbol as symbol, T.tweet, S.price
  insert into outputStream ;    
  ```

##### Pattern

这是一个状态机实现，允许您检测随时间而来的事件中的模式。这可以关联单个流或多个流之间的事件。

**目的**

模式允许您识别一段时间内事件的趋势。

**语法**

```
from (every)? <event reference>=<input stream>[<filter condition>] -> 
    (every)? <event reference>=<input stream [<filter condition>] -> 
    ... 
    (within <time gap>)?     
select <event reference>.<attribute name>, <event reference>.<attribute name>, ...
insert into <output stream>
```

| Items                  | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `->`                   | 这是用来指示应该跟随另一个事件的事件。后续事件不一定必须在前一个事件之后立即发生。前一个事件要满足的条件应该在符号之前添加，后一个事件要满足的条件应该在符号之后添加。 |
| `<event reference>`    | 这允许您添加对匹配事件的引用，以便以后可以访问它以进行进一步处理。 |
| `(within <time gap>)?` | within子句是可选的。它定义了所有匹配事件应发生的持续时间。   |
| `every`                | `every`是一个可选的关键字。这定义了是否应该为具有匹配条件的指定流中的每个事件到达触发事件匹配。如果未使用此关键字，则仅执行一次匹配。 |

Siddhi还支持模式匹配与计数事件和匹配事件的逻辑顺序，如 (`and`, `or`, and `not`).。这些将在本指南的下面进一步详细介绍。

E.g 如果房间温度在10分钟内增加5度，此查询将发送警报。

```
from every( e1=TempStream ) -> e2=TempStream[ e1.roomNo == roomNo and (e1.temp + 5) <= temp ]
    within 10 min
select e1.roomNo, e1.temp as initialTemp, e2.temp as finalTemp
insert into AlertStream;
```

在这里，匹配过程开始于TempStream流中的每个事件(因为e1=TempStream使用的都是each)，如果在10分钟内有另一个事件到达，其temp属性的值大于或等于e1。事件e1的temp + 5，通过AlertStream生成一个输出。

###### 计算模式

计数模式允许您匹配可能已针对相同匹配条件接收的多个事件。每个条件匹配的事件数可以通过条件后缀来限制。

**语法**

每个匹配条件都可以包含一组事件，其中包含要匹配的最小和最大事件数，如下面的语法所示。

```
from (every)? <event reference>=<input stream>[<filter condition>] (<<min count>:<max count>>)? ->  
    ... 
    (within <time gap>)?     
select <event reference>([event index])?.<attribute name>, ...
insert into <output stream>
```

| Postfix   | Description                            | Example                          |
| --------- | -------------------------------------- | -------------------------------- |
| `<n1:n2>` | 这将匹配n1到n2事件(包括n1且不超过n2)。 | `1:4` matches 1 to 4 events.     |
| `<n:>`    | 这匹配n个或更多事件（包括n）。         | `<2:>` matches 2 or more events. |
| `<:n>`    | 这最多匹配n个事件（不包括n）。         | `<:5>` matches up to 5 events.   |
| `<n>`     | 这恰好与n个事件匹配。                  | `<5>` matches exactly 5 events.  |

可以使用带有引用的事件索引来检索集合中事件的特定发生。方括号可以用来表示事件索引，其中1可以用作第一个事件的索引，最后一个可以用作事件集合中最后可用事件的索引。如果您提供的索引大于最后一个事件索引，系统将返回null。以下是一些有效的例子。

- `e1[3]`是指第3次事件。
- `e1[last]` 最后一次事件
- `e1[last - 1]` 指最后一个事件之前的事件。

E.g 以下Siddhi应用程序计算两个调节器事件之间的温差。

```
define stream TempStream (deviceID long, roomNo int, temp double);
define stream RegulatorStream (deviceID long, roomNo int, tempSet double, isOn bool);

from every( e1=RegulatorStream) -> e2=TempStream[e1.roomNo==roomNo]<1:> -> e3=RegulatorStream[e1.roomNo==roomNo]
select e1.roomNo, e2[0].temp - e2[last].temp as tempDiff
insert into TempDiffStream;
```

###### 逻辑模式

逻辑模式匹配以时间顺序到达的事件，并将它们与诸如and、or和not之类的逻辑关系关联起来。

**语法**

```
from (every)? (not)? <event reference>=<input stream>[<filter condition>] 
          ((and|or) <event reference>=<input stream>[<filter condition>])? (within <time gap>)? ->  
    ... 
select <event reference>([event index])?.<attribute name>, ...
insert into <output stream>
```

诸如and、or或not这样的关键字可以用来说明逻辑关系。

| Key Word                            | Description                                                  |
| ----------------------------------- | ------------------------------------------------------------ |
| `and`                               | 这允许任意顺序的两个事件的条件和匹配条件。                   |
| `or`                                | The state succeeds if either condition of `or` is satisfied. Here the event reference of the other condition is `null`. |
| `not <condition1> and <condition2>` | When `not` is included with `and`, it identifies the events that match arriving before any event that match . |
| `not <condition> for <time period>` | When `not` is included with `for`, it allows you to identify a situation where no event that matches `<condition1>` arrives during the specified `<time period>`. e.g.,`from not TemperatureStream[temp > 60] for 5 sec`. |

在这里，可以在not模式后面加上and子句或在给定的<time period>之后得出not的有效周期。此外，在Siddhi中，超过两种流不能使用and, or或not子句与逻辑条件匹配。

E.g 在Siddhi App之后，当钥匙从酒店房间移除时，将停止控制动作发送给调节器。

```
define stream RegulatorStateChangeStream(deviceID long, roomNo int, tempSet double, action string);
define stream RoomKeyStream(deviceID long, roomNo int, action string);


from every( e1=RegulatorStateChangeStream[ action == 'on' ] ) -> 
      e2=RoomKeyStream[ e1.roomNo == roomNo and action == 'removed' ] or e3=RegulatorStateChangeStream[ e1.roomNo == roomNo and action == 'off']
select e1.roomNo, ifThenElse( e2 is null, 'none', 'stop' ) as action
having action != 'none'
insert into RegulatorActionStream;
```

如果我们在温度达到12度之前关闭调节器，这个Siddhi应用程序会发出警报。

```
define stream RegulatorStateChangeStream(deviceID long, roomNo int, tempSet double, action string);
define stream TempStream (deviceID long, roomNo int, temp double);

from e1=RegulatorStateChangeStream[action == 'start'] -> not TempStream[e1.roomNo == roomNo and temp < 12] and e2=RegulatorStateChangeStream[action == 'off']
select e1.roomNo as roomNo
insert into AlertStream;
```

如果在打开调节器的5分钟内温度没有降低到12度，该Siddhi应用程序会发出警报。

```
define stream RegulatorStateChangeStream(deviceID long, roomNo int, tempSet double, action string);
define stream TempStream (deviceID long, roomNo int, temp double);

from e1=RegulatorStateChangeStream[action == 'start'] -> not TempStream[e1.roomNo == roomNo and temp < 12] for '5 min'
select e1.roomNo as roomNo
insert into AlertStream;
```



##### Sequence

Sequence是一种状态机实现，允许您随时检测事件发生的顺序。这里所有匹配事件需要连续到达以匹配序列条件，并且不存在任何到达匹配事件序列内的非匹配事件。这可以关联单个流内或多个流之间的事件。

**目的**

这允许您在指定的时间段内检测指定的事件序列。

**语法**

```
from (every)? <event reference>=<input stream>[<filter condition>], 
    <event reference>=<input stream [<filter condition>], 
    ... 
    (within <time gap>)?     
select <event reference>.<attribute name>, <event reference>.<attribute name>, ...
insert into <output stream>
```

| Items                  | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `,`                    | 这表示紧接着的下一个事件，即，当与第一个条件匹配的事件到达时，紧接在其之后到达的事件应该与第二个条件匹配。 |
| `<event reference>`    | 这允许您添加对匹配事件的引用，以便以后可以访问它以进行进一步处理。 |
| `(within <time gap>)?` | within子句是可选的。它定义了所有匹配事件应发生的持续时间。   |
| `every`                | `every`是一个可选的关键字。这定义了是否应该为到达具有匹配条件的指定流的每个事件触发匹配事件。如果未使用此关键字，则仅执行一次匹配。 |

E.g 如果两个连续温度事件之间的温度升高超过一度，则该查询生成警报。

```
from every e1=TempStream, e2=TempStream[e1.temp + 1 < temp]
select e1.temp as initialTemp, e2.temp as finalTemp
insert into AlertStream;
```

######计数序列

计数序列允许您在相同的匹配条件下匹配多个事件。每个条件匹配的事件数量可以通过条件后缀(如计数模式)来限制，或者使用*、+和?操作符。还可以使用事件索引检索匹配事件，类似于在计数中所做的工作。

**语法**

序列中的每个匹配条件都可以包含一系列事件，如下所示。

```
from (every)? <event reference>=<input stream>[<filter condition>](+|*|?)?, 
    <event reference>=<input stream [<filter condition>](+|*|?)?, 
    ... 
    (within <time gap>)?     
select <event reference>.<attribute name>, <event reference>.<attribute name>, ...
insert into <output stream>
```

| 后缀符号 | 必选/可选 | 描述                               |
| -------- | --------- | ---------------------------------- |
| `+`      | 可选的    | 这将一个或多个事件与给定条件匹配。 |
| `*`      | 可选的    | 这将零个或多个事件与给定条件匹配。 |
| `?`      | 可选的    | 这将零或一个事件与给定条件匹配。   |

E.g siddhi应用程序识别温度峰值。

```
define stream TempStream(deviceID long, roomNo int, temp double);

from every e1=TempStream, e2=TempStream[e1.temp <= temp]+, e3=TempStream[e2[last].temp > temp]
select e1.temp as initialTemp, e2[last].temp as peakTemp
insert into PeekTempStream;
```

###### 逻辑序列

逻辑序列使用`and`,`or`,`not`连续到达事件来标识逻辑关系。

**语法**

逻辑序列的语法如下:

```
from (every)? (not)? <event reference>=<input stream>[<filter condition>] 
          ((and|or) <event reference>=<input stream>[<filter condition>])? (within <time gap>)?, 
    ... 
select <event reference>([event index])?.<attribute name>, ...
insert into <output stream>
```

像and、or或not这样的关键字可以用来说明逻辑关系，类似于在逻辑模式中是如何完成的。

E.g 当温度和湿度事件紧接着调节器事件时，该Siddhi应用程序会通知状态。

```
define stream TempStream(deviceID long, temp double);
define stream HumidStream(deviceID long, humid double);
define stream RegulatorStream(deviceID long, isOn bool);

from every e1=RegulatorStream, e2=TempStream and e3=HumidStream
select e2.temp, e3.humid
insert into StateNotificationStream;
```

##### 限制输入速率

输出速率限制允许查询根据指定的条件定期输出事件。

**目的**

这允许您限制输出以避免后续执行过载，并删除不必要的信息。

**语法**

输出速率限制配置的语法如下：

```
from <input stream> ...
select <attribute name>, <attribute name>, ...
output <rate limiting configuration>
insert into <output stream>
```

Siddhi支持三种输出速率限制配置，如下表所述：

| 限速配置       | 语法                                           | 描述                                                         |
| -------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| 根据时间       | `<output event> every <time interval>`         | 每个<time interval> 输出<output event>事件                   |
| 根据事件的数量 | `<output event> every <event interval> events` | 每`<event interval>` 个事件，输出`<output event>`。          |
| 基于快照的输出 | `snapshot every <time interval>`               | 这将为每个给定的<time interval>输出窗口中的所有事件(如果查询中没有定义窗口，则输出最后一个事件)。 |

在这里，<output event>指定应该作为查询的输出返回的事件。可能的值如下:`first`:只发出查询在指定时间间隔/滑动窗口中处理的第一个事件。`last`:只发出查询在指定时间间隔/滑动窗口中处理的最后一个事件。* `all`:在指定的时间间隔/滑动窗口内，查询处理的所有事件都会被发出。如果没有定义<output事件>，则默认使用all。

E.g

* 根据事件数返回事件

  这里，每当指定数量的事件到达时，就会发出事件。您还可以指定是仅发出第一个事件/最后一个事件，还是仅发出已到达事件的所有事件。在此示例中，每10个事件发出每个传感器的最后温度。

  ```
  from TempStreamselect 
  select temp, deviceID
  group by deviceID
  output last every 10 events
  insert into LowRateTempStream;    
  ```

* 根据时间返回事件

  这里每隔预定义的时间间隔发出事件。您还可以指定是否仅发出在指定时间间隔内到达的事件中的第一个事件，最后一个事件或所有事件。在此示例中，每10秒发出一次所有温度事件.

  ```
  from TempStreamoutput 
  output every 10 sec
  insert into LowRateTempStream;    
  ```

* 返回事件的定期快照

  这种方法最适合Windows。当输入流连接到窗口时，快照速率限制会发出所有已到达的当前事件，并且每个预定义的时间间隔都没有相应的过期事件。如果输入流未连接到窗口，则仅发出每个预定义时间间隔的最后一个当前事件。此查询在每1秒5秒的时间窗口中发出事件的快照。

  ```
  from TempStream#window.time(5 sec)
  output snapshot every 1 sec
  insert into SnapshotTempStream;    
  ```

#### Partition 分区

分区将流和查询分成独立的组，以便并行和孤立地处理它们。分区可以包含一个或多个查询，并且可以有多个实例，其中为每个分区复制相同的查询和流。每个分区都标有分区键。这些分区仅处理与相应分区键匹配的事件。

**目的**

分区允许您单独处理事件组，以便可以使用每组的同一组查询执行事件处理。

***生产分区键值***

可以使用以下两种方法生成分区键：

* 按值划分

  这是通过使用输入流属性生成唯一值来创建的。

  ***语法***

  ```
  partition with ( <expression> of <stream name>, <expression> of <stream name>, ... )
  begin
      <query>
      <query>
      ...
  end; 
  ```

  E.g 此查询计算每个`deviceID`最近10个事件中记录的最高温度。

  ```
  partition with ( deviceID of TempStream )
  begin
      from TempStream#window.length(10)
      select roomNo, deviceID, max(temp) as maxTemp
      insert into DeviceTempStream;
  end;
  ```

* 按范围划分

  这是通过将每个分区键映射到输入流数字属性的范围条件来创建的。

  ***语法***

  ```
  partition with ( <condition> as <partition key> or <condition> as <partition key> or ... of <stream name>, ... )
  begin
      <query>
      <query>
      ...
  end;
  ```

   E.g 此查询计算每个办公区域最后10分钟的平均温度。

  ```
  partition with ( roomNo >= 1030 as 'serverRoom' or 
                   roomNo < 1030 and roomNo >= 330 as 'officeRoom' or 
                   roomNo < 330 as 'lobby' of TempStream)
  begin
      from TempStream#window.time(10 min)
      select roomNo, deviceID, avg(temp) as avgTemp
      insert into AreaTempStream
  end;
  ```

##### Inner Stream

分区块内的查询可以使用内部流相互通信，同时保留分区隔离。内部流由放置在流名称之前的“＃”表示，并且这些流不能在分区块之外访问。

**目的**

内部流允许您连接分区块中的查询，以便查询的输出只能被同一分区中的另一个查询用作输入。因此，如果流在分区内进行通信，则无需对流进行重新分区。

E.g 此分区计算每个传感器的每10个事件的平均温度，如果连续的平均温度值增加超过5度，则将输出发送到`DeviceTempIncreasingStream`流。

```
partition with ( deviceID of TempStream )
begin
    from TempStream#window.lengthBatch(10)
    select roomNo, deviceID, avg(temp) as avgTemp
    insert into #AvgTempStream

    from every (e1=#AvgTempStream),e2=#AvgTempStream[e1.avgTemp + 5 < avgTemp]
    select e1.deviceID, e1.avgTemp as initialAvgTemp, e2.avgTemp as finalAvgTemp
    insert into DeviceTempIncreasingStream
end;
```

####Table

表是流或事件表的存储版本。它的模式是通过类似于流定义的表定义来定义的。这些事件默认存储在内存中，但是Siddhi还提供了存储扩展，用于通过表抽象处理存储在各种数据存储中的数据/事件。

**目的**

表格允许Siddhi使用存储事件。通过为表定义模式，Siddhi允许使用其定义的属性和流数据进行查询。您还可以交互式地查询表中存储事件的状态。

**语法**

新表定义的语法如下：

```
define table <table name> (<attribute name> <attribute type>, <attribute name> <attribute type>, ... );
```

在表定义中配置以下参数：

| Parameter        | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `table name`     | The name of the table defined. (`PascalCase` is used for table name as a convention.) |
| `attribute name` | The schema of the table is defined by its attributes with uniquely identifiable attribute names (`camelCase`is used for attribute names as a convention.) |
| `attribute type` | The type of each attribute defined in the schema.  This can be `STRING`, `INT`, `LONG`, `DOUBLE`, `FLOAT`, `BOOL` or `OBJECT`. |

E.g 下面定义了一个名为RoomTypeTable的表，其中包含roomNo和数据类型为int和string的类型属性。

```
define table RoomTypeTable ( roomNo int, type string );
```

**主键**

表可以配置主键以避免数据重复。通过将`@PrimaryKey('key1'， 'key2')`注释包含到表定义中来配置主键。每个事件表配置只能有一个`@PrimaryKey`注释。根据表的实现，支持的属性数量不同。当主键使用多个属性时，存储在表中的事件的唯一性将根据这些属性的值的组合来确定。

E.g 此查询创建一个事件表，其中`symbol`属性作为主键。因此，此表中的每个条目都必须具有`symbol`属性的唯一值。

```
@PrimaryKey('symbol')
define table StockTable (symbol string, price float, volume long);
```

#####Indexes 索引

索引允许更快地搜索/修改表。通过将`@Index('key1'， 'key2')`注释包含到表定义中来配置索引。每个事件表配置可以有0-1 `@Index`注释。`对@Index`注释的支持和支持的属性数量根据表实现的不同而不同。当多个属性用于索引时，每个属性都用于索引表以快速访问数据。索引可以与主键一起配置。

E.g 此查询创建一个名为`RoomTypeTable`的索引事件表，其`roomNo`属性为索引键。

```
@Index('roomNo')
define table RoomTypeTable (roomNo int, type string);
```

#####操作符

以下操作符可以在表上执行。

###### Insert

这允许将事件插入表中。这类似于将事件插入流中。

> 如果表是用主键定义的，并且插入重复数据，则可能发生主键约束违反。在这种情况下，使用更新或插入操作。

**语法**

```
from <input stream> 
select <attribute name>, <attribute name>, ...
insert into <table>
```

与流类似，为了只插入特定的输出事件类型，需要在`insert`和`into `keywords之间使用当前事件、过期事件或all events关键字。有关更多信息，请参见[输出事件类型](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#output-event-types).

E.g 此查询将TempStream流中的所有事件插入TempTable表。

```
from TempStream
select *
insert into TempTable;
```

###### Join (Table)

这允许流以流方式从表中检索信息。

> Joins也可以使用两个流，聚合或对外部定义的窗口执行。

 **语法**

```
from <input stream> join <table>
    on <condition>
select (<input stream>|<table>).<attribute name>, (<input stream>|<table>).<attribute name>, ...
insert into <output stream>
```

> 表只能与流联合。两个表不能联合，因为必须至少有一个活动实体才能触发连接操作。

E.g 这个Siddhi应用程序执行一个连接，根据房间号从`RoomTypeTable`表中检索房间类型，因此它可以过滤与服务器房间相关的事件。

```
define table RoomTypeTable (roomNo int, type string);
define stream TempStream (deviceID long, roomNo int, temp double);

from TempStream join RoomTypeTable
    on RoomTypeTable.roomNo == TempStream.roomNo
select deviceID, RoomTypeTable.type as roomType, type, temp
    having roomType == 'server-room'
insert into ServerRoomTempStream;
```

###### Delete

删除存储在表中的选定事件。

**语法**

```
from <input stream> 
select <attribute name>, <attribute name>, ...
delete <table> (for <output event type>)?
    on <condition>
```

条件元素指定要删除的事件的基础。在指定条件时，应该使用表名引用表属性。要对特定的输出事件类型执行delete，使用当前事件、过期事件或句法中显示的all events关键字for。有关更多信息，请参见输出事件类型。

> 必须始终使用表名称引用表属性，如下所示：<table name>。<attibute name>

E.g 在此示例中，如果`RoomNo`属性的值与`DeleteStream`流中事件的`roomNumber`属性值匹配，则脚本将删除`RoomTypeTable`表中的记录。

```
define table RoomTypeTable (roomNo int, type string);

define stream DeleteStream (roomNumber int);

from DeleteStream
delete RoomTypeTable
    on RoomTypeTable.roomNo == roomNumber;
```

###### Update

此运算符根据条件更新存储在表中的选定事件属性。

**语法**

```
from <input stream> 
select <attribute name>, <attribute name>, ...
update <table> (for <output event type>)? 
    set <table>.<attribute name> = (<attribute name>|<expression>)?, <table>.<attribute name> = (<attribute name>|<expression>)?, ...
    on <condition>
```

条件元素指定要更新的事件的基础。在指定条件时，必须使用表名引用表属性。您可以使用set关键字从表中更新选定的属性。在这里，对于每个赋值，左边指定的属性必须是表属性，右边指定的属性可以是流/表属性、数学运算或其他。如果没有提供set子句，则更新表中的所有属性。要执行特定输出事件类型的更新，请使用当前事件、过期事件或all events关键字for，如语法中所示。有关更多信息，请参见[输出事件类型](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#output-event-types)。

> 必须始终使用表名称引用表属性，如下所示：<table name>。<attibute name>。

E.g 此Siddhi应用程序根据`UpdateStream`流中的新到达和退出，更新`RoomOccupancyTable`表中每个房间号的房间占用率。

```
define table RoomOccupancyTable (roomNo int, people int);
define stream UpdateStream (roomNumber int, arrival int, exit int);

from UpdateStream
select *
update RoomOccupancyTable
    set RoomOccupancyTable.people = RoomOccupancyTable.people + arrival - exit
    on RoomOccupancyTable.roomNo == roomNumber;
```

###### Update or Insert

这允许您根据条件更新表中是否已存在事件属性，或者将条目作为新属性插入。

**语法**

```
from <input stream> 
select <attribute name>, <attribute name>, ...
update or insert into <table> (for <output event type>)? 
    set <table>.<attribute name> = <expression>, <table>.<attribute name> = <expression>, ...
    on <condition>
```

条件元素指定选择哪些事件进行更新。在指定条件时，应该使用表名引用表属性。如果表中不存在与条件匹配的记录，则将到达的事件插入表中。set子句仅在插入/更新操作期间执行更新时使用。当使用set子句时，左边的属性总是表属性，右边的属性可以是流/表属性、数学运算或其他。左边的属性(例如如果满足给定条件，则事件表中的属性)将被更新为右侧的属性值。如果没有提供set子句，则更新表中的所有属性。

> 当右侧的属性是表属性时，支持的操作因数据库类型而异。

要执行特定输出事件类型的更新，请使用当前事件、过期事件或all events关键字for，如语法中所示。要了解更多信息，请参见输出事件类型。

> 表属性应始终引用，表名为<table name>。<attribute name>。

E.g 可更新事件表中具有与`UpdateStream`流中相同房间号的事件的查询更新如下。当在事件表中找到这些事件时，就会更新它们。当在事件表中没有找到流中可用的房间号时，它将从流中插入。

```
define table RoomAssigneeTable (roomNo int, type string, assignee string);
define stream RoomAssigneeStream (roomNumber int, type string, assignee string);

from RoomAssigneeStream
select roomNumber as roomNo, type, assignee
update or insert into RoomAssigneeTable
    set RoomAssigneeTable.assignee = assignee
    on RoomAssigneeTable.roomNo == roomNo;
```

###### In

这允许流检查表中是否存在期望值作为条件操作的一部分。

**语法**

```
from <input stream>[<condition> in <table>]
select <attribute name>, <attribute name>, ...
insert into <output stream>
```

条件元素指定要比较的事件的选择基础。在构造条件时，必须始终使用表名引用表属性，如下所示:<table>。< attibute名称>。

E.g 此Siddhi应用程序仅过滤`ServerRoomTable`表中列出的房间号。

```
define table ServerRoomTable (roomNo int);
define stream TempStream (deviceID long, roomNo int, temp double);

from TempStream[ServerRoomTable.roomNo == roomNo in ServerRoomTable]
insert into ServerRoomTempStream;
```

####增量聚合

增量聚合允许您以增量的方式获取特定时间段的聚合。这不仅允许您计算具有不同时间粒度的聚合，还允许您以交互方式访问它们，以用于报告、仪表板和进一步处理。它的模式是通过聚合定义定义的。增量聚合粒度数据持有者每15分钟自动清除一次。在执行数据清除时，将考虑在增量聚合查询中为每个粒度指定的保留时间。粒度定义的保留期需要大于或等于下表中指定的最小保留期。如果没有为粒度定义有效的保留期，则应用默认的保留期(如下表所示)。

| 粒度     | 默认保留      | 最低保留      |
| -------- | ------------- | ------------- |
| `second` | `120` seconds | `120` seconds |
| `minute` | `24` hours    | `120` minutes |
| `hour`   | `30` days     | `25` hours    |
| `day`    | `1` year      | `32` days     |
| `month`  | `All`         | `13` month    |
| `year`   | `All`         | `none`        |

**目的**

增量聚合允许您检索不同时间长度的聚合值。也就是说，它允许您获得诸如sum、count、avg、min、max、count和distinctCount之类的聚合，这些聚合用于持续时间(如sec、min、hour等)的流属性。这在许多分析场景中非常重要，因为聚合值通常需要几个时间段。此外，这确保聚合不会因为意外的系统故障而丢失，因为聚合可以存储在不同的持久性存储中。

**语法**

```
@store(type="<store type>", ...)
@purge(enable="<true or false>",interval=<purging interval>,@retentionPeriod(<granularity> = <retention period>, ...) )
define aggregation <aggregator name>
from <input stream>
select <attribute name>, <aggregate function>(<attribute name>) as <attribute name>, ...
    group by <attribute name>
    aggregate by <timestamp attribute> every <time periods> ;
```

以上语法包括以下内容：

| Item                           | Description                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| `@BufferSize`                  | **DEPRECIATED FROM V4.2.0**. 这标识了按顺序保留在缓冲区中的过期事件数处理乱序事件处理。这是可选的仅当聚合基于外部时才适用的参数时间戳（因为事件聚集基于事件到达时间不能无序）。Siddhi确定事件是否过期基于最新事件的时间戳和最精细的持续时间计算哪个聚合。例如，如果聚合计算为sec ... year，则最精细的持续时间是秒。因此，如果缓冲区大小为3且事件在第51,52,53和54秒期间到达，则所有较旧的聚合（即，第51,52和53秒）将保留在缓冲区中，因为最新事件在第54次到达第二。默认值为0。 |
| `@IgnoreEventsOlderThanBuffer` | **DEPRECIATED FROM V4.2.0**.此注释指定是否聚合早于的事件缓冲。如果此参数设置为false（默认值），则为任何事件比缓冲区更早的值与缓冲区中最旧的事件聚合在一起。如果此参数设置为true，删除任何早于缓冲区的事件。这是一个可选的注释。 |
| `@store`                       | 此注释用于指代计算所在的数据存储汇总结果存储。此注释是可选的。什么时候没有提供注释，数据存储在内存存储中。 |
| `@purge`                       | 此批注用于配置聚合粒度中的清除。如果未提供此注释，则应用上述默认清除。如果要禁用自动数据清除，可以使用此批注，如下所示：“@purge（enable=false）/如果Siddhi应用程序中包含的聚合查询仅用于只读目的，则应禁用数据清除。 |
| `@retentionPeriod`             | 此注释用于指定执行数据清除时数据需要保留的时间长度。如果未提供此批注，则应用默认保留期。 |
| `<aggregator name>`            | 这指定了聚合的唯一名称，以便可以引用它访问聚合结果时。       |
| `<input stream>`               | 提供聚合的流。**注意！这个流应该是已定义。**                 |
| `group by <attribute name>`    | group by子句是可选的。如果它包含在Siddhi应用程序中，则汇总值按属性按每组计算。如果不使用，全部事件汇总在一起。 |
| `by <timestamp attribute>`     | 这个条款是可选的。这定义了应该用作的属性时间戳。如果不使用此子句，则默认使用事件时间。时间戳可以作为字符串或长值给出。如果它是一个长值，unix时间戳(以毫秒为单位)是预期的(例如1496289950000)。如果它是一个字符串值，支持的格式是<yyyy>-<MM>-<dd> <HH>:< MM>:<ss>(如果时间是GMT时间)和< yyyy > - < MM > < dd > < HH >:< MM >:<ss> < Z >(如果不是GMT), here the ISO 8601 UTC offset must be provided for `<Z>` . |
| (e.g., `+05:30`, `-11:00`).    |                                                              |
| `<time periods>`               | 时间段可以作为由三个点分隔的范围给出，或者以逗号分隔的值给出。范围将以秒...年为单位，其中聚合将按秒，分钟，小时，日，月和年进行。逗号分隔值可以以min，hour给出。但是，对于逗号分隔值，尚不支持跳过持续时间（例如，min，day不是有效子句，因为已跳过小时持续时间） |

> 从V4.2.0开始，对于具有GMT时区的每个粒度，在日历开始时间执行聚合

> 从V4.2.6开始，可以在多个Siddhi应用程序中定义相同的聚合以进行加入，但是，只有一个siddhi应用程序应该执行处理（即聚合输入流应该仅将事件提供给一个聚合定义）。

E.g 此Siddhi应用程序定义了名为`TradeAggregation`的聚合，以计算到达`TradeStream`流的事件的`price`属性的平均值和总和。这些聚合是按照第二年范围内的每个时间粒度计算的。

```
define stream TradeStream (symbol string, price double, volume long, timestamp long);

@purge(enable='true', interval='10 sec',@retentionPeriod(sec='120 sec',min='24 hours',hours='30 days',days='1 year',months='all',years='all'))
define aggregation TradeAggregation
  from TradeStream
  select symbol, avg(price) as avgPrice, sum(price) as total
    group by symbol
    aggregate by timestamp every sec ... year;
```

##### Join (Aggregation)

这允许流从聚合中检索计算的聚合值。

> 也可以使用两个流，一个表和一个流，或者一个流来对外部定义的窗口执行连接。

**语法**

连接与聚合类似于连接与表，但附加在子句内部和每个子句中。

```
from <input stream> join <aggrigation> 
  on <join condition> 
  within <time range> 
  per <time granularity>
select <attribute name>, <attribute name>, ...
insert into <output stream>;
```

除了表连接的构造外，还包括以下内容。请注意，“`on`”条件是可选的:

| Item                     | Description                                                  |
| ------------------------ | ------------------------------------------------------------ |
| `within <time range>`    | 这允许您指定需要检索聚合值的时间间隔。这可以通过将逗号分隔的开始和结束时间作为字符串或长值或使用指定数据范围的通配符字符串来指定。详情请参阅示例。 |
| `per <time granularity>` | 这指定了必须对聚合值进行分组和返回的时间粒度。例如，如果指定天数，则会在选定的时间间隔内为检索到的聚合值进行分组。 |

`within`和`par`子句也接受来自流的属性值。

> 可以通过AGG_TIMESTAMP属性访问聚合的时间戳。

E.g 以下聚合定义将用于示例。

```
define stream TradeStream (symbol string, price double, volume long, timestamp long);

define aggregation TradeAggregation
  from TradeStream
  select symbol, avg(price) as avgPrice, sum(price) as total
    group by symbol
    aggregate by timestamp every sec ... year;
```

此查询检索“2014-02-15 00:00:00 +05:30”、“2014-03-16 00:00:00 +05:30”(请注意，如果时区是GMT，可以省略+05:30)范围内的每日聚合。

```
define stream StockStream (symbol string, value int);

from StockStream as S join TradeAggregation as T
  on S.symbol == T.symbol 
  within "2014-02-15 00:00:00 +05:30", "2014-03-16 00:00:00 +05:30" 
  per "days" 
select S.symbol, T.total, T.avgPrice 
insert into AggregateStockStream;
```

此查询在2014-02-15之内检索每小时聚合。

```
define stream StockStream (symbol string, value int);

from StockStream as S join TradeAggregation as T
  on S.symbol == T.symbol 
  within "2014-02-15 **:**:** +05:30"
  per "hours" 
select S.symbol, T.total, T.avgPrice 
insert into AggregateStockStream;
```

此查询在时间戳1496200000000和1596434876000之间的时间段内检索每`perValue`流属性的所有聚合。

```
define stream StockStream (symbol string, value int, perValue string);

from StockStream as S join TradeAggregation as T
  on S.symbol == T.symbol 
  within 1496200000000L, 1596434876000L
  per S.perValue
select S.symbol, T.total, T.avgPrice 
insert into AggregateStockStream;
```

#### *(Defined)* Window

定义的窗口是可以跨多个查询共享的窗口。事件可以从一个或多个查询插入到定义的窗口中，并且可以根据定义的窗口类型生成输出事件。

**语法**

```
define window <window name> (<attribute name> <attribute type>, <attribute name> <attribute type>, ... ) <window type>(<parameter>, <parameter>, …) <output event type>;
```

在表定义中配置以下参数：

| Parameter                         | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| `window name`                     | 定义的窗口名称。（PascalCase用于窗口名称作为约定。）         |
| `attribute name`                  | 窗口的模式由其属性定义，具有唯一可识别的属性名称（camelCase用于属性名称作为约定。） |
| `attribute type`                  | 模式中定义的每个属性的类型。这可以是`STRING`，`INT`，`LONG`，`DOUBLE`，`FLOAT`，`BOOL`或`OBJECT`。 |
| `<window type>(<parameter>, ...)` | 与窗口及其参数关联的窗口类型。                               |
| `output <output event type>`      | 这是可选的。诸如当前事件，过期事件和所有事件（默认值）之类的关键字可用于指定何时应该公开窗口输出。有关更多信息，请参阅[输出事件类型](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#output-event-types)。 |

E.g

* 当事件到达时以及事件从窗口到期时返回所有输出。在此查询中，未指定输出事件类型。因此，它返回当前和过期事件作为输出。

  ```
    define window SensorWindow (name string, value float, roomNo int, deviceID string) timeBatch(1 second);
  ```

* 仅当事件从窗口到期时才返回输出。在此查询中，窗口的输出事件类型是过期事件。因此，它仅返回从窗口过期的事件作为输出。

  ```
    define window SensorWindow (name string, value float, roomNo int, deviceID string) timeBatch(1 second) output expired events;
  ```

**已定义窗口上的操作符**

可以在定义的窗口上执行以下运算符。

##### Insert

这允许将事件插入到窗口中。这类似于将事件插入流中。

**syntax**

```
from <input stream> 
select <attribute name>, <attribute name>, ...
insert into <window>
```

要仅插入特定输出事件类型的事件，请在insert和into keywords之间添加`current events`、`expired events`或`all events`关键字(类似于对流执行的方式)。有关更多信息，请参见[输出事件类型](https://wso2.github.io/siddhi/documentation/siddhi-4.0/#output-event-types)。

E.g 此查询将`TempStream`流中的所有事件插入`OneMinTempWindow`窗口。

```
define stream TempStream(tempId string, temp double);
define window OneMinTempWindow(tempId string, temp double) time(1 min);

from TempStream
select *
insert into OneMinTempWindow;
```

##### Join (Window)

允许流根据条件从窗口中检索信息。

> 也可以使用两个流，聚合或表来执行连接。

**syntax**

```
from <input stream> join <window>
    on <condition>
select (<input stream>|<window>).<attribute name>, (<input stream>|<window>).<attribute name>, ...
insert into <output stream>
```

E.g 该Siddhi应用程序执行连接计数，即最近2分钟内具有超过40度的温度事件的数量。

```
define window TwoMinTempWindow (roomNo int, temp double) time(2 min);
define stream CheckStream (requestId string);

from CheckStream as C join TwoMinTempWindow as T
    on T.temp > 40
select requestId, count(T.temp) as count
insert into HighTempCountStream;
```

##### From

窗口可以是查询的输入，类似于流。注意 ！！！当窗口用作查询的输入时，不能在此基础上应用另一个窗口。

**Syntax**

```
from <window> 
select <attribute name>, <attribute name>, ...
insert into <output stream>
```

E.g 此Siddhi应用程序计算最近5分钟内的最高温度。

```
define window FiveMinTempWindow (roomNo int, temp double) time(5 min);


from FiveMinTempWindow
select max(temp) as maxValue, roomNo
insert into MaxSensorReadingStream;
```

#### Trigger 触发器

触发器允许周期性地生成事件。触发器定义可用于定义触发器。触发器的工作方式也类似于带有预定义模式的流。

**Purpose**

对于某些用例，系统应该能够基于指定的时间间隔定期生成事件，以执行一些定期执行。可以为“开始”操作、为给定的<时间间隔>或为给定的'<cron表达式>'执行触发器。

**Syntax**

触发器定义的语法如下所示。

```
define trigger <trigger name> at ('start'| every <time interval>| '<cron expression>');
```

与流类似，触发器可用作输入。它们遵循以下流定义并生成`long`类型的`triggered_time`属性。

```
define stream <trigger name> (triggered_time long);
```

目前支持以下类型的触发器：

| Trigger type            | Description                                                  |
| ----------------------- | ------------------------------------------------------------ |
| `'start'`               | Siddhi启动时会触发事件。                                     |
| `every <time interval>` | 在给定的时间间隔周期性地触发事件。                           |
| `'<cron expression>'`   | 根据给定的cron表达式定期触发事件。有关配置详细信息，请参阅[quartz-scheduler](http://www.quartz-scheduler.org/documentation/quartz-2.2.x/tutorials/tutorial-lesson-06)。 |

E.g 

* 定期以特定时间间隔触发事件

  以下查询每5分钟触发一次事件。

  ```
      define trigger FiveMinTriggerStream at every 5 min;
  ```

* 在指定日期的特定时间触发事件

  以下查询在每个工作日的上午10点15分触发事件。

  ```
       define trigger FiveMinTriggerStream at '0 15 10 ? * MON-FRI';
  ```

#### Script

脚本允许您用其他编程语言编写函数，并在Siddhi查询中执行它们。通过脚本定义的函数可以在类似于任何其他内置函数的查询中访问。函数定义可以用来定义这些脚本。函数参数作为Object[]和名称数据传递到函数逻辑中。

**Purpose**

脚本允许您定义Siddhi核心或其扩展中未提供的功能操作。不需要编写扩展来定义函数逻辑。

**Syntax**

```
define function <function name>[<language name>] return <return type> {
    <operation of the function>
};
```

定义脚本时配置以下参数。

| Parameter                   | Description                                                  |
| --------------------------- | ------------------------------------------------------------ |
| `function name`             | 函数的名称（驼峰命名法，用于函数名称）作为约定。             |
| `language name`             | 用于定义脚本的编程语言的名称，例如javascript，r和scala。     |
| `return type`               | 函数返回的属性类型。这可以是int，long，float，double，string，bool或object。这里函数实现者应该负责在定义的返回类型上返回输出属性以获得适当的功能。 |
| `operation of the function` | 这里，添加了函数的执行逻辑。此逻辑应使用语言名称下指定的语言编写，并应返回通过返回类型参数指定的数据类型的输出。 |

**Examples**

此查询使用JavaScript执行连接，并将输出作为字符串返回。

```
define function concatFn[javascript] return string {
    var str1 = data[0];
    var str2 = data[1];
    var str3 = data[2];
    var responce = str1 + str2 + str3;
    return responce;
};

define stream TempStream(deviceID long, roomNo int, temp double);

from TempStream
select concatFn(roomNo,'-',deviceID) as id, temp 
insert into DeviceTempStream;
```







































































Siddhi是一个轻量级的，简单的开源的复杂事件流程引擎。它使用类SQL的语言描述事件流任务，可以很好的支撑开发一个可扩展的，可配置的流式任务执行引擎。https://docs.wso2.com/display/CEP410/Inbuilt+Functions#InbuiltFunctions-ifThenElseifThenElse
&ensp;&ensp;Siddhi支持对于流式数据的类 SQL 的查询，SQL 式的 query 通过 complier 翻译成 Java 代码。 当一条数据流或多条数据流流入时，Siddhi Core 会实时的 check 当前数据流是否满足定义的 query，如果满足则触发 Callback 执行相应的逻辑。

## siddhi查询语言介绍
&ensp;&ensp;siddhi查询语言（siddhiql）旨在处理事件流以识别复杂的事件发生。下表提供了siddhi查询语言中几个术语的定义。



| 术语                    | 定义                                                         |
| :---------------------- | :----------------------------------------------------------- |
| Event Stream Definition | 定义事件流。一个事件流有一个唯一的名字和一组赋予特定类型的属性，其中唯一可识别的名字定义了它的模式。 |
| Event                   | 一个事件只与一个事件流关联，并且该流的所有事件都具有一组相同的属性，这些属性被分配了特定的类型（或相同的模式）。 事件包含时间戳和根据模式的属性值。 |
| Attribute               | 一个属性在事件流中具有唯一的名称。属性类型可以是字符串，int，long，float，double，bool或object。 |
| Event Table             | 存储数据的结构化表示，允许存储的数据在运行时被访问和操作。   |
| Event Stream            | 一系列按时排序的事件。                                       |
| Partition               | 一个逻辑容器，它根据预定义的分离规则处理查询的一个子集。     |
| Query                   | 通过组合现有流来推导新流的逻辑结构。查询包含一个或多个输入流，修改这些输入流的处理程序以及发布其输出事件的输出流。 |

siddhi有以下语言结构：
* Event Stream Definitions
* Event Table Definitions
* Partitions
* Queries

siddhi的执行逻辑可以作为一个执行计划组合在一起，所有上述的语言结构可以写成一个执行计划中的脚本。
每个构造应该用分号（;）分隔。

### Event Stream
&ensp;&ensp;事件流是具有定义的模式的事件序列。可以使用查询导入和处理一个或多个事件流以识别复杂的事件条件，并且创建新的事件流以通知查询响应.
&ensp;&ensp;将具有定义的模式的事件的类型序列，一个或多个事件流可以被查询消耗和操纵以便识别复杂的事件条件，并且可以发射新的事件流以通知查询响应。
### Event Stream Definition
定义了事件流模式。一个事件流定义包含一个唯一的名字和一组赋予特定类型的属性，并在流中有唯一可识别的名字。
> define stream &lt;stream name\&gt; (&lt;attribute name&gt; &lt;attribute type&gt;, &lt;attribute name&gt; &lt;attribute type&gt;, ... );

Eg.可以使用以下属性创建一个名为tempstream的流，如下所示。

| 属性名称 | 属性类型 |
| :------- | :------- |
| deviceID | long     |
| roomNo   | int      |
| temp     | double   |

> define stream TempStream (deviceID long, roomNo int, temp double);

### Query
每个siddhi查询都可以使用一个或多个事件流，并从中创建一个新的事件流。所有的查询都包含一个输入部分和一个输出部分。有些还包含投影部分。所有三个部分的简单查询如下。
> from &lt;input stream name&gt;
> select &lt;attribute name&gt;, &lt;attribute name&gt;, ...
> insert into &lt;output stream name&gt;

Eg.
>from bankSummaryInfo#window.timeBatch(5 sec)
>select idc,
> &ensp;&ensp;sum(bankCount) as totalBankCount,
>&ensp;&ensp;convert(sum(bankChannelTotalTime),'double')/convert(sum(bankCount),'double') as bankChannelAvgTime,
>&ensp;&ensp;convert(sum(bankBizSuccessCount),'double')/convert(sum(bankCount),'double') as bankBizPercent,
>&ensp;&ensp;convert(sum(bankSysSuccessCount),'double')/convert(sum(bankCount),'double') as bankSysPercent,
>&ensp;&ensp;convert(sum(bankChannelSysSuccessCount),'double')/con vert(sum(bankCount),'double') as bankChannelSysPercent,
>&ensp;&ensp;convert(sum(bankTotalTime),'double')/convert(sum(bankCount),'double') as bankAvgTime
>insert into defaultBankSummaryInfo;

#### Inferred Stream:
&ensp;&ensp;这里的defaultBankSummaryInfo是一个推断的流，即defaultBankSummaryInfo可以用作另一个查询的输入查询而不显式定义其事件流定义。因为它的事件流定义是从上面的查询中推断出来的。

#### 
|      |      |
| :--- | :--- |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |

#### Functions
一个函数需要零个，一个或多个函数参数并产生一个结果值。
#### Function parameters
函数参数可以是属性（int，long，float，double，string，bool，object），其他函数的结果，数学或逻辑表达式的结果或时间参数。时间是一个特殊的参数，我们可以使用时间值定义为int，单位类型定义为&lt;int&gt; &lt;unit&gt;。 以下是受支持的单位类型，执行时间将以毫秒为单位将其表达式作为长整型值返回。

| Unit         | Syntax                               |
| :----------- | :----------------------------------- |
| Year         | year &brvbar; yuears                 |
| Month        | month &brvbar; month                 |
| Week         | week &brvbar; weeks                  |
| Day          | day   &brvbar; days                  |
| Hour         | hour  &brvbar; hours                 |
| Minutes      | minute &brvbar; minutes &brvbar; min |
| Seconds      | second &brvbar; seconds &brvbar; sec |
| Milliseconds | millisecond &brvbar; milliseconds    |
Eg.通过1小时25分钟测试功能。
>test(1 hour 25 min)

函数，数学表达式和逻辑表达式可以以嵌套方式使用。

#### Inbuilt Functions
siddhi支持以下内置功能。
* coalesce  合并
  &lt;int|long|float|double|string|bool|object&gt; coalesce(&lt;int|long|float|double|string|bool|object&gt; arg1, &lt;int|long|float|double|string|bool|object&gt; arg2,.., &lt;int|long|float|double|string|bool|object&gt; argN)
  * Extension Type：Function
  * Description：返回第一个非null输入参数的值。
  * Parameter: 这个函数接受一个或多个参数，它们都必须是相同类型的任何一种可用类型。
  * Return Type：返回类型将是第一个输入参数的类型
  * Examples：coalesce('123', null, '789') returns '123'. coalesce(null, 76, 567) returns 76. coalesce(null, null, null) returns null.
* convert   转换
  &lt;int|long|float|double|string|bool&gt; convert(&lt;int|long|float|double|string|bool&gt;  toBeConverted, &lt;string&gt; convertedTo)
  * Extension Type：Function
  * Description：根据转换后的参数转换第一输入参数。
  * Parameter: toBeConverted：用对象以外的类型转换参数。
  * Parameter: convertedTo: 一个字符串常量参数，表示使用以下字符串值之一的外部类型 : 'int', 'long', 'float', 'double', 'string', 'bool'.
  * Return Type：返回类型将是由convertedto参数指定的类型。
  * Examples：convert('123', 'double') returns 123.0. convert(45.9, 'int') returns 46. convert(true, 'string') returns 'true'.
* instanceOfBoolean
  &lt;bool&gt; instanceOfBoolean(&lt;int|long|float|double|string|bool|object&gt; arg)
   * Extension Type: Function
   * Description：检查参数是否是布尔值的一个实例
   * Parameter: arg：要检查的参数。
   * Return Type：返回布尔型，如果参数是布尔型的实例，则返回true，否则返回false。
   * Examples：instanceOfBoolean(123) returns false. instanceOfBoolean(true) returns true. instanceOfBoolean(false) returns true.
* instanceOfDouble
  &lt;bool&gt;  instanceOfDouble(&lt;int|long|float|double|string|bool|object&gt;  arg)
  * Extension Type: Function
  * Description：检查参数是否是double的一个实例。
  * Parameter: arg：要检查的参数。
  * Return Type：返回bool，如果参数是double的实例，则返回true，否则返回false。
  * Examples：instanceOfDouble(123) returns false. instanceOfDouble(56.45) returns true. instanceOfDouble(false) returns false.
* instanceOfFloat
  &lt;bool&gt;  instanceOfFloat(&lt;int|long|float|double|string|bool|object&gt;  arg)
  * Extension Type: Function
  * Description：检查参数是否是float的一个实例。
  * Parameter: arg：要检查的参数。
  * Return Type：返回bool，如果参数是float的实例，则返回true，否则返回false。
  * Examples： instanceOfFloat(123) returns false. instanceOfFloat(56.45) returns false. instanceOfFloat(56.45f) returns true.
* instanceOfInteger
  &lt;bool&gt; instanceOfInteger(&lt;int|long|float|double|string|bool|object&gt; arg)
  * Extension Type: Function
  * Description：检查参数是否是整数的一个实例。
  * Parameter: arg：要检查的参数
  * Return Type: 返回bool，如果参数是integer的一个实例，则返回true，否则返回false。
  * Examples：instanceOfLong(123) returns false. instanceOfLong(5667l) returns true. instanceOfLong(56.67) returns false.
* instanceOfString
  &lt;bool&gt; instanceOfString(&lt;int|long|float|double|string|bool|object&gt; arg)
  * Extension Type: Function
  * Description：检查参数是否是字符串的一个实例。
  * Parameter: arg：要检查的参数
  * Return Type：返回bool，如果参数是字符串的实例，则返回true，否则返回false。
  * Examples：instanceOfString('test') returns true. instanceOfString('5667') returns true. instanceOfString(56.67) returns false.
* UUID
  &lt;string&gt; UUID()
  * Extension Type: Function
  * Description：生产一个UUID
  * Return Type：返回一个UUID字符串
  * Examples：UUID() returns a34eec40-32c2-44fe-8075-7f4fde2e2dd8.

* ifThenElse
* maximum
* minimum
* cast

Eg.将房间号转换为字符串并将消息ID引入每个事件
> from TempStream
> select convert(roomNo, 'string') as roomNo, temp, UUID() as messageID
> insert into RoomTempStream;

#### Filter
过滤器可以与输入流一起使用，以根据给定的过滤条件过滤事件。过滤条件应该在输入流名称旁边的方括号中定义。
>from &lt;input stream name&gt;[&lt;filter condition&gt;]
>select &lt;attribute name&gt;, &lt;attribute name&gt;, ...
>insert into &lt;output stream name&gt;

Eg.过滤温度大于40度的所有服务器房间。
>from TempStream [(roomNo >= 100 and roomNo < 110) and temp > 40 ]
>select roomNo, temp
>insert into HighTempStream;

#### Window
Windows允许基于来自输入事件流的标准来捕获事件子集以用于计算，可以使用“#window”在输入流旁边定义它们。 前缀，每个输入流最多只能有一个窗口，如下所示。
>from &lt;input stream name&gt;[&lt;filter condition&gt;]#window.&lt;window name&gt;(&lt;parameter&gt;, &lt;parameter&gt;, ... )
>select &lt;attribute name&gt;, &lt;attribute name&gt;, ...
>insert into &lt;output stream name&gt;

Windows为其使用的每个事件发出两个事件：它们是当前事件和过期事件。 当新事件到达窗口时，窗口发出当前事件，并且每当窗口中的事件基于该窗口条件到期时发出过期事件。

##### Inbuilt Windows
siddhi支持以下内置窗口。
* time
  &lt;event> time(&lt;int|long|time&gt; windowTime)
 * Extension Type: Window
 * Description：滑动时间窗口，其持有在上一个窗口时间段内到达的事件，并在每个事件到达和到期时得到更新。
 * Parameter: windowTime: 窗口应该容纳事件的滑动时间段。
 * Return Type：返回当前和过期的事件。
 * Examples： time(20) for processing events arrived in last 20 milliseconds. time(2 min) for processing events arrived in last 2 minutes.
* timeBatch
  &lt;event&gt; timeBatch(&lt;int|long|time&gt; windowTime)
  * Extension Type：Window
  * Description：批量（翻滚）时间窗口，用于保存在窗口时间段之间到达的事件，并在每个窗口时间更新。
  * Parameter: windowTime：窗口应该保存事件的批处理时间段。
  * Return Type：返回当前和过期的事件。
  * Examples: timeBatch(20) for processing events arrived every 20 milliseconds. timeBatch(2 min) for processing events arrived every 2 minutes.

* length
  &lt;event&gt; length(&lt;int&gt; windowLength)
  * Extension Type: Window
  * Description：滑动长度窗口，保存最后的窗口长度事件，并在每个事件到达和到期时得到更新。
  * Parameter: windowLength: 需要在滑动长度窗口中的事件的数量。
  * Return Type：返回当前和过期的事件。
  * Examples： length(10) for processing last 10 events. length(200) for processing last 200 events.

* lengthBatch
  &lt;event&gt; lengthBatch(&lt;int&gt; windowLength)
  * Extension Type: Window
  * Description：批量（滚动）长度窗口，可以容纳窗口事件，并在每个窗口事件到达时更新。
  * Parameter: windowLength：对于窗口应该翻滚的事件数量。
  * Return Type：返回当前和过期的事件。
  * Examples: lengthBatch(10) for processing 10 events as a batch. lengthBatch(200) for processing 200 events as a batch.

* externalTime
  &lt;event&gt; time(&lt;long&gt; timestamp, &lt;int|long|time&gt; windowTime)
  * Extension Type: Window
  * Description：基于外部时间的滑动时间窗口，其保持来自外部时间戳的最后一个窗口时间段期间到达的事件，并且在每个单调递增的时间戳上得到更新。
  * Parameter: timestamp：窗口确定为当前时间并将采取行动的时间，此参数的值应单调递增。
  * Parameter: windowTime: 窗口应该容纳事件的滑动时间段。
  * Return Type：返回当前和过期的事件。
  * Examples： externalTime(eventTime,20) for processing events arrived in last 20 milliseconds from the eventTime. externalTime(eventTimestamp, 2 min) for processing events arrived in last 2 minutes from eventTimestamp.

* cron
  &lt;event&gt; cron(&lt;string&gt; cronExpression)
  * Extension Type: Window
  * Description：cron窗口会以时间重复的方式周期性的输出处理过的事件，这就是基于时间的流逝而触发的。
  * Parameter: cronExpression：代表时间表的cron表达式。
  * Return Type：返回当前和过期的事件。
  * Examples： cron('*/5 * * * * ?') will output processed events every 5 seconds.

* firstUnique
  &lt;event&gt; firstUnique(&lt;string&gt; attribute)
  * Extension Type: Window
  * Description：第一个唯一窗口处理器根据给定的唯一属性只保留唯一的第一个事件。
  * Parameter: attribute：应该检查唯一性的属性。
  * Return Type：返回当前和过期的事件。
  * Examples：firstunique（ip）将返回每个唯一ip的第一个事件。

* unique
  &lt;event&gt; unique(&lt;string&gt; attribute)
  * Extension Type: Window
  * Description：独特的窗口处理器只根据给定的唯一属性保留唯一的最新事件。
  * Parameter: attribute：应该检查唯一性的属性。
  * Return Type：返回当前和过期的事件。
  * Examples：unique（IP）将返回最新的事件到达每个独特的IP。

* sort
  &lt;event&gt; sort(&lt;int&gt; windowLength)
  &lt;event&gt; sort(&lt;int&gt; windowLength, &lt;string&gt; attribute, &lt;string&gt; order)
  &lt;event&gt; sort(&lt;int&gt; windowLength, &lt;string&gt; attribute, &lt;string&gt; order, .. , &lt;string&gt; attributeN, &lt;string&gt; orderN)
  * Extension Type: Window
  * Description：排序处理器将保持到windowlength事件，并按给定的顺序排序。
  * Parameter: windowLength：对于窗口应该翻滚的事件数量
  * Parameter: attribute：应该检查订单的属性。
  * Parameter: order：由“asc”或“desc”定义的属性的顺序。如果某个属性既不是“asc”也不是“desc”，那么order默认为“asc”。
  * Return Type：返回当前和过期的事件。
  * Examples：sort(5, price, 'asc') 按升序排列按价格排序的事件. 因此，在任何时候，窗口都包含5个最低价格。

* frequent
  &lt;event&gt; frequent(&lt;int&gt; eventCount)
  &lt;event&gt; frequent(&lt;int&gt; eventCount, &lt;string&gt; attribute, .. , &lt;string&gt; attributeN)
  * Extension Type: Window
  * Description：频繁的窗口处理器将返回给定属性最常出现的值的最新事件。这个窗口处理器的频率计算是基于misra-gries（Misra-Gries算法是频繁项挖掘中一个著名的算法）计算算法的。
  * Parameter: eventCount: 发送到流中的最频繁事件的数量
  * Parameter: attribute：属性来分组事件。如果没有给出属性，则将考虑事件的所有属性的连接。
  * Return Type：返回当前和过期的事件。
  * Examples： frequent(2) 将返回2个最频繁的事件， frequent(2, cardNo) 将返回2个最新的事件与最频繁出现的卡号码。

* lossyFrequent
  &lt;event&gt; lossyFrequent(&lt;double&gt; supportThreshold, &lt;double&gt; errorBound)
  &lt;event&gt; lossyFrequent(&lt;double&gt; supportThreshold, &lt;double&gt; errorBound, &lt;string&gt; attribute, .. , &lt;string&gt; attributeN)
  * Extension Type: Window
  * Description：有损频繁窗口处理器将识别并返回当前频率超过支持阈值的所有事件。该窗口处理器的频率计算基于有损计数算法。
  * Parameter: supportThreshold：支持阈值
  * Parameter: errorBound：错误界限值
  * Parameter: attribute：属性来分组事件。如果没有给出属性，则将考虑事件的所有属性的连接。
  * Return Type：返回当前和过期的事件。
  * Examples： lossyFrequent(0.1, 0.01)将返回当前频率超过0.1的所有事件，误差范围为0.01。lossyFrequent(0.3, 0.05, cardNo)将返回cardno属性频率超过0.3的所有事件，误差为0.05。


#### Output Event Categories
窗口输出可以基于事件类别（即当前事件和过期事件）来操作，使用以下关键字和输出流来操纵输出。
* current events：将发出所有到达窗口的事件。这是默认的功能是没有指定事件类别。
* expired events：将从窗口发出所有到期的事件。
* all events：将从窗口发出所有到达和到期的事件。

Eg.将流中的所有事件延迟1分钟。
>from TempStream#window.time(1 min)
>select *
>insert expired events into DelayedTempStream


#### Aggregate Functions
可以在窗口中使用集合函数在定义的窗口内执行集合计算。

#### Inbuilt Aggregate Functions
siddhi支持以下内置聚合函数。
* sum
  &lt;long|double&gt; sum(&lt;int|long|double|float&gt; arg)
  * Extension Type：Aggregate Function (聚合函数)
  * Description：计算所有事件总和
  * Parameter: arg：需要总结的值
  * Return Type：如果输入参数类型为int或long，则返回long，如果输入参数类型为float或double，则返回double。
  * Examples：sum(20)为每个事件的到达和到期返回一个20的总和.sum(temp)根据每个事件的到达和到期返回所有临时属性的总和。

* avg
  &lt;double&gt; avg(&lt;int|long|double|float&gt; arg)
  * Extension Type: Aggregate Function
  * Description：计算所有事件的平均值。
  * Parameter: arg：需要平均的值。
  * Return Type：将计算的平均值作为双倍返回。
  * Examples：avg(temp)根据到达和到期时间返回所有事件的平均温度值。

* max
  &lt;int|long|double|float&gt; max(&lt;int|long|double|float&gt; arg)
  * Extension Type: Aggregate Function
  * Description：返回所有事件的最大值。
  * Parameter: arg：需要比较的值才能找到最大值
  * Return Type：返回与输入相同类型的最大值。
  * Examples：max(temp)根据其到达和到期时间返回所有事件记录的最大温度值

* min
  &lt;int|long|double|float&gt; min(&lt;int|long|double|float&gt; arg)
  * Extension Type: Aggregate Function
  * Description：返回所有事件的最小值
  * Parameter: arg：需要比较的值才能找到最小值
  * Return Type：返回与输入相同类型的最小值。
  * Examples：min(temp)根据到达和到期时间返回所有事件记录的最低温度值

* count
  &lt;double&gt; stddev（&lt;int | long | double | float&gt; arg）
  * Extension Type: Aggregate Function
  * Description：返回所有事件的计数。
  * Return Type：返回事件计数
  * Examples：count() 将返回所有事件的计数。

* stddev
  &lt;double&gt; stddev(&lt;int|long|double|float&gt; arg)
  * Extension Type: Aggregate Function
  * Description：返回所有事件的计算标准偏差。
  * Parameter: arg：在计算标准偏差时应该使用的数值
  * Return Type：将计算的标准偏差值作为双精度返回。
  * Examples：stddev(temp)返回所有基于到达和到期的事件的温度的计算标准偏差
    Eg.通知所有活动到达和到期的所有房间的平均温度基于在过去10分钟到达的所有事件。
>from TempStream#window.time(10 min)
>select avg(temp) as avgTemp, roomNo, deviceID
>insert all events into AvgTempStream;

#### Group By
group by允许我们根据属性对group进行分组。
Eg.查找最近10分钟内每个房间和设备ID的平均温度。
>from TempStream#window.time(10 min)
>select avg(temp) as avgTemp, roomNo, deviceID
>group by roomNo, deviceID
>insert into AvgTempStream;

#### Having
允许我们在聚合之后和在选择器处理之后过滤事件。
Eg.查找最近10分钟内的每个房间的平均温度，并在超过30度时发出警报。

>from TempStream#window.time(10 min)
>select avg(temp) as avgTemp, roomNo
>group by roomNo
>having avgTemp > 30
>insert into AlertStream;

#### Output Rate Limiting
输出速率限制允许查询根据指定的条件周期性地发送事件。
速率限制遵循以下语法。
>from &lt;input stream name&gt;...
>select &lt;attribute name&gt;, &lt;attribute name&gt;, ...
>output ({&lt;output-type&gt;} every (&lt;time interval&gt;|&lt;event interval&gt; events) | snapshot every &lt;time interval&gt;)
>insert into &lt;output stream name&gt;

使用“<output-type>”可以指定需要发出的事件数量，“first”，“last”和“all”是可指定为只发出第一个事件，最后一个事件，
或来自所到达事件的所有事件。如果关键字被省略，它将默认为“全部”发出所有事件。
用“<time interval>”来定义周期性事件情感的时间间隔。
通过“<event interval>”，可以指定需要到达的周期事件情感的事件数量。

#### Based on number of events   根据事件数量
这里事件将在预定数量的事件到达时发出，当发射事件可以被指定为仅发出来自事件的第一事件，最后事件或所有事件时。
Eg.每10个事件发出一个传感器的最后温度事件
>from TempStream
>select temp
>group by deviceID
>output last every 10 events
>insert into LowRateTempStream;

#### Based on time  基于时间
这里事件将在每个预定义的时间间隔发射，当发射它可以被指定为仅发射来自事件的第一事件，最后事件或所有事件。
Eg.每10秒发出一次温度事件
>from TempStream
>output every 10 sec
>insert into LowRateTempStream;

#### Periodic snapshot   定期快照
这对于Windows最有效，当输入流作为窗口附加的快照速率限制时，将发出迄今为止到达的所有当前事件，在每个预定义的时间间隔内没有相应的过期事件，同时当没有窗口连接到输入时流只会在每个预定义的时间间隔内发出最后的当前事件。
Eg.以每秒5秒的时间窗口发出事件的快照。
>from TempStream#window.time(5 sec)
>output snapshot every 1 sec
>insert into SnapshotTempStream;

#### Joins
join允许两个事件流根据条件进行合并.这里每个流都应该与一个窗口相关联（如果没有窗口赋值＃window.length（0）被分配给输入事件流）。在加入过程中，基于给定的条件，每个流上的每个传入事件将与另一个输入事件流窗口中的所有事件匹配，并且对于所有匹配的事件对，将生成输出事件。
连接的语法如下所示:
>from &lt;input stream name&gt;[&lt;filter condition&gt;]#window.&lt;window name&gt;(&lt;parameter&gt;, ... ) {unidirectional} {as &lt;reference&gt;}
>​       join &lt;input stream name&gt;#window.&lt;window name&gt;(&lt;parameter&gt;,  ... ) {unidirectional} {as &lt;reference&gt;}
>   on &lt;join condition&gt;
>   within &lt;time gap&gt;
>select &lt;attribute name&gt;, &lt;attribute name&gt;, ...
>insert into &lt;output stream name&gt;

与“在<join condition>”siddhi只加入匹配条件的事件。
用“单向”关键字可以控制加入过程的触发。默认情况下，到达两个流的事件触发加入过程，并且在输入流上使用单向关键字时，只有到达该流的事件才会触发加入过程。请注意，我们不能对这两个输入流使用单向关键字（因为它等于默认行为，根本不使用单向关键字）。
与“在<time gap>”加入过程相匹配的事件是在规定的时间间隔彼此。
当投影连接事件时，每个流的属性需要用流名称（例如<stream name>。<attribute name>）或引用ID（特别是当连接相同流的事件时）引用（例如<stream reference Id>。<attribute name>），可以使用“select *”或者“select”语句本身，如果连接事件的所有属性都需要被投影，则这些语句本身可以被忽略，但是这些只能在两个流都没有具有相同名称的属性。
Eg.假定温度调节器每分钟更新一次。如果房间温度大于30度的所有房间都没有打开温度调节器，那么以下开关将会打开。

>define stream TempStream(deviceID long, roomNo int, temp double);
><br>define stream RegulatorStream(deviceID long, roomNo int, isOn bool);<br>
>from TempStream[temp &gt; 30.0]#window.time(1 min) as T
> &ensp;join RegulatorStream[isOn == false]#window.length(1) as R
> &ensp;on T.roomNo == R.roomNo
>select T.roomNo, R.deviceID, 'start' as action
>insert into RegulatorActionStream;

#### Pattern
模式允许事件流随时间相关，并根据事件到达的顺序检测事件模式。与模式可以有其他事件之间的事件符合模式条件。它将在内部创建状态机来跟踪匹配进程的状态。模式可以在多个输入流或相同的输入流上关联事件，因此每个匹配的输入事件需要被引用，以便它可以被访问用于未来的处理和输出生成。
模式的语法如下所示:
>from {every} &lt;input event reference&gt;=&lt;input stream name&gt;[&lt;filter condition&gt;] -&gt; {every} &lt;input event reference&gt;=&lt;input stream name&gt;[&lt;filter condition&gt;] -&gt; ...
>   &ensp;&ensp;within &lt;time gap&gt;
>select &lt;input event reference&gt;.&lt;attribute name&gt;, &lt;input event reference&gt;.&lt;attribute name&gt;, ...
>insert into &lt;output stream name&gt;

输入流不能与窗口关联。
使用“ - >”我们可以关联传入的事件到达，在匹配事件之间有零个或多个其他事件到达。
使用"&lt;input event reference>=”匹配的事件可以被存储以备将来参考。
使用“within&lt;time gap>”的模式将只与相互之间定义的时间间隔内的事件相匹配。
如果没有“every”关键字，模式只能匹配一次，恰当地使用“每个”关键字来触发事件到达时的模式匹配过程。
Eg.如果房间温度在10分钟内上升5度，则发出警报。
>from every( e1=TempStream ) -> e2=TempStream[e1.roomNo==roomNo and (e1.temp + 5) <= temp ]
>   &ensp;&ensp;within 10 min
>select e1.roomNo, e1.temp as initialTemp, e2.temp as finalTemp
>insert into AlertStream;

#### Logical Pattern  逻辑模式
模式不仅匹配按时间顺序到达的事件，还可以将具有逻辑关系的事件关联起来。
可以在“ - >”之间使用“and”，“or”等关键词来说明逻辑关系。
"and" 可以匹配任何顺序的两个事件的发生
"or" 可以匹配来自任何输入流的事件的发生
Eg.当房间温度达到调节器上设置的温度时，提醒（只要调节器上设置的温度发生变化，模式匹配应该重新设置）。
>define stream TempStream(deviceID long, roomNo int, temp double);
><br>define stream RegulatorStream(deviceID long, roomNo int, tempSet double);
><br>from every( e1=RegulatorStream ) -> e2=TempStream[e1.roomNo==roomNo and e1.tempSet <= temp ] or e3=RegulatorStream[e1.roomNo==roomNo]
><br>select e1.roomNo, e2.temp as roomTemp
>having e3 is null
>insert into AlertStream;


#### Counting Pattern  计算模式
计数模式使我们能够根据相同的匹配条件匹配多个事件。使用以下后缀可以限制预期的事件数量。
With <1:4> 可以匹配1到4个时间
With <2:> 匹配2个或更多时间
with <:5> 最多匹配5个事件
With <5>  完全匹配5个事件
根据计数限制来引用事件的具体事件，方括号可以与数字和“last”关键字一起使用，例如e1 [3]将引用第三个事件，e1 [last]将引用最后一个事件和e1 [last  -  1]将引用匹配事件组的最后一个事件之前的事件。
Eg.得到两个调节器事件之间的温差。
>define stream TempStream(deviceID long, roomNo int, temp double);
>define stream RegulatorStream(deviceID long, roomNo int, tempSet double, isOn bool);
> from every( e1=RegulatorStream) -> e2=TempStream[e1.roomNo==roomNo]<1:> -> e3=RegulatorStream[e1.roomNo==roomNo]
>select e1.roomNo, e2[0].temp - e2[last].temp as tempDiff
>insert into TempDiffStream;

#### Sequence  序列
序列允许事件流随时间相关，并根据事件到达的顺序检测事件序列。在序列中，在与序列条件匹配的事件之间不能有其他事件。它将在内部创建状态机来跟踪匹配进程的状态。序列可以关联多个输入流或相同输入流上的事件，因此每个匹配的输入事件都需要被引用，使得它可以被访问用于未来的处理和输出生成。
序列的语法如下所示:
>from {every} &lt;input event reference&gt;=&lt;input stream name&gt;[&lt;filter condition&gt;], &lt;input event reference&gt;=&lt;input stream name&gt;[&lt;filter condition&gt;]{+|*|?}, ...
>   within &lt;time gap&gt;
>select &lt;input event reference&gt;.&lt;attribute name&gt;, &lt;input event reference&gt;.&lt;attribute name&gt;, ...
>insert into &lt;output stream name&gt;

输入流不能与窗口关联：
With "," 我们可以将即将到来的下一个到达的事件关联起来，在匹配事件之间没有其他事件到达。
With "&lt;input event reference>=” 匹配的事件可以被存储以备将来参考。
With "within &lt;time gap>" 该序列将仅与在彼此的定义的时间间隙内的事件相匹配。
Without "every" 关键字模式只能匹配一次，在每个事件到来时，使用开始处的“every”关键字来触发序列匹配过程。
Eg.如果两次连续的温度事件之间的温度升高超过1度，则应警惕。
>from every e1=TempStream, e2=TempStream[e1.temp + 1 < temp ]
>select e1.temp as initialTemp, e2.temp as finalTemp
>insert into AlertStream;

#### Logical Sequence   逻辑序列
序列不仅匹配按时间顺序到达的连续事件，而且还可以关联具有逻辑关系的事件。
“and”和“or”等关键词可以用于“，”之间，说明逻辑关系。
With "and" 两个事件发生的顺序是可以匹配的
With "or" 可以匹配来自任何输入流的事件的发生
Eg.通知温度和湿度事件发生在监管事件之后。
>define stream TempStream(deviceID long, temp double);
>define stream HumidStream(deviceID long, humid double);
>define stream RegulatorStream(deviceID long, isOn bool);
>from every e1=RegulatorStream, e2=TempStream and e3=HumidStream
>select e2.temp, e3.humid
>insert into StateNotificationStream;

### Counting Sequence 计算序列