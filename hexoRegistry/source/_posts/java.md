---
title: java
date: 2018-06-12 19:46:16
categories: java
tags: java
---
基础知识点学习
======

## 1、for(;;)与while(true)
从字面理解for(;;)是无条件循环而while(true)是有条件循环。
`while(true)`
编译后的指令
>mov     eax,1
test    eax,eax
je      wmain+29h
jmp     wmain+1Eh
>

`for(;;)`编译后的指令
> jmp     wmain+29h     　　

很显然，for ( ; ; )指令少，不占用寄存器，而且没有判断、跳转，比while (true)好。

## 2、transient
  我们都知道一个对象只要实现了Serilizable接口，这个对象就可以被序列化，java的这种序列化模式为开发者提供了很多便利，我们可以不必关系具体序列化的过程，只要这个类实现了Serilizable接口，这个类的所有属性和方法都会自动序列化。

  然而在实际开发过程中，我们常常会遇到这样的问题，这个类的有些属性需要序列化，而其他属性不需要被序列化，打个比方，如果一个用户有一些敏感信息（如密码，银行卡号等），为了安全起见，不希望在网络操作（主要涉及到序列化操作，本地序列化缓存也适用）中被传输，这些信息对应的变量就可以加上transient关键字。换句话说，这个字段的生命周期仅存于调用者的内存中而不会写到磁盘里持久化。

  总之，java 的transient关键字为我们提供了便利，你只需要实现Serilizable接口，将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会序列化到指定的目的地中。

```java
package com.nucc.govern;

import java.io.*;

import lombok.Getter;
import lombok.Setter;

/**
 * @description: transient 关键词
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/29 18:19
 * @version: 1.0.0
 */
public class TransientKeyWords {


    public static void main(String[] args) {
        User user = new User();
        user.setUsername("Ant");
        user.setPasswd("123456");

        System.out.println("read before Serializable: ");
        System.out.println("username: " + user.getUsername());
        System.out.println("password: " + user.getPasswd());
        ObjectOutputStream os = null;
        ObjectInputStream is = null;
        String path = "D:/data/appLogs/user.txt";
        /*
         * 将User对象写进文件
         */
        try {
            os = new ObjectOutputStream(
                    new FileOutputStream(path));
            os.writeObject(user);
            os.flush();
            os.close();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (os != null) {
                try {
                    os.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        /*
         * 读取User文件
         */
        try {
            is = new ObjectInputStream(new FileInputStream(path));
            User u = (User) is.readObject();
            System.out.println("\nread after Serializable: ");
            System.out.println("username: " + u.getUsername());
            System.out.println("password: " + u.getPasswd());
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (is != null) {
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

@Getter
@Setter
class User  implements Serializable {
    private String username;
    private transient String passwd;
}
```

