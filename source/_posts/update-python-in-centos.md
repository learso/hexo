---
title: CentOs 6.5升级Python 3.5
date: 2016-07-08 17:24:20
tags: centos,python,yum
categories: 信
---


### 更新系统
```
yum -y update
```

### 安装编译工具
```
yum groupinstall -y 'development tools'
```

### 下载安装源码
```
wget https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tgz
tar -zxvf Python-3.5.2.tgz
cd Python-3.5.2
./configure
make && make install
```

### 检查版本
```
python -V
```

### 备份原Python
```
mv /usr/bin/python /usr/bin/python2.6.6
ln -s /usr/local/bin/python3.5 /usr/bin/python
```

### 修改yum
```
vim /usr/bin/yum

第一行修改为:
#!/usr/bin/python2.6.6
```

### 修改pip
```
ln -s /usr/local/bin/pip3 /usr/bin/pip
```
