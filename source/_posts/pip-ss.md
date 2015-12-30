---
date: 2015-01-14
layout:  post
title:  "python 版本 shadowsocks"
tagline:
categories:
- web
tags:
- shadowsocks
- supervisor
- fqrouter
---

因为墙更高了， fqrouter 都用不了了，没办法，只能把之前的 ss 拿起来用了。
这次重新使用 python 版本的 ss。

首先，安装

	apt-get update
	apt-get install python-pip python-m2crypto supervisor
	pip install shadowsocks

执行

	service supervisor start
	supervisorctl reload

如果遇到问题，可以检查日志：

	supervisorctl tail -f shadowsocks stderr

如果修改了 shadowsocks 配置 /etc/shadowsocks.json， 可以重启 shadowsocks：

	supervisorctl restart shadowsocks

如果修改了 Supervisor 的配置文件 /etc/supervisor/*， 可以更新 supervisor 配置：

	supervisorctl update

Shadowsocks 的服务单独启动方法：

	ssserver -c /etc/shadowsocks.json -d start
	ssserver -c /etc/shadowsocks.json -d stop

结束。
