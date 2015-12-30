---
date: 2011-04-14
layout:  post
title:  "搜索引擎配置优化笔记 - 老板的讲课"
tagline:
categories:
- web
tags:
- seo
---
搜索引擎优化 并不是 只seo 而是只自建搜索引擎的配置优化

使用了两个开源的软件：<a href="http://sphinxsearch.com/" target="_blank">sphinx</a> 和 <a href="http://timyang.net/data/redis-misunderstanding/" target="_blank">redis</a>

开源搜索引擎

1.Lucence/Nutch/Solr    Java编写

2.Sphinx/Coreseek    C++

3.Xapian    豆瓣

4.BosS


Sphinx 介绍

1.配置索引文件

2.索引    （正向索引 -> like %key%  ;    反向索引 -> 先建关键词列表）

3.处理搜索

4.2-3不断重复

 

Sphinx 特点

索引快，支持中文，丰富的查询表达式，可以分段落，支持模糊查询，多种结果后处理机制

排序，BM25，搜索算法

支持实时索引，地理位置搜索

 

Redis 介绍

Nosql 数据库， 数据常驻内存， 实时异步存储到数据库

 

Redis 特点

数据不会丢失，查询速度快

 

流程

论坛 -> 索引服务器 -> 处理文档 去特殊字符-> 存储到Redis ,获得ID -> 索引服务器Sphinx

 

中文分词

Sphinx 汉字自动单词分词 一元分词法

查询时用“”取消分词，对汉字进行词语分组

最多分词法，一元分词法（最灵活）

中文分词法 httpcus 张宴

分词中学习，检查某几个字合在一起得到的结果多少

同义词表

自动纠错

自动完成功能

SCWS 分词 php中文分词

搜索的时候找稀少词，分词后，搜索结果越少的词越是用户需要的
