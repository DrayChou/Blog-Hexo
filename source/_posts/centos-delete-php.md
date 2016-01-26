layout: 删除已经安装的PHP
title: centos-delete-php
date: 2016-01-26 22:50:37
categories:
- linux
tags:
- linux
- php
- delete
---

### 可以编译删除的
```
make   uninstall
make   clean
rm -rf php   //php目录
```

### 单独的可执行文件
whereis xxx 找到软件安装目录，rm -rf 把这些目录都删除

### 重新编译安装发

找一个临时目录重新安装一遍。比如./configure --prefix=/tmp/to_remove && make install
然后遍历/tmp/to_remove里的文件，把你原来安装位置的文件都删除。