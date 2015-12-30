---
date: 2013-08-22
layout:  post
title:  "在Ubuntu上创建只有访问权限的帐号"
tagline:
categories:
- linux
tags:
- vps
---

## ubuntu

首先SSH登录VPS，创建一个登录脚本：
vi /bin/nologin.sh
在vim中按下i，添加下面的内容：

	#!/bin/sh
	echo ""
	echo "  ***********************************************************"
	echo "  * Sorry,you can't Login by this way, press a key to exit. *"
	echo "  ***********************************************************"
	echo ""
	read x
	exit

写完之后按esc，输入:wq回车保存。为此文件添加执行权限：

	chmod 755 /bin/nologin.sh

添加一个用户到nogroup组，并且指定它的启动脚本：

	useradd newuser -g nogroup -s /bin/nologin.sh

注意有些linux系统是添加到nobody组。最后更改一下这个用户的密码：

	passwd newuser

本地调用代理的话使用

    ssh -qTfnN -D 7070 username@sshserver.com

来生成本地 socks5 代理地址，或者安装 gstm 来配置代理。

    sudo apt-get install gstm

## centos

1，增加一个linux用户，并赋予该用户一个nologin的shell权限。

    useradd username -s /sbin/nologin

2，设置该用户密码。

    passwd username

over!
