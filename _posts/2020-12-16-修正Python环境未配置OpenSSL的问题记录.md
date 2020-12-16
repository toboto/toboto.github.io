---
layout:     post
title:      "修正Python环境未配置OpenSSL的问题记录"
subtitle:   "对于Python未包含SSL模块的情况予以修正"
date:       2020-12-16
author:     "toboto"
tags:
    - OpenSSL
    - Ubuntu
    - Python
---

本文环境是Ubuntu Server 14.04.2 LTS，内核版本3.13.0，使用的Python版本是3.7.3。

## 问题描述

在执行一些Python代码以及使用pip搜索安装包时报错，如下所示：
``` 
(venv) wangrui@dev-host:/data0/htdocs/dev-midata$ pip search numpy

WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'SSLError("Can't connect to HTTPS URL because the SSL module is not available.")': /pypi
WARNING: Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'SSLError("Can't connect to HTTPS URL because the SSL module is not available.")': /pypi
WARNING: Retrying (Retry(total=2, connect=None, read=None, redirect=None, status=None)) after connection broken by 'SSLError("Can't connect to HTTPS URL because the SSL module is not available.")': /pypi
WARNING: Retrying (Retry(total=1, connect=None, read=None, redirect=None, status=None)) after connection broken by 'SSLError("Can't connect to HTTPS URL because the SSL module is not available.")': /pypi
WARNING: Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'SSLError("Can't connect to HTTPS URL because the SSL module is not available.")': /pypi

ERROR: Exception:
Traceback (most recent call last):
  File "/data0/htdocs/dev-midata/venv/lib/python3.7/site-packages/pip/_vendor/urllib3/connectionpool.py", line 688, in urlopen
    conn = self._get_conn(timeout=pool_timeout)

  File "/data0/htdocs/dev-midata/venv/lib/python3.7/site-packages/pip/_vendor/urllib3/connectionpool.py", line 280, in _get_conn
    return conn or self._new_conn()

  File "/data0/htdocs/dev-midata/venv/lib/python3.7/site-packages/pip/_vendor/urllib3/connectionpool.py", line 980, in _new_conn
    "Can't connect to HTTPS URL because the SSL module is not available."

pip._vendor.urllib3.exceptions.SSLError: Can't connect to HTTPS URL because the SSL module is not available.
``` 
最开始怀疑了OpenSSL版本的问题，所以将OpenSSL从1.0.1先升到了1.1.1，事后证明这个步骤可能是不需要的。实际的问题是，本机上的Python3.7版本在编译时没有包含SSL的模块，因此导致python或者pip执行过程中，无法找到SSL模块。

## 解决方法
解决这个问题的方式就是重新安装或者重新编译Python3.7，可以用两种方法。

### 方法1：通过apt安装
本机使用的apt源是阿里的镜像，默认情况下安装的python3版本是3.4，也可能你所遇到的源安装的版本不一样。这里不必纠结，如果安装源中不包含你需要的Python版本，则添加一个包含所需要版本的apt源。本文中，我们的目标是Python3.7
```
add-apt-repository ppa:deadsnakes/ppa
apt install python3.7
```
通过以上方式即可完成，完成后已经默认包含了对SSL的支持。

### 方法2：重新编译源代码
建议自行尝试一下这种方式，将来遇到其他问题的时候，可能还是用得上。
首先下载Python3.7的代码：
```
wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz
```
随后，解压安装包，并且编辑Modules/Setup配置文件：
```
tar -zxvf Python-3.7.3.tgz
cd Python-3.7.3
./configure
vi Modules/Setup
```
在Modules/Setup配置文件中，找到SSL相关的部分，配置为本地的OpenSSL安装路径（本文中为/usr/local/openssl/）。
```
# Socket module helper for SSL support; you must comment out the other
# socket line above, and possibly edit the SSL variable:
SSL=/usr/local/openssl/      #取消这一行的注释，并将原来的/usr/local/ssl改为/usr/local/openssl/
_ssl _ssl.c \     #取消这一行的注释
true-DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \      #取消这一行的注释
true-L$(SSL)/lib -lssl -lcrypto      #取消这一行的注释
```
编辑之后就可以编译和安装了。
```
make && make install
```
安装好的位置默认是在/usr/local/bin/python3.7，此时再运行代码错误消失。

## 附录
### Ubuntu环境下的update-alternatives工具
通常我们都会在环境中具有多个不同的Python版本，比如同时具有Python2、Python3等，由于版本容易碎片化，建议尽量使用virtualenv来配置每个应用的执行环境，具体方法可参考[基于HBase的数据分析方案](/2020/06/09/基于HBase的数据分析方案.html)一文。

当然，我们也希望在系统环境中，python指向的是我们希望的版本。这时，可以利用update-alternatives，它可以用来管理在系统路径下的文件链接指向。其原理就是建立系统路径下的links，来指向对应的实际可执行文件，并且对配置过的多个指向，进行管理而不是简单的覆盖或者删除。

例如，我们需要对python这个命令配置默认指向，那么可以使用：
```
update-alternatives --config python
```
在本文环境下得到的是：
```
There are 2 choices for the alternative python (providing /usr/bin/python).
  Selection    Path                      Priority   Status
------------------------------------------------------------
  0            /usr/bin/python3.7         10        auto mode
  1            /usr/bin/python3.7         10        manual mode
* 2            /usr/local/bin/python3.7   2         manual mode
```
可以看到除了auto模式外，有两个python3.7可以供我们选择，这里我选择的是优先级较低的那个。实际上，这就是我们上文中重新编译的Python3.7，指向后我们建立了一个链接
```
lrwxrwxrwx 1 root root 24 Jul  8 01:42  /usr/bin/python  ->  /etc/alternatives/python 
```
也就是将/usr/bin下的python指向了/etc/alternatives/python，而/etc/alternatives/python又指向了/usr/local/bin/python3.7
```
lrwxrwxrwx 1 root root 24 Dec 15 22:45  /etc/alternatives/python  ->  /usr/local/bin/python3.7
```
当然，要实现这样的效果，我们需要将我们希望指向的可执行文件，配置到python这个alternatives名称中。   
方法如下：
```
update-alternatives --install /usr/bin/python python /usr/local/bin/python3.7 2
```
其中第一个参数（/usr/bin/python ）是link的位置，第二个参数python是这个alternative的名称，第三个参数是实际执行命令，第四个参数是优先级，优先级最高的选项会被auto模式选中。
关于update-alternatives的其他管理，建议自行尝试。
