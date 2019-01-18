---
title: virtualenv
date: 2018-04-21 11:21:02
categories: python
tags: virtualenv
---

# virtualenv
virtualenv 用来创建隔离的Python环境。解决依赖模块版本冲突等问题。
## 安装
```shell
pip install virtualenv
```
## 创建虚拟环境
```shell
virtualenv env
```
创建一个名为ENV的目录，并安装了ENV/bin/python并生成lib,include,bin目录安装了pip。
lib目录 : 所有安装的python库都会放在这个目录中的lib/pythonX.X/site-packages/中 ;
bin目录 : bin/python是当前虚拟环境使用的python解析器 ;
如果在命令行中运行
```shell
virtualenv --system-site-packages ENV
```
会继承/usr/lib/python3.6/site-packages下的所有库, 最新版本virtualenv把把访问全局site-packages作为默认行为
default behavior.

## 激活virtalenv
```shell
source ENV/bin/activate
```
当用户名前面出现小括号括起来的虚拟环境名时，表明虚拟环境被成功激活

## 关闭virtualenv
```shell
deactivate
```
## 参数
```shell
virtualenv -h
```
>选项:
--version
显示当前版本号。
-h, --help
显示帮助信息。
-v, --verbose
显示详细信息。
-q, --quiet
不显示详细信息。
-p PYTHON_EXE, --python=PYTHON_EXE
指定所用的python解析器的版本，比如 --python=python2.5 就使用2.5版本的解析器创建新的隔离环境。 默认使用的是当前系统安装(/usr/bin/python)的python解析器
--clear
清空非root用户的安装，并重头开始创建隔离环境。
--no-site-packages
令隔离环境不能访问系统全局的site-packages目录。
--system-site-packages
令隔离环境可以访问系统全局的site-packages目录。
--unzip-setuptools
安装时解压Setuptools或Distribute
--relocatable
重定位某个已存在的隔离环境。使用该选项将修正脚本并令所有.pth文件使用相当路径。
--distribute
使用Distribute代替Setuptools，也可设置环境变量VIRTUALENV_DISTRIBUTE达到同样效要。
--extra-search-dir=SEARCH_DIRS
用于查找setuptools/distribute/pip发布包的目录。可以添加任意数量的–extra-search-dir路径。
--never-download
禁止从网上下载任何数据。此时，如果在本地搜索发布包失败，virtualenv就会报错。
--prompt==PROMPT
定义隔离环境的命令行前缀。
环境变量和配置文件
>

## 迁移
可以直接压缩生产的ENV文件夹:
```shell
tar -zcvf ENV.tar.gz ENV
```
然后拷贝迁移至其他服务器下进行解压：
```shell
tar -zxvf ENV.tar.gz
```
<font color='FF9933'>此处需要注意如果迁移的两台机器路径完全一直可以直接激活使用，如果两台机器不一直需要进入./ENV/bin/下修改activate文件中参数：</font>
>VIRTUAL_ENV="/home/ENV"
export VIRTUAL_ENV

将上述VIRTUAL_ENV修改为当前venv文件夹正确的路径，然后执行:
```shell
source activate
```
然后执行：
```shell
which python
或者
which pip
```
查看是否是虚拟venv路径下的工具，如果是的话，则成功。
