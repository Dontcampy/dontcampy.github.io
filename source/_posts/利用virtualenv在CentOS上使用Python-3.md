---
title: 利用virtualenv在CentOS上使用Python 3
date: 2018-10-07 12:56:17
tags: Python
categories: Python
---

## 步骤：

### 1.准备编译环境：

​	安装一些编译环境以防安装出错并且避免以后发生遇见的问题。

```shell
yum groupinstall -y "Development Tools"

yum install -y readline-devel sqlite-devel zlib-devel bzip2-devel openssl-devel ncurses-devel
```

### 2.下载Python 3源码

​	这里以Python 3.6.6为例

```shell
wget  https://www.python.org/ftp/python/3.6.6/Python-3.6.6.tar.xz
```

​	如果要下载其他的版本，可以在https://www.python.org/downloads/选择想要使用的版本，点进去选择XZ compressed source tarball的Version下载。

### 3.编译源码

​	此处以刚刚下载的Python-3.6.6.tar.xz为例，使用其他版本请注意指令中的文件名。

```shell
tar Jxvf Python-3.6.6.tar.xz # 解压刚刚下载的文件

cd Python-3.6.6 # 进入刚刚解压的文件夹内

./configure --prefix=/usr/local/python3 # 设置安装路径

make && make install # 安装
```

​	稍等片刻，我们的Python 3编译好了，路径在/usr/local/python3。

### 4.安装virtualenv并使用它切换至Python 3环境

```shell
pip install virtualenv # 使用系统自带的Python2安装virtualenv

virtualenv -p /usr/local/python3/bin/python3 venv # 配置virtualenv所使用的Python路径，这里我们就使用刚刚安装的Python3路径，然后这个环境取名为venv。

source venv/bin/activate # 进入刚刚配置的环境。
```

进入环境以后，不论是python还是pip都会默认使用配置路径中的路径，不会再使用系统默认的了。

退出venv环境。

```shell
deactivate
```

PS：你也可以利用virtualenv给你的每个项目都配置单独的环境，方便起见你可以进入你的项目根目录然后按照第四步的步骤来做，注意环境名是唯一的不能重复。

