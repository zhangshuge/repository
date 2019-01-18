---
title: druid
date: 2018-06-12 19:17:09
categories: java
tags: java
---

# 概述
Druid是阿里巴巴开源的一个Java语言数据库连接池 [GitHub地址](https://github.com/alibaba/druid)。Druid能够提供强大的监控和扩展功能。

# 性能对比

测试执行申请归还连接1,000,000（一百万）次总耗时性能对比。 

| Jdbc Connection Pool | 1 thread | 2 threads | 5 threads         | 10 threads | 20 threads        | 50 threads         |
| -------------------- | -------- | --------- | ----------------- | ---------- | ----------------- | ------------------ |
| Druid                | 898      | 1,191     | 1,324             | 1,362      | 1,325             | 1,459              |
| tomcat-jdbc          | 1,269    | 1,378     | 2,029             | 2,103      | 1,879             | 2,025              |
| DBCP                 | 2,324    | 5,055     | 5,446             | 5,471      | 5,524             | 5,415              |
| BoneCP               | 3,738    | 3,150     | 3,194             | 5,681      | 11,018            | 23,125             |
| jboss-datasource     | 4,377    | 2,988     | 3,680             | 3,980      | 32,708            | 37,742             |
| C3P0                 | 10,841   | 13,637    | 10,682            | 11,055     | 14,497            | 20,351             |
| Proxool              | 16,337   | 16,187    | 18,310(Exception) | 25,945     | 33,706(Exception) | 39,501 (Exception) |

# 监控

druid号称为监控而生的数据库连接池，内置提供了一个StatViewServlet用于展示Druid的统计信息。 除了提供HTML监控页面StatViewServlet还提供了监控信息的JSON格式API。已下demo是在springboot中的配置:

```properties
## druid 监控
spring.datasource.druid.web-stat-filter.enabled=true
spring.datasource.druid.web-stat-filter.url-pattern=/*
spring.datasource.druid.web-stat-filter.exclusions=*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*
## druid 监控页面
spring.datasource.druid.stat-view-servlet.enabled=true
spring.datasource.druid.stat-view-servlet.url-pattern=/druid/*
spring.datasource.druid.stat-view-servlet.login-username=admin
spring.datasource.druid.stat-view-servlet.login-password=admin
# 配置监控统计拦截的filters，去掉后监控界面sql无法统计，'wall'用于防火墙
spring.datasource.filters=stat,wall,log4j
# 通过connectProperties属性来打开mergeSql功能；慢SQL记录
spring.datasource.connectionProperties=druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000
```

这里的slowSqlMills即为慢SQL的判定时间，缺省值为3000ms。访问[内置监控演示](http://120.26.192.168/druid/index.html)

**登录页面**

![1528112457080](http://oy48q6kwm.bkt.clouddn.com/ee0fa92f97c04ff42980114bb65aab0b.png)

**首页**

![7080](http://oy48q6kwm.bkt.clouddn.com/360a2ad756a6f591d476666ec20af9e9.png)

**数据源**

![1528112546505](http://oy48q6kwm.bkt.clouddn.com/bdbbfb9e816858468d1aca4f61c48b17.png)

**SQL监控**

![1528110735860](http://oy48q6kwm.bkt.clouddn.com/8263f54dafb23db72466206d5b177f61.png)

URL监控

![1528116492169](http://oy48q6kwm.bkt.clouddn.com/f6e7912e173a4372da5859a59bd2dc64.png)

# 可扩展性Filter-Chain

DruidDataSource支持通过Filter-Chain模式进行扩展，类似Serlvet的Filter，扩展十分方便，可以拦截任何JDBC的方法。 Filter主要重新定义了来自Connection、Statement、ResultSet等对象的接口，并且通过对应的Proxy对象来代替，每个接口中还带有一个FilterChain参数，用于支持Filter链。以下代码省略了一些方法：

```java
public interface Filter extends Wrapper {
    /**
     * 初始化Filter
     * @param dataSource
     */
    void init(DataSourceProxy dataSource);

    /**
     * 显示的销毁Filter
     */
    void destroy();

    /**
     * 读取properties配置文件
     * @param properties
     */
    void configFromProperties(Properties properties);

    boolean isWrapperFor(java.lang.Class<?> iface);

    <T> T unwrap(java.lang.Class<T> iface);

    /**
     * 创建一个连接
     * @param chain 拦截器链
     * @param info  配置信息
     * @return  返回ConnectionProxy代理对象
     * @throws SQLException
     */
    ConnectionProxy connection_connect(FilterChain chain, Properties info) throws SQLException;

    StatementProxy connection_createStatement(FilterChain chain, ConnectionProxy connection) throws SQLException;

    PreparedStatementProxy connection_prepareStatement(FilterChain chain, ConnectionProxy connection, String sql)
        
    // / statement相关方法

    /**
     * 执行查询操作
     * @param chain
     * @param statement
     * @param sql
     * @return
     * @throws SQLException
     */
    ResultSetProxy statement_executeQuery(FilterChain chain, StatementProxy statement, String sql) throws SQLException;

    /**
     * 执行更新操作
     * @param chain
     * @param statement
     * @param sql
     * @return
     * @throws SQLException
     */
    int statement_executeUpdate(FilterChain chain, StatementProxy statement, String sql) throws SQLException;
    
    // ResultSet 相关方法

    /**
     * 获取下一条数据
     * @param chain
     * @param resultSet
     * @return
     * @throws SQLException
     */
    boolean resultSet_next(FilterChain chain, ResultSetProxy resultSet) throws SQLException;

    /**
     * 关闭ResultSet
     * @param chain
     * @param resultSet
     * @throws SQLException
     */
    void resultSet_close(FilterChain chain, ResultSetProxy resultSet) throws SQLException;
}
```

​	同Filter类似，FilterChain也是定义了Connection，Statement，ResultSet等对象的相关接口，只是在实际调用这些对象前，会先执行一遍配置的Filter链。 Druid提供了一些可选的Filter,存放在META-INF/druid-filter.properties中 

```properties
druid.filters.default=com.alibaba.druid.filter.stat.StatFilter
druid.filters.stat=com.alibaba.druid.filter.stat.StatFilter
druid.filters.mergeStat=com.alibaba.druid.filter.stat.MergeStatFilter
druid.filters.counter=com.alibaba.druid.filter.stat.StatFilter
druid.filters.encoding=com.alibaba.druid.filter.encoding.EncodingConvertFilter
druid.filters.log4j=com.alibaba.druid.filter.logging.Log4jFilter
druid.filters.log4j2=com.alibaba.druid.filter.logging.Log4j2Filter
druid.filters.slf4j=com.alibaba.druid.filter.logging.Slf4jLogFilter
druid.filters.commonlogging=com.alibaba.druid.filter.logging.CommonsLogFilter
druid.filters.commonLogging=com.alibaba.druid.filter.logging.CommonsLogFilter
druid.filters.wall=com.alibaba.druid.wall.WallFilter
druid.filters.config=com.alibaba.druid.filter.config.ConfigFilter
```

* StatFilter:	主要负责对连接池监控操作，统计监控信息参考[StatFilter](https://github.com/alibaba/druid/wiki/%E9%85%8D%E7%BD%AE_StatFilter)。

* LogFilter：  内置提供了四种LogFilter（Log4jFilter、Log4j2Filter、CommonsLogFilter、Slf4jLogFilter），这样开发人员就可以自由配置需要在哪些JDBC操作上进行日志记录，比如数据源，数据库连接等， 详细配置参考[LogFilter](https://github.com/alibaba/druid/wiki/%E9%85%8D%E7%BD%AE_LogFilter)。

* ConfigFilter：主要负责从配置文件中读取配置，同时也支持向远程服务发送http请求获取配置（配置文件外化时使用）。常用一个常用的功能就是对数据库密码进行加密。

* WallFilter：防御SQL注入攻击。参考[wallfilter](https://github.com/alibaba/druid/wiki/%E9%85%8D%E7%BD%AE-wallfilter)。

* EncodingConvertFilter：主要用于当客户端编码不一致时，使用较少，除非一些遗留问题(oracle－mysql)，应保证客户端与服务端使用的编码一致。 

* MergeStatFilter：提供合并参数化SQL统计功能。

   SELECT * FROM t FROM id = 1; 

   SELECT * FROM t FROM id = 2;

  参数化为 select * from t where id = ?然后作为一条语句来统计。  

*  WebStatFilter：用于采集web-jdbc关联监控的数据，即通过Servlet容器中的Filter来作相关的收集及监控，详细配置可 参考[配置_配置WebStatFilter](https://github.com/alibaba/druid/wiki/%E9%85%8D%E7%BD%AE_%E9%85%8D%E7%BD%AEWebStatFilter)

下面我们做一个Demo实现一个自定义Filter：

```java
@Component
public class MyFilter extends FilterEventAdapter{

    @Override
    protected void statementExecuteAfter(StatementProxy statement, String sql, boolean result) {
        super.statementExecuteAfter(statement, sql, result);
    }

}
```

配置的Filter会在获取到连接后再被执行，并且Filter的执行顺序与配置的的顺序相反，即Slf4jLogFilter更先执行。 

# 分库分表

​	Druid打算在0.2.9之后的版本开始提供分库分表的功能，由于没有项目支撑，这部分功能的成熟度不够，更多是试验性质，为其他的框架提供基础设施，不建议在生产环境直接使用。生产环境使用分库分表，建议使用淘宝的tddl或者cobar。 阿里云的drds/sharding jdbc。（村长也讲过CDS）



# 常规配置

```properties
## datasource 配置
spring.datasource.type = com.alibaba.druid.pool.DruidDataSource
spring.datasource.druid.url = jdbc:mysql://xx.xx.xx.xx:3306/zhangchi?useUnicode=true&characterEncoding=utf-8&useSSL=false
spring.datasource.druid.username = root
spring.datasource.druid.password = root
spring.datasource.druid.driver-class-name = com.mysql.jdbc.Driver


### 连接池最大、最小、初始化数量
spring.datasource.druid.initial-size = 1
spring.datasource.druid.min-idle = 1
spring.datasource.druid.max-active = 20
### 获取连接时最大等待时间，单位毫秒。配置了maxWait之后，缺省启用公平锁，并发效率会有所下降，如果需要可以通过配置useUnfairLock属性为true使用非公平锁。
spring.datasource.druid.max-wait = 6000
### 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒Destroy线程会检测连接的间隔时间，如果连接空闲时间大于等于minEvictableIdleTimeMillis则关闭物理连接。
spring.datasource.druid.time-between-eviction-runs-millis = 6000
### 配置一个连接在池中最小生存的时间，单位是毫秒(5分钟)
spring.datasource.druid.min-evictable-idle-time-millis = 300000
### 用来检测连接是否有效的sql，要求是一个查询语句，常用select 'x'。如果validationQuery为null，testOnBorrow、testOnReturn、testWhileIdle都不会起作用。
spring.datasource.druid.validation-query = select 'x'
### 建议配置为true，不影响性能，并且保证安全性。申请连接的时候检测，如果空闲时间大于timeBetweenEvictionRunsMillis，执行validationQuery检测连接是否有效。
spring.datasource.druid.test-while-idle = true
### 申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。
spring.datasource.druid.test-on-borrow = false
### 归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。
spring.datasource.druid.test-on-return = false





## druid 监控
spring.datasource.druid.web-stat-filter.enabled=true
spring.datasource.druid.web-stat-filter.url-pattern=/*
spring.datasource.druid.web-stat-filter.exclusions=*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*
## druid 监控页面
spring.datasource.druid.stat-view-servlet.enabled=true
spring.datasource.druid.stat-view-servlet.url-pattern=/druid/*
spring.datasource.druid.stat-view-servlet.login-username=admin
spring.datasource.druid.stat-view-servlet.login-password=admin
# 配置监控统计拦截的filters，去掉后监控界面sql无法统计，'wall'用于防火墙
spring.datasource.filters=stat,wall,log4j
# 通过connectProperties属性来打开mergeSql功能；慢SQL记录
spring.datasource.connectionProperties=druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000
```

# 核心代码

## 1、创建连接

通过springboot创建连接，springboot对DataSource进行了一层轻薄的封装。
```java
/**
 * @description: 连接druid
 * @author: zhangchi
 * @email: zhangchi@nucc.com
 * @datetime: 2018/5/19 14:41
 * @version: 1.0.0
 */
@Component
public class DruidConnet {
    @Primary
    @Bean
    public DataSource dataSource(){
        return DruidDataSourceBuilder.create().build();
    }
}
```
DruidDataSourceBuilder类只是扩展了对springboot 1.X版本中的 .properties 内配置属性不能按照配置声明顺序进行绑定，进而导致配置出错而提供的方法。同时创建DruidDataSourceWrapper类，该类扩展支持spring前缀。
```java
@Override
  public void afterPropertiesSet() throws Exception {
      //if not found prefix 'spring.datasource.druid' jdbc properties ,'spring.datasource' prefix jdbc properties will be used.
      if (super.getUsername() == null) {
          super.setUsername(basicProperties.determineUsername());
      }
      if (super.getPassword() == null) {
          super.setPassword(basicProperties.determinePassword());
      }
      if (super.getUrl() == null) {
          super.setUrl(basicProperties.determineUrl());
      }
      if(super.getDriverClassName() == null){
          super.setDriverClassName(basicProperties.getDriverClassName());
      }

  }
```
DataSource接口是连接管理的父接口。DruidDataSource继承了DruidAbstractDataSource类并实现了DataSource接口。
```java
package javax.sql;

import java.sql.Connection;
import java.sql.SQLException;
import java.sql.Wrapper;

public interface DataSource  extends CommonDataSource, Wrapper {

  Connection getConnection() throws SQLException;

  Connection getConnection(String username, String password)
    throws SQLException;
}

```
![](http://oy48q6kwm.bkt.clouddn.com/926ba822ac19161889fa093f0bad2f68.png)
以上几个类就是druid核心的连接管理类，下面看下具体的getConnection()实现。
```java
@Override
public DruidPooledConnection getConnection() throws SQLException {
    return getConnection(maxWait);
}

public DruidPooledConnection getConnection(long maxWaitMillis) throws SQLException {
    //初始化数据源
    init();

    if (filters.size() > 0) {
        // 经过filter中获取连接
        // 这里是每次获取连接，都需要构造Filter链，即执行各Filter
        FilterChainImpl filterChain = new FilterChainImpl(this);
        return filterChain.dataSource_connect(this, maxWaitMillis);
    } else {
        //直接获取连接
        return getConnectionDirect(maxWaitMillis);
    }
}
```
```java
@Override
public DruidPooledConnection dataSource_connect(DruidDataSource dataSource, long maxWaitMillis) throws SQLException {
    if (this.pos < filterSize) {
        //还有未执行的Filter，则先执行Filter.dataSource_getConnection()
        DruidPooledConnection conn = nextFilter().dataSource_getConnection(this, dataSource, maxWaitMillis);
        return conn;
    }

    return dataSource.getConnectionDirect(maxWaitMillis);
}
```

maxWaitMillis最大的超时时间。先调用init()初始化

```java
{
	//使用重入锁
    final ReentrantLock lock = this.lock;
    try {
        lock.lockInterruptibly();
    } catch (InterruptedException e) {
        throw new SQLException("interrupt", e);
    }
    try {
        initStackTrace = Utils.toString(Thread.currentThread().getStackTrace());
      /**
	    * 获取数据源ID，多数据源时会大于1
	    */
        this.id = DruidDriver.createDataSourceId();
        if (this.id > 1) {
            long delta = (this.id - 1) * 100000;
            this.connectionIdSeedUpdater.addAndGet(this, delta);
            this.statementIdSeedUpdater.addAndGet(this, delta);
            this.resultSetIdSeedUpdater.addAndGet(this, delta);
            this.transactionIdSeedUpdater.addAndGet(this, delta);
        }

       /**
        * 执行拦截器初始化DataSourceProxy
        */
        for (Filter filter : filters) {
            filter.init(this);
        }

    	//创建存放连接数组
        connections = new DruidConnectionHolder[maxActive];
        //当maxActive被修改时，执行shrink()函数缩容时使用
        evictConnections = new DruidConnectionHolder[maxActive];
        //当maxActive被修改时，执行shrink()函数扩容时使用
        keepAliveConnections = new DruidConnectionHolder[maxActive];

        SQLException connectError = null;

        if (createScheduler != null) {
            for (int i = 0; i < initialSize; ++i) {
                createTaskCount++;
                CreateConnectionTask task = new CreateConnectionTask(true);
                this.createSchedulerFuture = createScheduler.submit(task);
            }
        } else if (!asyncInit) {
            try {
                // init connections
                for (int i = 0; i < initialSize; ++i) {
                    //创建真正的数据库连接池
                    PhysicalConnectionInfo pyConnectInfo = createPhysicalConnection();
                    DruidConnectionHolder holder = new DruidConnectionHolder(this, pyConnectInfo);
                    connections[poolingCount] = holder;
                    incrementPoolingCount();
                }

                if (poolingCount > 0) {
                    poolingPeak = poolingCount;
                    poolingPeakTime = System.currentTimeMillis();
                }
            } catch (SQLException ex) {
                LOG.error("init datasource error, url: " + this.getUrl(), ex);
                connectError = ex;
            }
        }

        createAndLogThread();//开启创建日志跟踪的线程
        createAndStartCreatorThread();//开启创建数据库连接的线程
        createAndStartDestroyThread();//开启销毁数据库连接的线程

        initedLatch.await();//调用await()方法的线程会被挂起，它会等待直到count值为0才继续执行
        init = true;

        initedTime = new Date();
        registerMbean();

        if (connectError != null && poolingCount == 0) {
            throw connectError;
        }

        if (keepAlive) {
            // async fill to minIdle
            if (createScheduler != null) {
                for (int i = 0; i < minIdle; ++i) {
                    createTaskCount++;
                    CreateConnectionTask task = new CreateConnectionTask(true);
                    this.createSchedulerFuture = createScheduler.submit(task);
                }
            } else {
                this.emptySignal();
            }
        }

    } catch (SQLException e) {
        LOG.error("{dataSource-" + this.getID() + "} init error", e);
        throw e;
    } catch (InterruptedException e) {
        throw new SQLException(e.getMessage(), e);
    } catch (RuntimeException e){
        LOG.error("{dataSource-" + this.getID() + "} init error", e);
        throw e;
    } catch (Error e){
        LOG.error("{dataSource-" + this.getID() + "} init error", e);
        throw e;

    } finally {
        inited = true;
        lock.unlock();

        if (init && LOG.isInfoEnabled()) {
            String msg = "{dataSource-" + this.getID();

            if (this.name != null && !this.name.isEmpty()) {
                msg += ",";
                msg += this.name;
            }

            msg += "} inited";

            LOG.info(msg);
        }
    }
}
```

getConnectionDirect()调用getConnectionInternal()返回DruidPooledConnection对象。

```java
DruidConnectionHolder takeLast() throws InterruptedException, SQLException {
    try {
        while (poolingCount == 0) {//没有可用线程了
            emptySignal(); // send signal to CreateThread create connection

            if (failFast && failContinuous.get()) {
                throw new DataSourceNotAvailableException(createError);
            }

            notEmptyWaitThreadCount++;
            if (notEmptyWaitThreadCount > notEmptyWaitThreadPeak) {
                notEmptyWaitThreadPeak = notEmptyWaitThreadCount;
            }
            try {
                notEmpty.await(); // signal by recycle or creator
            } finally {
                notEmptyWaitThreadCount--;
            }
            notEmptyWaitCount++;

            if (!enable) {
                connectErrorCountUpdater.incrementAndGet(this);
                throw new DataSourceDisableException();
            }
        }
    } catch (InterruptedException ie) {
        notEmpty.signal(); // propagate to non-interrupted thread
        notEmptySignalCount++;
        throw ie;
    }

    decrementPoolingCount();
    DruidConnectionHolder last = connections[poolingCount];
    connections[poolingCount] = null;

    return last;
}
```

​	先判断池中的连接数，如果到0了，那么本线程就得被挂起，同时释放empty信号，并且等待notEmpty的信号。如果还有连接，就取出数组的最后一个，同时更改poolingCount。 当然如果当poolingCount不为0的时候，那么直接从连接数组中获取下标为poolingCount-1的连接返回就可以啦。 

　	最终我们对Connection的操作都是通过DruidPooledConnection来实现，比如commit、rollback等，它们大都是通过实际的数据库连接完成工作。DruidPooledConnection.close()关闭的核心函数是recycle()。

```java
public void recycle() throws SQLException {
    if (this.disable) {
        return;
    }

    DruidConnectionHolder holder = this.holder;
    if (holder == null) {
        if (dupCloseLogEnable) {
            LOG.error("dup close");
        }
        return;
    }

    if (!this.abandoned) {
        DruidAbstractDataSource dataSource = holder.getDataSource();
        dataSource.recycle(this);
    }

    this.holder = null;
    conn = null;
    transactionInfo = null;
    closed = true;
}
```

## 2、 SQL解析

​	SQL Parser是Druid的一个重要组成部分，Druid内置使用SQL Parser来实现防御SQL注入（[WallFilter](https://github.com/alibaba/druid/wiki/%E7%AE%80%E4%BB%8B_WallFilter)）、合并统计没有参数化的SQL([StatFilter](https://github.com/alibaba/druid/wiki/%E9%85%8D%E7%BD%AE_StatFilter)的mergeSql)、[SQL格式化](https://github.com/alibaba/druid/wiki/SQL%E6%A0%BC%E5%BC%8F%E5%8C%96)、分库分表。 Druid SQL Parser性能非常好，可以用于生产环境直接对SQL进行分析处理。 

​	Druid的sql parser是目前支持各种数据语法最完备的SQL Parser。目前对各种数据库的支持如下： 

| 数据库                                      | DML        | DDL           |
| ------------------------------------------- | ---------- | ------------- |
| [odps](https://www.aliyun.com/product/odps) | 完全支持   | 完全支持      |
| mysql                                       | 完全支持   | 完全支持      |
| postgresql                                  | 完全支持   | 完全支持      |
| oracle                                      | 支持大部分 | 支持大部分    |
| sql server                                  | 支持常用的 | 支持常用的ddl |
| db2                                         | 支持常用的 | 支持常用的ddl |
| hive                                        | 支持常用的 | 支持常用的ddl |

druid parser处理大约是600纳秒，也就是说单线程每秒可以处理1500万次以上。在1.1.3~1.1.4版本中，SQL Parser的性能有极大提升，完全可以适用于生产环境中对SQL进行处理。 

https://github.com/alibaba/druid/wiki/SQL-Parser