---
title: Centos6.7安装pip + python2.6到3.6
date: 2017-09-25 15:29:42
categories: Centos
tags: [Centos, Python]
---

# 1.安装pip    
Centos6.7 默认安装的是Python2.6没有安装pip，所以要想用pip去管理软件就需要自己手
	
动安装一下pip了。要安装pip,首先要安装setuptools.当前最新版本是36.5.0，这里是下载
	
[链接](https://pypi.python.org/pypi/setuptools#downloads “链接”)  解压下载的文件: 

<!--more-->

接下来进行安装：

> cd setuptools-36.5.0       
> python setup.py install

安装完成后，下载pip, 最新版本是9.0.1，这是下载[链接](https://pypi.python.org/pypi/pip “链接”)   
同样的，进行安装：  

>tar vxf pip-9.0.1.tar.gz    
>cd pip-9.0.1   
>python setup.py intsall

安装完成后，运行pip

![pip安装成功](http://op2hba6jz.bkt.clouddn.com/2017/9/pip-%E5%AE%89%E8%A3%852017-09-25_164327.png)
 
 
# 2.升级Python2.6到3.6   

由于Centos6.7安装的是python2.6，而且还不能卸载，因为很多系统组件需要依赖python2.6,

所以升级到python3.6会略微有点麻烦，所以写个博客记录一下。

1.在终端输入：

> python -V

Python 2.6.6 

2.使用pip安装wget

> pip install wget   

3.使用wget下载 Python-3.6.0

> wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz  

4.解压文件：

> tar zxvf Python-3.6.0.tgz

5.切换工作目录：

> cd Python-3.6.0

6.安装：

> ./configure    
> make all    
> make install   
> make clean  
> make distclean  

7.查看版本信息：

> /usr/local/bin/python3.6 -V

Python 3.6 

8.建立软连接，使系统默认的 python指向 python3.6

> mv /usr/bin/python /usr/bin/python2.6.6  
> ln -s /usr/local/bin/python3.6 /usr/bin/python  

9.重新检验Python 版本:

>python -V  

10.解决系统 Python 软链接指向 Python3.6 版本后，因为yum是不兼容 Python 3.6的，所以
yum不能正常工作，我们需要指定 yum 的Python版本: 

> vi /usr/bin/yum

将文件头部的

> !/usr/bin/python

改成

> !/usr/bin/python2.6.6

将PIP3链接到/usr/bin/pip目录

