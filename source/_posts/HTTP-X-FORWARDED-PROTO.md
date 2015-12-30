layout: post
title: HTTP_X_FORWARDED_PROTO
date: 2015-12-31 02:08:26
categories:
 - web
tags:
 - linux
 - yii
 - php
---

yii2 框架中根据 2 个值判断是不是 https ，如下：

    isset($\_SERVER['HTTPS']) && (strcasecmp($\_SERVER['HTTPS'], 'on') === 0 || $\_SERVER['HTTPS'] == 1) ||
    isset($\_SERVER['HTTP_X_FORWARDED_PROTO']) && strcasecmp($\_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') === 0;

其中 HTTPS 这个值比较好理解，直接查询服务器有没有配置过 HTTPS 就可以知道了。
但是， HTTP_X_FORWARDED_PROTO 这个值我就没看懂是什么意思，而且在网上查了蛮多资料，一般来说，是有设置过下面的值

    proxy_set_header   X-Forwarded-Proto $scheme;

之后，才可以在 php 的 $\_SERVER 中看到这个值，但是我们目前的服务器配置中并没有设置过这些内容，那么这个值是怎么来的呢？
先记下来，后面有头绪了再说。
