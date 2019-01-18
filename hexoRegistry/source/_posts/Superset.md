---
title: Superset
date: 2018-03-31 17:59:23
tags: superset
categories: BigData
---


# 简介superset安装使用
## 基础组件
### Flask
Python 几大著名 Web 框架之一，以其轻量级, 高可扩展性而著名。

- Jinja2：模板引擎
- Werkzeug：WSGI 工具集

### Gunicorn

Gunicorn 是一个开源的 Python WSGI HTTP 服务器，移植于 Ruby 的 Unicorn 项目的采用 pre-fork 模式的服务器

### WSGI

即 Python Web Server Gateway Interface，是 Python 专门的用于 Python 应用程序或框架与 Web 服务器之间的一种接口，没有官方的实现，因为 WSGI 更像一个协议，只要遵照这些协议，WSGI 应用都可以在 任何服务器上运行，反之亦然.

### Pre-Fork

预先创建进程，pre-fork 采用的是预派生子进程方式，用子进程处理不同的请求，每个请求对应一个子进程，进程之间是彼此独立的<br>
一定程度上加快了进程的响应速度

### Django

Django 是一个开放源代码的 Web 应用框架，由 Python 写成。采用了 MVC 的软件设计模式.使得开发复杂的、数据库驱动的网站变得简单。Django 注重组件的重用性和"可插拔性"，敏捷开发和 DRY 法则（Don't Repeat Yourself）<br>
_核心组件_

- 物件导向的映射器，用作数据模型（以Python类的形式定义）和 关联性数据库间的媒介
- 基于正则表达式的 URL 分发器
- 视图系统，用于处理请求
- 模板系统

### PyDruid

一个Druid的Python连接器公开一个简单的API来创建，执行和分析Druid查询等操作。

### Pandas

Pandas是一个Python包，提供快速，灵活和富有表现力的数据结构，旨在使"关系"或"标记"数据的工作既简单又直观

### SciPy

SciPy 是基于 Numpy 构建的一个集成了多种数学算法和方便的函数的 Python 模块

### Scikit-learn

Python中的机器学习依赖组件

### D3.js

D3.js 是一个操纵数据的 JavaScript 库

## 安装

### 基础环境

Linux version 3.10.0-123.el7.x86_64(builder@kbuilder.dev.centos.org)(gcc version 4.8.2 20140120 (Red Hat 4.8.2-16) (GCC) ) #1 SMP Mon Jun 30 12:09:22 UTC 2014

### yum源安装

- 配置yum源

  > cd /etc/yum.repos.d<br>
  > sudo wget <http://mirrors.nucc.com/repo/nucc-yum.repo>

- 安装epel源

  > sudo wget <http://mirrors.nucc.com/epel/epel-release-latest-7.noarch.rpm><br>
  > sudo rpm -ivh epel-release-latest-7.noarch.rpm

- 配置epel源

  > sudo wget <http://mirrors.nucc.com/repo/nucc-epel.repo>

- 验证配置

  > yum repolist

**note:** _如果使用过程中发现不能访问域名，需要配置DNS服务器地址_

> sudo vim /etc/resolv.conf<br>
> nameserver 172.16.1.4

### pip源安装

- 配置

  > mkdir ~/.python-pip<br>
  > cd ~/.pip<br>
  > sudo wget <http://mirrors.nucc.com/repo/pip.conf>

### superset安装

- 安装依赖

  > sudo yum upgrade python-setuptools<br>
  > sudo yum install gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel libsasl2-devel openldap-devel

- 安装Python虚拟环境

  > sudo pip install -i <http://pypi.nucc.com/simple> --trusted-host pip.nucc.com virtualenv<br>
  > mkdir /tooles/superset<br>
  > cd /tooles/superset<br>
  > virtualenv --no-site-packages superset<br>
  > source /tooles/superset/superset/bin/activate

- 安装Python包管理工具

  > pip install --upgrade setuptools pip

- 安装Superset

  - superset

    > pip install -U cryptography<br>
    > pip install superset

  - 创建管理员用户

    > fabmanager create-admin --app superset

    **创建用户时，需要交互填写用户姓氏、名字、邮箱、密码**<br>
    _Username [admin]: admin_<br>
    _User first name [admin]: channel_<br>
    _User last name [admin]: channel_<br>
    _Email [admin@fab.org]: channel@nucc.com_<br>
    _Password: admin_<br>
    _Repeat for confirmation: admin_<br>

    _<font color="#006400">Recognized Database Authentications.</font>_

    <br>

    _<font color="#006400">Admin User admin Created</font>_

  - 初始化数据库

    > superset db upgrade

  - 加载样例数据

    > superset load_examples

  - 创建默认角色和权限

    > superset init

  - 启动服务

    > superset runserver

测试环境启动：
>source /tools/superset/superset/bin/activate
>nohup superset runserver -p 8080 > /data/appLogs/superset.log 2>&1 &


  ## 安装mysql数据源

  - 下载mysql-community-devel-5.7.16-1.el7.x86_64.rpm,手动安装

    > sudo rpm -ivh mysql-community-devel-5.7.16-1.el7.x86_64.rpm

  - 安装驱动

    > pip install mysqlclient

  _如果出现openssl版本问题需要安装pip install pyOpenssl并导入python验证_<br>
  _python_<br>
  _>>> import OpenSSL;_<br>
  _如果出现StatementError cannot import name aead导入异常需要安装pip install aead_<br>
  _python_<br>
  _>>> import aead;_<br>
  _如果还出现以上异常可重新启动下superset服务_


