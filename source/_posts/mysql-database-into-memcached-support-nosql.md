---
date: 2011-04-14
layout:  post
title:  "Mysql 数据库引入 memcached，支持 Nosql"
tagline:
categories:
- web
tags:
- mysql
---
mysql 也开始支持Nosql了，这样一来如果可以直接用sql语句进行检索查询的话无疑会把原先的Memcache等给排挤出去，如果效率方面又很高的话，那么memcache还活什么啊？

嗯。。。期待。。。


Oracle 前天在 <strong>2011 Mysql user conference and expo</strong> 大会上发布的 Mysql 5.6.2 测试版本，详情请看<a href="http://www.oschina.net/news/17118/mysql-5-6-2-dev">这里</a>。

该版本最值得关注的便是对 Nosql 技术的支持，尽管目前还是实验阶段，该技术使得 Mysql 内置 Nosql 技术，该技术可减少 memcached 的查询延迟。在单台机器中，Nosql 当前只适用一张 InnoDB 表，但未来将支持多个表。在 memcached 中的 key和value 分别对应表中的相应字段，同时可为 key定义多列的值。所有这些数据都存储在一张 InnoDB 表，可通过 sql 命令来进行检索和修改。目前集成 memcached 守护进程的版本只能用于 linux。

来自 InnoDB 的<a href="http://blogs.innodb.com/wp/2011/04/get-started-with-innodb-memcached-daemon-plugin/" target="_blank">博客</a>向你介绍如何启用该功能

下图是该技术的架构图：

<img src="http://pic003.cnblogs.com/2011/66372/201104/2011041310182092.jpg" alt="" width="627" height="468">

来自:<a href="http://news.cnblogs.com/n/97243/">http://news.cnblogs.com/n/97243/</a>
