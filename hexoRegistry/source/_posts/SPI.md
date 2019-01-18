---
title: SPI
date: 2018-06-12 20:24:46
categories: java
tags: java
---
# SPI
SPI 全称为 (Service Provider Interface) ,是JDK内置的一种服务提供发现机制。面向的对象的设计里，我们一般推荐模块之间基于接口编程，模块之间不对实现类进行硬编码。一旦代码里涉及具体的实现类，就违反了可拔插的原则，如果需要替换一种实现，就需要修改代码。
为了实现在模块装配的时候能不在程序里动态指明，这就需要一种服务发现机制。java spi就是提供这样的一个机制：为某个接口寻找服务实现的机制。有点类似IOC的思想，就是将装配的控制权移到程序之外，在模块化设计中这个机制尤其重要。


## SPI与API
API：侧重于服务端，服务方对外提供一支接口服务，并将对应实现类打入同一包结构中。
SPI：侧重于调用端，服务方对外提供一支接口服务，但是具体实现服务方可以提供也可以不提供，有调用端自行实现。

| 对比 |  概念差异 |  逻辑差异 | 结构差异 |
|:----: |:--------: |:--------: |:-------: |
| SPI  | 更接近于实现方 | 组织上位于实现方所在的包中 | 实现和接口在一个包中|
| API  | 更接近于调用方 | 组织上位于调用方所在的包中 |实现位于独立的包中（也可认为在提供方中）|

简单理解API更注重于服务端的实现，SPI更关注与调用方的扩展性。想修改一个实现时不需要对它进行硬编码了。api`是给使用者使用的,`spi`是给拓展者使用的.一个好的开源框架,必须要留一些拓展点.让参与者尽量黑盒拓展,而不是白盒修改代码,否则分支,质量,合并,冲突都会很难管理.并且框架作者能做到的功能,拓展者也一定能做到. 

## SPI规范
要实现一个SPI应该具备哪些规范呢
![spi规范](http://oy48q6kwm.bkt.clouddn.com/89f1b570bd2bc6f736864b6dcd223da8.png)

## SPI实例
项目结构：
![spi](http://oy48q6kwm.bkt.clouddn.com/844260e730402156de6fc27fdaab4225.png)

HelloSpi接口：
```java
package com.nucc.channel.govern.demo.spi;

/**
 * @description: SPI接口
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/6 18:24
 * @version: 1.0.0
 */
public interface HelloSpi {
    /**
     * hello,SPI
     */
    void sayHello();
}

```

实现类：
```java
package com.nucc.channel.govern.demo.spi.impl;

import com.nucc.channel.govern.demo.spi.HelloSpi;

/**
 * @description: spi
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/6 18:26
 * @version: 1.0.0
 */
public class HelloSpiImpl implements HelloSpi{
    @Override
    public void sayHello() {
        System.out.println("hello, SPI!");
    }
}
```
```java
package com.nucc.channel.govern.demo.spi.impl;

import com.nucc.channel.govern.demo.spi.HelloSpi;

/**
 * @description: 扩展
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/6 18:50
 * @version: 1.0.0
 */
public class HelloSpiImplExtend implements HelloSpi{
    @Override
    public void sayHello() {
        System.out.println("扩展helloSpi接口");
    }
}
```

调用SPI：
```java
package com.nucc.channel.govern.demo.spi;

import java.util.Iterator;
import java.util.ServiceLoader;

/**
 * @description: 调用SPI
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/6 18:38
 * @version: 1.0.0
 */
public class Run {
    public static void main(String[] args) {

        ServiceLoader<HelloSpi> serviceLoader = ServiceLoader.load(HelloSpi.class);
        for (HelloSpi spi : serviceLoader) {
            spi.sayHello();
        }
    }
}
```
执行结果：
![执行结果](http://oy48q6kwm.bkt.clouddn.com/99cc45ae7656f070832417cd2a8937e2.png)


## Dubbo的SPI
* JDK标准的SPI会一次性实例化扩展接口的所有实现，如果有扩展的实现初始化很耗时，如果有扩展的实现没有使用，那么这种场景就会增加额外资源开销。
* JDK标准的SPI不具备依赖注入能力，Dubbo增加了对扩展实现的IOC和AOP的支持。一个扩展实现可以直接setter注入其他扩展实现。

### 规范
![dubboSPI](http://oy48q6kwm.bkt.clouddn.com/5d10eb2954d50d994b881d8b9de2aac0.png)

### 实现路径

 * <T> ExtensionLoader<T> getExtensionLoader(Class<T> type)：为接口类new一个ExtensionLoader对象，并将其缓存起来。
 * T getAdaptiveExtension()：获取一个扩展装饰类对象(使用装饰模式)，这个类定义了一个规则，如果没有@Adaptive注解，则动态创建装饰类。例如：Protocol$Adaptive对象（$代表动态）。
 * T getExtension(String name)：获取一个对象
