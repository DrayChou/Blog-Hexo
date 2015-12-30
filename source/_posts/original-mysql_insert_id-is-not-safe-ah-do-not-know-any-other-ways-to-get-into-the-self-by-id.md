---
date: 2011-04-15
layout:  post
title:  原来mysql_insert_id()也不安全啊，不知道有没有其他方法可以用来得到插入的自增ID
tagline:
categories:
- web
tags:
- mysql
---
今天我负责的一个项目出了问题，插入数据之后调用mysql_insert_id()拿取插入的自增ID的时候一直返回0，试了一下在本地是可以拿到的，但是放到线上就不可以了。

无奈，只好插入完毕之后再通过插入的值来查询一遍得到insert_id。

后来发现，mysql_insert_id() 带上数据量连接ID之后成功率倒是上升了很多，但是高并发下还是有可能会出现得到mysql_insert_id()返回0的现象。

不知道有没有其他方法可以用来得到插入的自增ID。

记。。。