## Windows开发环境安装
superset在Windows环境上依赖于visual c++ build tools 2015需要安装BuildTools_Full.exe。
在windows上，superset/superset/static目录下的指向assets的link无效，需要先用mklink命令创建一个Link。
删除static/assets
在windows/system32目录下找到cmd命令，右键，选中以管理员权限运行
在cmd窗口中用cd命令change dir到superset\superset\static目录
> mklink assets ..\assets

**注意：**sql查询时设置的超时执行信号是signal.SIGALRM实现的，signal模块在Windows上兼容不好，在signal的文档中明确说明 On Windows, signal() can only be called with SIGABRT, SIGFPE, SIGILL, SIGINT, SIGSEGV, SIGTERM, or SIGBREAK. A ValueError will be raised in any other case. Note that not all systems define the same set of signal names; an AttributeError will be raised if a signal name is not defined as SIG* module level constant.

本地开发环境可以注释掉~/superset/utils.py中的第428、429、438行代码，修改后代码如下
```Python
def __enter__(self):
       try:
           #signal.signal(signal.SIGALRM, self.handle_timeout)
           #signal.alarm(self.seconds)
           pass
       except ValueError as e:
           logging.warning("timeout can't be used in the current context")
           logging.exception(e)

   def __exit__(self, type, value, traceback):
       try:
           #signal.alarm(0)
           pass
       except ValueError as e:
           logging.warning("timeout can't be used in the current context")
           logging.exception(e)
```
## 源码执行
```Python
# coding=utf-8
# format参数中可能用到的格式化串：
# %(name)s Logger的名字
# %(levelno)s 数字形式的日志级别
# %(levelname)s 文本形式的日志级别
# %(pathname)s 调用日志输出函数的模块的完整路径名，可能没有
# %(filename)s 调用日志输出函数的模块的文件名
# %(module)s 调用日志输出函数的模块名
# %(funcName)s 调用日志输出函数的函数名
# %(lineno)d 调用日志输出函数的语句所在的代码行
# %(created)f 当前时间，用UNIX标准的表示时间的浮 点数表示
# %(relativeCreated)d 输出日志信息时的，自Logger创建以 来的毫秒数
# %(asctime)s 字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒
# %(thread)d 线程ID。可能没有
# %(threadName)s 线程名。可能没有
# %(process)d 进程ID。可能没有
# %(message)s用户输出的消息
import logging
logging.basicConfig(level=logging.DEBUG,
                    format='%(asctime)s %(thread)d %(pathname)s [line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S',
                    # filename='D:/test.log',
                    filename='/data/appLogs/superset.log',
                    filemode='w')
#################################################################################################
# 定义一个StreamHandler，将INFO级别或更高的日志信息打印到标准错误，并将其添加到当前的日志处理对象#
console = logging.StreamHandler()
console.setLevel(logging.DEBUG)
formatter = logging.Formatter('%(asctime)s %(thread)d %(pathname)s [line:%(lineno)d] %(levelname)s %(message)s')
console.setFormatter(formatter)
logging.getLogger('').addHandler(console)
#################################################################################################

from superset import app
app.run(debug=True, host='localhost', port=8088)

```
## 优化配置
### 1、修改MySQL数据源
修改SQLALCHEMY_DATABASE_URI，默认使用sqlite数据库，为了搭建统一开发环境这里修改成mysql数据库。
eg:
> SQLALCHEMY_DATABASE_URI = 'mysql://name:password@172.0.0.1:3306/mysql'

这里要注意源码中提供的config.py不能直接被加载，官网也明确指出To configure your application, you need to create a file (module) superset_config.py and make sure it is in your PYTHONPATH.意思是要在python的安装路径下创建superset_config.py文件才可以。如果使用python virtualenv虚拟环境把这个文件放到venv的bin目录即可。
由于我的卡发环境是再Windows上而且也没有使用virtualenv，所以只在D:\softs\python3安装路径创建了superset_config.py文件，由于执行的源码程序这里还需要改下BASE_DIR = "D:/workSpace/wl/channel-superset/superset"。
还要注意Windows下运行源码时会提示superset不是内部命令，此时需要进入工作空间D:/workSpace/wl/channel-superset/superset/bin 目录下执行python superset xxx

### 2、修改Redis缓存
Superset使用Flask-Cache进行缓存，Flask-Cache支持redis，memcached，simplecache（内存），或本地文件系统）等缓存后端，如果使用redis，需要安装 redis-py 库(Redis 的 Python 接口)。
> pip install redis

修改superset-config.py
```Python
CACHE_DEFAULT_TIMEOUT = 60 * 60 * 24
CACHE_CONFIG = {'CACHE_TYPE': 'redis',
                'CACHE_REDIS_HOST': '172.16.1.43',  # 配置域名
                'CACHE_REDIS_PORT': 7378,  # 配置端口号
                'CACHE_REDIS_PASSWORD' : 'dev123'
                }
```
这里需要注意superset是通过Flask-Cache管理缓存的，默认情况下不支持redisCluster集群。
![20180330000](http://oy48q6kwm.bkt.clouddn.com/1e24e71c7b3d2cf715982d4a0b351215.png)
不过通过修改Flask-Cache引用Flask-Cache-Redis-Cluster 0.0.5，应该是可以实现支持redisCluster的，这里没有尝试只是一个建议方法。