![transient](http://oy48q6kwm.bkt.clouddn.com/e019e975f7cd6411cc279c2f60d93153.png)

* 一旦变量被transient修饰，变量将不再是对象持久化的一部分，该变量内容在序列化后无法获得访问。
* transient关键字只能修饰变量，而不能修饰方法和类。注意，本地变量(局部变量)是不能被transient关键字修饰的。变量如果是用户自定义类变量，则该类需要实现Serializable接口。
* 被transient关键字修饰的变量不再能被序列化，一个静态变量不管是否被transient修饰，均不能被序列化。
*  我们知道在Java中，对象的序列化可以通过实现两种接口来实现，若实现的是Serializable接口，则所有的序列化将会自动进行，若实现的是Externalizable接口，则没有任何东西可以自动序列化，需要在writeExternal方法中进行手工指定所要序列化的变量，这与是否被transient修饰无关。

## 3、Thread深入理解

#### 3.1 基本概念

​	提到线程首先要区分下线程和进程之间的关系，一些老的面试题也总喜欢问这种问题。首先我们来明确下进程和线程的基本概念（以下定义均来自百度百科）。

* 进程（Process）是计算机中的程序关于某数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位，是[操作系统](https://baike.baidu.com/item/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F)结构的基础。在早期面向进程设计的计算机结构中，进程是程序的基本执行实体；在当代面向线程设计的计算机结构中，进程是线程的容器。程序是指令、数据及其组织形式的描述，进程是程序的实体 。简单的说进程是正在运行的程序的实例 。

 ![1527948600360](http://oy48q6kwm.bkt.clouddn.com/01fd522cdfd7440286bdae412496d8a8.png)

* 线程，有时被称为轻量级进程(Lightweight Process，LWP），是程序执行流的最小单元。一个标准的线程由线程ID，当前指令[指针](https://baike.baidu.com/item/%E6%8C%87%E9%92%88)(PC），[寄存器](https://baike.baidu.com/item/%E5%AF%84%E5%AD%98%E5%99%A8)集合和[堆栈](https://baike.baidu.com/item/%E5%A0%86%E6%A0%88)组成。另外，线程是进程中的一个实体，是被系统独立调度和分派的基本单位，线程自己不拥有系统资源，只拥有一点儿在运行中必不可少的资源，但它可与同属一个进程的其它线程共享进程所拥有的全部资源。一个线程可以创建和撤消另一个线程，同一进程中的多个线程之间可以并发执行。由于线程之间的相互制约，致使线程在运行中呈现出间断性。线程也有[就绪](https://baike.baidu.com/item/%E5%B0%B1%E7%BB%AA)、[阻塞](https://baike.baidu.com/item/%E9%98%BB%E5%A1%9E)和[运行](https://baike.baidu.com/item/%E8%BF%90%E8%A1%8C)三种基本状态。就绪状态是指线程具备运行的所有条件，逻辑上可以运行，在等待处理机；运行状态是指线程占有处理机正在运行；阻塞状态是指线程在等待一个事件（如某个信号量），逻辑上不可执行。每一个程序都至少有一个线程，若程序只有一个线程，那就是程序本身。

  线程是程序中一个单一的顺序控制流程。

  进程内有一个相对独立的、可调度的执行单元，是系统独立调度和分派CPU的基本单位指令[运行](https://baike.baidu.com/item/%E8%BF%90%E8%A1%8C)时的程序的调度单位。在单个程序中同时运行多个线程完成不同的工作，称为[多线程](https://baike.baidu.com/item/%E5%A4%9A%E7%BA%BF%E7%A8%8B)。

​      **进程和线程的主要差别在于它们是不同的操作系统资源管理方式。进程有独立的地址空间，一个进程崩溃后，在保护模式下不会对其它进程产生影响，而线程只是一个进程中的不同执行路径。线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间，一个线程死掉就等于整个进程死掉，所以多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。但对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程。** 

首先实现一个简单的线程任务：

```java
public class ThreadsAndRunnables {
    public static void main(String[] args) {

        //实现Runnable接口函数
        Runnable task = () -> {
            System.out.println(Thread.currentThread().getName());
        };
        task.run();

        //定义线程指定其执行任务
        Thread thread = new Thread(task);
        thread.start();

        System.out.println("Done");
    }
}
```

![1527950161141](http://oy48q6kwm.bkt.clouddn.com/d72b60acf2daaf1c047ef60c33037906.png)

这里可以看出main函数本身就是一个线程入口，thread.start()执行前先执行了输入Done。由于我们不能预测这个runnable是在打印'done'前执行还是在之后执行。顺序是不确定的，因此在大的程序中编写并发程序是一个复杂的任务。 

指定thread睡眠：

```java
public class ThreadsAndRunnables {
    public static void main(String[] args) {

        //实现Runnable接口函数
        Runnable task = () -> {
            String threadName = Thread.currentThread().getName();
            System.out.println("This thread foo :" + threadName + "_" + LocalDateTime.now());
            try {
                TimeUnit.SECONDS.sleep(5);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("This tread bar :" + threadName  + "_" + LocalDateTime.now());
        };
        task.run();

        //定义线程指定其执行任务
        Thread thread = new Thread(task);
        thread.start();

        System.out.println("Done");
    }
}
```

![1527951519015](http://oy48q6kwm.bkt.clouddn.com/a6fe0d14dbe2fbb32df06d76480a5a9d.png)


从上面的输出内容可以看出main和Thread-0再打印foo和bar时均间隔5秒。TimeUnit.SECONDS.sleep(5)等价于Thread.sleep(5000)。

#### 3.2 线程池

​	线程的基本概念与实现方式熟悉后我们来看下线程池是个什么鬼。线程池是一种多线程处理形式，处理过程中将任务添加到队列，然后在创建线程后自动启动这些任务。线程池线程都是后台线程。每个线程都使用默认的[堆栈](https://baike.baidu.com/item/%E5%A0%86%E6%A0%88)大小，以默认的优先级运行，并处于多线程单元中。如果某个线程在[托管代码](https://baike.baidu.com/item/%E6%89%98%E7%AE%A1%E4%BB%A3%E7%A0%81)中空闲（如正在等待某个事件）,则线程池将插入另一个[辅助线程](https://baike.baidu.com/item/%E8%BE%85%E5%8A%A9%E7%BA%BF%E7%A8%8B)来使所有处理器保持繁忙。如果所有线程池线程都始终保持繁忙，但队列中包含挂起的工作，则线程池将在一段时间后创建另一个辅助线程，但线程的数目永远不会超过最大值。超过最大值的线程可以排队，但他们要等到其他线程完成后才启动。简单理解线程池是可以控制线程创建、释放，并通过某种策略尝试复用线程去执行任务的一种管理框架，从而实现线程资源与任务之间的一种平衡。 

​	常见的线程池有四中分类：

* FixThreadPool

  具有固定的线程数量即定长线程池。其特点为每当提交一个任务就创建一个工作线程，如果工作线程数量达到线程池初始的最大数，则将提交的任务存入到池队列中。 核心线程是没有超时机制的，队列大小没有限制，除非线程池关闭了核心线程才会被回收。

* CacheThreadPool

  缓存线程池也叫无界线程池。这种线程池的特点是只有非核心线程 ，最大工作线程数几乎没有限制完全根据参数maximumPoolSize来配置（但实际大小不能超过Interger. MAX_VALUE ）。它会为每一个任务添加一个新的线程，这边有一个超时机制，当空闲的线程在keepAliveTime指定空闲时间内没有用到的话，就会被回收（缺省值是60s）。缺点就是没有考虑到系统的实际内存大小。 

* SingleThreadPool

  单线程池。整个线程池中只有一条核心工作线程，如果这条线程异常结束了那么会新启一条线程替代它继续执行保证任务按顺序执行。单工作线程最大的特点是可保证顺序地执行各个任务，并且在任意给定的时间不会有多个线程是活动的 ，避免了多线程并发的问题同时也可以看到性能低下。

* ScheduledThreadPool

  定时线程池。首先它是一个定长的线程池同时它有具备按照周期反复执行task的能力。它的核心线程池固定，非核心线程的数量没有限制，但是闲置时会立即会被回收。 

		 **Java中线程的架构**


![1527953979409](http://oy48q6kwm.bkt.clouddn.com/eaa7f5883e640463ca174dae3a65a872.png)
Executor是最基础的执行接口；

ExecutorService接口继承了Executor，在其上做了一些shutdown()、submit()的扩展，可以说是真正的线程池接口；

AbstractExecutorService抽象类实现了ExecutorService接口中的大部分方法；

TheadPoolExecutor继承了AbstractExecutorService，是线程池的具体实现；

ScheduledExecutorService接口继承了ExecutorService接口，提供了带"周期执行"功能ExecutorService；

ScheduledThreadPoolExecutor既继承了TheadPoolExecutor线程池，也实现了ScheduledExecutorService接口，是带"周期执行"功能的线程池；

Executors是线程池的静态工厂，其提供了快捷创建线程池的静态方法。

***代码分析***

1. Executor

   ```java
   public interface Executor {
   
       /**
        * Executes the given command at some time in the future.  The command
        * may execute in a new thread, in a pooled thread, or in the calling
        * thread, at the discretion of the {@code Executor} implementation.
        *
        * @param command the runnable task
        * @throws RejectedExecutionException if this task cannot be
        * accepted for execution
        * @throws NullPointerException if command is null
        */
       void execute(Runnable command);
   }
   ```

   Executor译为执行者。该接口只提供了一个execute()方法用来执行提交的Runnable对象，这个接口提供了一种将任务提交与任务执行的解耦方法。

2. ExecutorService

   执行者服务接口，它是线程池的真正接口。在Executor接口上做了一些扩展封装，例如用来管理任务如何停止的shutdown()相关方法、用来追踪一个或多个异步任务执行结果的Future对象的submit()相关方法。

   ExecutorService提供的所有方法。

   ```java
   /**
    * 启动一次有序的关闭，之前提交的任务执行，但不接受新任务
    * 这个方法不会等待之前提交的任务执行完毕
    */
   void shutdown();
    
   /**
    * 试图停止所有正在执行的任务，暂停处理正在等待的任务，返回一个等待执行的任务列表
    * 这个方法不会等待正在执行的任务终止
    */
   List<Runnable> shutdownNow();
    
   /**
    * 如果已经被shutdown，返回true
    */
   boolean isShutdown();
    
   /**
    * 如果所有任务都已经被终止，返回true
    * 是否为终止状态
    */
   boolean isTerminated();
    
   /**
    * 在一个shutdown请求后，阻塞的等待所有任务执行完毕
    * 或者到达超时时间，或者当前线程被中断
    */
   boolean awaitTermination(long timeout, TimeUnit unit) throws InterruptedException;
   ```

   

   当我们使用完ExecutorService之后应该关闭它，否则它里面的线程会一直处于工作状态。例如通过main()方法启动应用服务，当退出main()方法时如果没有关闭ExecutorService，那么这个应用服务奖一直执行。之所以会出现这种现象是因为ExecutorService中运行的线程会组织JVM关闭。那么如何要==安全==的停掉关闭线程池呢

   ```java
   public class StopThread {
       public static void main(String[] args) {
           ExecutorService pool = Executors.newFixedThreadPool(5);
           final long awitTime1 = 8;
           final long awitTime2 = 5;
   
           Runnable task1 = () -> {
               try {
                   System.out.println("task1 is start!");
                   TimeUnit.SECONDS.sleep(awitTime1);
                   System.out.println("task1 is end!");
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
           };
   
   
           Runnable task2 = () -> {
               try {
                   System.out.println("task2 is start!");
                   TimeUnit.SECONDS.sleep(awitTime2);
                   System.out.println("task2 is end!");
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
           };
           //执行task1
           pool.execute(task1);
   
           for (int i = 0; i < 200; i++) {
               pool.execute(task2);
           }
           //关闭线程池
           pool.shutdown();
   
           try {
               //如果等待的线程没有执行完成
               if(!pool.awaitTermination(awitTime2,TimeUnit.SECONDS)){
                   // 超时的时候向线程池中所有的线程发出中断(interrupted)。  
                   pool.shutdownNow();
               }
           } catch (InterruptedException e) {
               pool.shutdownNow();
           }
       }
   }
   ```

   ​	从上面的代码中可以看出要想安全的停掉一个线程池，首先调用`shutdown()`方法停止接收新的线程任务，然后判断阻塞等待的线程是否处理完成，也就是平时所说的在途业务是否处理完成。规定的阻塞等待时间内没有完成的线程将通过调用`shutdownNow()`方法强行中断。

   ​	下面再来看下线程执行跟踪的相关方法：

   ```java
   /**
    * 提交一个可执行的任务，返回一个Future代表这个任务
    * 等到任务成功执行，Future#get()方法会返回null
    * 注意，future.get()方法会产生阻塞。
    */
   Future<?> submit(Runnable task);
    
   /**
    * 提交一个可以执行的任务，返回一个Future代表这个任务
    * 等到任务执行结束，Future#get()方法会返回这个给定的result
    */
   <T> Future<T> submit(Runnable task, T result);
    
   /**
    * 提交一个有返回值的任务，并返回一个Future代表等待的任务执行的结果
    * 等到任务成功执行，Future#get()方法会返回任务执行的结果
    */
   <T> Future<T> submit(Callable<T> task);
   ```

   `submit(Runnable)`和`execute(Runnable)`区别是前者可以返回一个**Future**对象，通过返回的Future对象，我们可以检查提交的任务是否执行完毕。`submit(Callable)`和`submit(Runnable)`类似，也会返回一个Future对象，但是除此之外，submit(Callable)接收的是一个Callable的实现，Callable接口中的`call()`方法有一个返回值，可以返回任务的执行结果，而Runnable接口中的`run()`方法是`void`的，没有返回值 

3. ScheduledExecutorService

   ```java
   /**
    * 在给定延时后，创建并执行一个一次性的Runnable任务
    * 任务执行完毕后，ScheduledFuture#get()方法会返回null
    */
   public ScheduledFuture<?> schedule(Runnable command, long delay, TimeUnit unit);
    
   /**
    * 在给定延时后，创建并执行一个ScheduledFutureTask
    * ScheduledFuture 可以获取结果或取消任务
    */
   public <V> ScheduledFuture<V> schedule(Callable<V> callable, ong delay, TimeUnit unit);
    
   /**
    * 创建并执行一个在给定初始延迟后首次启用的定期操作，后续操作具有给定的周期
    * 也就是将在 initialDelay 后开始执行，然后在 initialDelay+period 后执行，接着在 initialDelay + 2 * period 后执行，依此类推
    * 如果执行任务发生异常，随后的任务将被禁止，否则任务只会在被取消或者Executor被终止后停止
    * 如果任何执行的任务超过了周期，随后的执行会延时，不会并发执行
    */
   public ScheduledFuture<?> scheduleAtFixedRate(Runnable command,
                                                     long initialDelay,
                                                     long period,
                                                     TimeUnit unit);
    
   /**
    * 创建并执行一个在给定初始延迟后首次启用的定期操作，随后，在每一次执行终止和下一次执行开始之间都存在给定的延迟
    * 如果执行任务发生异常，随后的任务将被禁止，否则任务只会在被取消或者Executor被终止后停止
    */
   public ScheduledFuture<?> scheduleWithFixedDelay(Runnable command,
                                                        long initialDelay,
                                                        long delay,
                                                        TimeUnit unit);
   ```

   #### ThreadPoolExecutor

   ​	先来看下ThreadPoolExecutor的构造函数。

   ```java
   public ThreadPoolExecutor(int corePoolSize,
                             int maximumPoolSize,
                             long keepAliveTime,
                             TimeUnit unit,
                             BlockingQueue<Runnable> workQueue,
                             ThreadFactory threadFactory,
                             RejectedExecutionHandler handler) {
       if (corePoolSize < 0 ||
           maximumPoolSize <= 0 ||
           maximumPoolSize < corePoolSize ||
           keepAliveTime < 0)
           throw new IllegalArgumentException();
       if (workQueue == null || threadFactory == null || handler == null)
           throw new NullPointerException();
       this.acc = System.getSecurityManager() == null ?
               null :
               AccessController.getContext();
       this.corePoolSize = corePoolSize;
       this.maximumPoolSize = maximumPoolSize;
       this.workQueue = workQueue;
       this.keepAliveTime = unit.toNanos(keepAliveTime);
       this.threadFactory = threadFactory;
       this.handler = handler;
   }
   ```

   | 参数名          | 参数作用                                                     |
   | --------------- | ------------------------------------------------------------ |
   | corePoolSize    | 核心线程数量也就是线程池中最小数量                           |
   | maximumPoolSize | 线程池中允许的最大线程池数量                                 |
   | keepAliveTime   | 空闲线程存活时间                                             |
   | unit            | 空闲线程存活时间单位                                         |
   | workQueue       | 线程池中使用的缓冲队列（ workQueue必须是BlockingQueue阻塞队列 ） |
   | threadFactory   | 执行程序创建新线程时要使用的线程工厂                         |
   | handler         | 线程池对拒绝任务的处理策略                                   |

   **小结：**

   * 如果线程池中运行的线程数量小于 < corePoolSize，即使线程池中的线程都属于空闲状态，也要创建新的线程来处理被添加的任务。如果执行了线程池的prestartAllCoreThreads()方法，线程池会提前创建并启动所有核心线程。 
   * 如果线程池中运行的线程数量大于或等于≥ corePoolSize,但缓冲队列workQueue未满，那么新添加的任务将被放入缓冲队列中等待被执行。
   * 如果线程池中运行的线程数量大于 > corePoolSize同时缓冲队列workQueue已满，并且线程池中的数量小于maximumPoolSize，则通过新建线程来处理新添加的任务。
   * 如果线程池中运行的线程数量大于 > corePoolSize同时缓冲队列workQueue已满，并且线程池中的数量等于maximumPoolSize，则通过handler所指定的策略来处理任务。
   * 当线程池中运行的线程数量大于 > corePoolSize，如果某条线程的空闲时间超过keepAliveTime，那么这条线程将被终止，这样线程池就可以动态的调整线程数量。

   *这里主要介绍一下workQueue几种排队策略：*

    * 有界队列

      ArrayBlockingQueue是基于数组结构的有界队列(FIFO，first in first out)，可以指定队列的最大长度。使用有界队列可以防止资源被耗尽，但也会造成超过队列大小和maximumPoolSize后，提交的任务会被拒绝的问题，使用过程中比较难调整和控制。

    * 无界队列

      LinkedBlockingQueue是基于链表结构的无界队列(FIFO)，理论上该队列可以对无限多的任务排队。在所有核心线程corePoolSize都工作的情况下新添加的任务将配分配到队列之中，创建的线程数量就不会超过maximumPoolSize，也因此maximumPoolSize值就无效了，但是这样会有耗尽资源的风险。实际应用场景中可能会造成雪崩效果。

    * 不排队，直接提交

      SynchronousQueue 就是讲任务直接交给线程执行而不保存他们。如果线程池中的线程都在运行当中那么试图把任务加入缓冲队列将会失败，因此会创建一个新的线程执行任务并加入线程池中(corePoolSize-->maximumPoolSize扩容的过程)。Executors.newCachedThreadPool()采用的便是这种策略 。





http://www.cnblogs.com/trust-freedom/p/6594270.html#label_1_3







## 4、Stopwatch

​	如文档`nanoTime`所述，返回的值没有绝对含义，只能解释为相对于`nanoTime`在不同时间返回的另一个时间戳。`Stopwatch`是一种更有效的抽象，因为它只揭示这些相对值，而不是绝对值。

```java
package com.nucc.govern;

import com.google.common.base.Stopwatch;

import static java.util.concurrent.TimeUnit.MILLISECONDS;

/**
 * @description: StopWatch任务执行时间监视器
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/6/5 20:08
 * @version: 1.0.0
 */
public class StopwatchTest {

    public static void main(String[] args) throws InterruptedException {
        /*
        * 以纳秒为单位测量已用时间的对象
        */

        //创建（并开始）使用System.nanoTime（）作为其时间源的新秒表。
        Stopwatch stopwatch = Stopwatch.createStarted();
        Thread.sleep(1000);
        System.out.println("time: " + stopwatch);

        Thread.sleep(2000);
        //返回此秒表上显示的当前经过时间，以所需时间单位表示，其中任何小数部分向下舍入
        long millis = stopwatch.elapsed(MILLISECONDS);
        System.out.println("elapsed：" + millis);
        System.out.println("time：" + stopwatch);

        //将此秒表的经过时间设置为零，并将其置于停止状态。
        stopwatch.reset();
        System.out.println("reset：" + stopwatch);

        //启动秒表
        stopwatch.start();
        Thread.sleep(3000);
        System.out.println("start：" + stopwatch);

        //停止秒表
        System.out.println("isRunning："+stopwatch.isRunning());
        stopwatch.stop();
        System.out.println("isRunning："+stopwatch.isRunning());
        Thread.sleep(3000);
        System.out.println("stop：" + stopwatch);

    }


}
```

![1528201776510](http://oy48q6kwm.bkt.clouddn.com/d7dad14c34ab8aa6418cfd48172fb26a.png)

## 5、ConfigFactory

​	Typesafe的Config库，纯Java写成、零外部依赖、代码精简、功能灵活、API友好。支持Java properties、JSON、JSON超集格式HOCON以及环境变量。 

```java
package com.nucc.channel.gorges.core.common.config;

import java.io.File;
import java.util.List;
import java.util.Map;
import java.util.Objects;

import com.typesafe.config.Config;
import com.typesafe.config.ConfigFactory;
import com.typesafe.config.ConfigParseOptions;
import com.typesafe.config.ConfigRenderOptions;

/**
 * Gorges 公共配置中心,这里是做一个typesafe的封装,后续可以按照需求更改实现
 *
 * @author corner
 */
public class Configuration implements java.io.Serializable {

    /**
     * serial id
     */
    private static final long serialVersionUID = 470414124040013890L;
    private Config config = null;

    /**
     * ConfigFactory.load()会加载配置文件，默认加载classpath下的application.conf,application.json和application.properties文件。
     * 当然也可以调用ConfigFactory.load(confFileName)加载指定的配置文件。
     */
    public Configuration() {
        this(ConfigFactory.load());
    }

    private Configuration(Config config) {
        this.config = config;
    }

    public String getString(String path) {
        return config.getString(path);
    }

    public String getString(String path, String defaultValue) {
        String value = getString(path);
        return Objects.isNull(value) ? defaultValue : value;
    }

    public boolean hasPath(String path) {
        return config.hasPath(path);
    }

    public Configuration getConfig(String path) {
        Config value = config.getConfig(path);
        return Objects.isNull(value) ? null : new Configuration(value);
    }

    public int getInt(String path) {
        return config.getInt(path);
    }

    public long getLong(String path) {
        return config.getLong(path);
    }

    public Configuration withFallback(Configuration paramConfigMergeable) {
        return new Configuration(
                config.withFallback(paramConfigMergeable.config));
    }

    public boolean getBoolean(String path) {
        return config.getBoolean(path);
    }

    public static Configuration parseMap(Map<String, ? extends Object> values) {
        return Objects.isNull(values) ? new Configuration()
                : new Configuration(ConfigFactory.parseMap(values));
    }
	//获取Config作为ConfigObject的树。这是一个恒定时间操作（它与Config中的数值不成比例）
    public String config() {
        return config.root().render(ConfigRenderOptions.concise());
    }

    public List<String> getStringList(String path) {
        return config.getStringList(path);
    }

    public Map<String, Object> unwrapped() {
        return config.root().unwrapped();
    }

    public Configuration withValue(String path, Map<String, Object> value) {
        return new Configuration(config.withValue(path,
                ConfigFactory.parseMap(value).root()));
    }

    public static Configuration parseString(String s) {
        return new Configuration(ConfigFactory.parseString((String) s,
                ConfigParseOptions.defaults()));
    }

    public Map getObject(String path){
		return config.getObject(path);
	}

    public static Configuration parseFile(File file) {
        return new Configuration(ConfigFactory.parseFile(file));
    }

}

```

​	如果多个config 文件有冲突时，解决方案有: 1. a.withFallback(b) //a和b合并，如果有相同的key，以a为准  2. a.withOnlyPath(String path) //只取a里的path下的配置 3. a.withoutPath(String path) //只取a里出path外的配置 

## 6、Annotation

​	[java.lang.annotation](https://baike.baidu.com/item/java.lang.annotation)，接口 Annotation。对于Annotation，是Java5的新特性，JDK5引入了Metadata（元数据）很容易的就能够调用Annotations。Annotations提供一些本来不属于程序的数据，比如：一段[代码](https://baike.baidu.com/item/%E4%BB%A3%E7%A0%81)的作者或者告诉[编译器](https://baike.baidu.com/item/%E7%BC%96%E8%AF%91%E5%99%A8)禁止一些特殊的错误。An annotation 对代码的执行没有什么影响。Annotations使用@annotation的形式应用于代码：类(class),属性(attribute),方法(method)等等。一个Annotation出现在上面提到的开始位置，而且一般只有一行，也可以包含有任意的参数。 

​	注解通过 `@interface` 关键字进行定义。 

```java
/**
 *  定义注解
 */
public @interface AnnotationTest {
    int id() default -1;
    String msg();
}
```

​	注解的应用

```java
@AnnotationTest(id=1,msg="hello annotation")
public class Test {
}
```

	### 6.1 元注解

​	注解annotation可以抽象的理解为是一个标签，AnnotationTest就是定义了一个标签，让后将这个标签贴到Test类上，时Test类具备了annotationTest标签提供的属性或者能力。要想让annotation正常工作还需要加入一些元注解，元注解是可以注解到注解上的注解，或者说元注解是一种基本注解，但是它能够应用到其它的注解上面 。

* @Retention

  Retention的英文是保留期的意思。当@Retention作用到一个注解上的时候，它解释说明了这个注解的存活时间。

  * RetentionPolicy.SOURCE    注解只在源码阶段保留，在编译器进行编译时它将被丢弃忽视。  
  * RetentionPolicy.CLASS       注解只被保留到编译进行的时候，它并不会被加载到 JVM 中。(缺省值)
  * RetentionPolicy.RUNTIME   注解可以保留到程序运行的时候，它会被加载进入到 JVM 中，所以在程序运行时可以通过反射获取到它们。    

  可以把@Retention理解成是这张标签的有效期，例如标签上记录了某天你要给某人过生日，那么这张标签的存在意义就是生日日期这一天，再往后就没有意思了。

* @Documented

  顾名思义，这个元注解肯定是和文档有关。它的作用是能够将注解中的元素包含到 Javadoc 中去。 

* @Target

  Target 是目标的意思，@Target 指定了注解运用的地方。当注解类型声明中没有@Target元注解，则默认可以适用所有的程序元素。 

  - ElementType.ANNOTATION_TYPE	  注解类型声明，可以给一个注解进行注解 
  - ElementType.CONSTRUCTOR    构造方法声明
  - ElementType.FIELD    字段声明（包括枚举常量）
  - ElementType.LOCAL_VARIABLE     局部变量
  - ElementType.METHOD   方法注解
  - ElementType.PACKAGE   包路径注解
  - ElementType.PARAMETER   方法内参数注解
  - ElementType.TYPE  可以给一个类型进行注解，比如类、接口、枚举

* @Inherited

  Inherited是遗传、继承的意思，但并不是说这个注解本身可以被继承，而是说如果一个父类被@Inherited注解了，并且如果这个父类的子类没有使用任何注解的时候，那么这个子类将继承父类的注解。

  ```java
  @Inherited
  @Retention(RetentionPolicy.RUNTIME)
  @interface Test {}
  
  ```

  ```java
  @Test
  public class A {}
  ```

  ```java
  public class B extends A {}
  ```

  注解 Test 被 @Inherited 修饰，之后类 A 被 Test 注解，类 B 继承 A,类 B 也拥有 Test 这个注解。 

* @Repeatable

  Repeatable是jdk1.8新增的重复注解，就是允许在同一申明类型（类，属性，或方法）上多次使用同一个注解 。

  ```java
  @interface Persons {
      Person[]  value();
  }
  
  @Repeatable(Persons.class)
  @interface Person{
      String role default "";
  }
  
  
  @Person(role="artist")
  @Person(role="coder")
  @Person(role="PM")
  public class SuperMan{
  }
  ```

  @Repeatable 注解了 Person。而 @Repeatable 后面括号中的Persons类相当于一个容器注解,Persons本身也是一个注解同时它可以用来存储其他的注解。它里面必须要有一个 value 的属性，属性类型是一个被 @Repeatable 注解过的注解数组，注意它是数组 。

### 6.2 注解属性

​	注解的属性也叫作成员变量。注解只有成员变量没有方法。注解的环境变量在注解定义中以“无形参的方法”形式来声明，其方法名定义了该成员变量的名称，其返回值定义了该成员变量的类型。

最开始的例子中的AnnotationTest注解拥有id、msg两个属性，属性的类型分别是int、string。在使用@AnnotationTest(id=1,msg="hello annotation")时通过括号内value=""形式赋值.需要注意的是注解中定义的属性必须是8中基本类型外加类、接口、注解以及他们的数组，注解中的属性可以通过default关键词设置默认值。另外，还有一种情况。如果一个注解内仅仅只有一个名字为 value 的属性时，应用这个注解时可以直接接属性值填写到括号内。 

```java
public @interface Check {
    String value();
}

@Check("hi")
int a;

//等价于
@Check(value="hi")
int b;
```

最后，还需要注意的一种情况是一个注解没有任何属性。比如 

```java
public @interface Perform {}
```

那么在应用这个注解的时候，括号都可以省略。 

```java
@Perform
public void testMethod(){}
```

### 6.3 内置注解

* @Deprecated：标识被标记的元素已过时。编译器在编译阶段遇到这个注解时会发出提醒警告，告诉开发者正在调用一个过时的元素比如过时的方法、过时的类、过时的成员变量。 

* @Override：方法重写，提示子类要复写父类中被 @Override 修饰的方法 。

* @SuppressWarnings：阻止警告。通过该注解可以忽略编译器的警告提醒。

* @SafeVarargs：参数安全类型注解。它的目的是提醒开发者不要用参数做一些不安全的操作,它的存在会阻止编译器产生 unchecked 这样的警告。它是在 Java 1.7 的版本中加入的。 

  ```java
  @SafeVarargs // Not actually safe!
      static void m(List<String>... stringLists) {
      Object[] array = stringLists;
      List<Integer> tmpList = Arrays.asList(42);
      array[0] = tmpList; // Semantically invalid, but compiles without warnings
      String s = stringLists[0].get(0); // Oh no, ClassCastException at runtime!
  }
  ```

  上面的代码中，编译阶段不会报错，但是运行时会抛出 ClassCastException 这个异常，所以它虽然告诉开发者要妥善处理，但是开发者自己还是搞砸了。Java 官方文档说，未来的版本会授权编译器对这种不安全的操作产生错误警告。

* @FunctionalInterface：函数式接口注解，这个是 Java 1.8 版本引入的新特性。所谓的函数式接口，当然首先是一个接口，然后就是在这个接口里面**只能有一个抽象方法**。 这种类型的接口也称为SAM接口，即Single Abstract Method interfaces。 它们主要用在Lambda表达式和方法引用（实际上也可认为是Lambda表达式）上。 

  ```java
    @FunctionalInterface
    interface GreetingService{
        void sayMessage(String message);
    }
  ```

  ==提醒：加不加@FunctionalInterface对于接口是不是函数式接口没有影响，该注解知识提醒编译器去检查该接口是否仅包含一个抽象方法== .

  函数式接口里是可以包含默认方法，因为默认方法不是抽象方法，其有一个默认实现，函数式接口里是可以包含静态方法，因为静态方法不能是抽象方法，是一个已经实现了的方法，所以是符合函数式接口的定义的:

  ```java
  @FunctionalInterface
  interface GreetingService {
      //一个抽象方法
      void sayMessage(String message);
      default void doSomeMoreWork1(){
              // 默认方法1
      }
      default void doSomeMoreWork2(){
              // 默认方法2
      }
      //可以包含静态方法
      static void printHello(){
          System.out.println("Hello");
      }
  }
  ```

  函数是接口里也允许定义java.lang.Object里的Public方法，这些方法对于函数式接口来说，不被当成是抽象方法（虽然它们是抽象方法）；因为任何一个函数式接口的实现，默认都继承了Object类，包含了来自java.lang.Object里对这些抽象方法的实现； 

  ```java
      @FunctionalInterface
      interface GreetingService  
      {
          void sayMessage(String message);
          
          @Override
          boolean equals(Object obj);
      }
  ```




## 7、泛型



## 8、JDK内存排查



## 9、Greys/dubbo/nmong



## 10、死锁

























































