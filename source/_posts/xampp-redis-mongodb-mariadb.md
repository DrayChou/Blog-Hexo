---
date: 2013-08-29
layout:  post
title:  "在 Xampp 上配置 redis,mongodb,mariadb"
tagline:
categories:
- windows
tags:
- xampp
---

之前为了在本地调试方便，配置了这几个客户端在 xampp 下面的环境。现记录下

##程序

    可以去官网下载，也可以用我分享出来的地址 [http://goo.gl/zOGQ9m](百度网盘)

##安装

    将下载下来的压缩包中的 dll 文件拷贝到  xampp\php\ext 目录下，目录和 bat 文件放在 xampp 目录下

##配置

    修改 xampp\php\php.ini 配置文件，添加下面几行

    extension=php_mongo-1.4.0RC1-5.4-vc9.dll
    extension=php_igbinary.dll
    extension=php_redis.dll

##执行

    点击 redis_start.bat, mariadb_start.bat, mongodb_start.bat 来开启服务。

    点击 redis_stop.bat, mariadb_stop.bat, mongodb_stop.bat 来关闭服务。

注：现在的网盘大竞争真是让很多人得了便宜啊，可以去放一些乱七八糟的东西上去了。
