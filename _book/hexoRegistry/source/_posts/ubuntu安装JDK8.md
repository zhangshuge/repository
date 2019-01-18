---
title: ubuntu安装JDK8
date: 2018-09-04 21:48:27
categories:
tags:
---

### 1.安装software-properties-common软件包
```shell
apt-get install software-properties-common
```
### 2.添加PPA并安装Oracle Java8
```shell
sudo add-apt-repository ppa:webupd8team/java

sudo apt-get update

sudo apt-get install oracle-java8-installer
```
当执行install时会从Oracle的官网下载Java二进制文件，然后安装到Ubuntu系统．在安装过程中，需要同意Oracle的使用条款．
![oracle java](http://oy48q6kwm.bkt.clouddn.com/a72c98527e9613de8d8dc9f84f01dcff.png)
### 3.安装完成后检查Java版本
```shell
java -version
```
![java version](http://oy48q6kwm.bkt.clouddn.com/0655a79fe09aeba6423c6c6524ef0331.png)

### 4.设置环境变量
```shell
sudo apt-get install oracle-java8-set-default
```
命令完成后，在/etc/profile.d/目录下会有两个新的文件: jdk.csh和jdk.sh．这两个文件是shell脚本，里面是设置Java环境变量的命令，共有５个环境变量.
```shell
cat /etc/profile.d/jdk.sh
```
![jdk shell](http://oy48q6kwm.bkt.clouddn.com/b1e51e91ed086d4077f4ee07490b4b87.png)
刷新配置文件，使其生效。
```shell
source /etc/profile
```
查看JavaHome
```shell
echo $JAVA_HOME
```
![javaHome](http://oy48q6kwm.bkt.clouddn.com/a40ae3b958d4b10a2f5da2b2507b6aab.png)
