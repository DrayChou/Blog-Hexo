---
date: 2013-11-30
layout:  post
title:  "ubuntu 下面配置 go 运行环境"
tagline:
categories:
- linux
tags:
- golang
---

# Go

## 配置安装环境

go 的安装需要用到很多的 package, 所以需要很多版本管理应用的支持，所以首先安装这些环境

	sudo apt-get install bison ed gawk gcc libc6-dev make python-setuptools python-dev build-essential git mercurial

## 安装Go

到 [官方网站](http://golang.org/dl/) 根据机器型号下载相应的版本，然后执行语句解压，

	$ tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz

我一般是放在 /usr/local/go 目录下

## 添加环境变量

	#go config
	export GOROOT=/usr/local/go
	export GOARCH=amd64
	export GOOS=linux
	export GOPATH=/srv/go_root
	export GOBIN=$GOROOT/bin
	export GOTOOLS=$GOROOT/pkg/tool/
	export PATH=$PATH:$GOBIN:$GOTOOLS:$GOPATH/bin

其中 /usr/local/go 为 go 安装目录， /srv/go_root 为代码存放目录
把这些添加到 .bashrc 文件中，然后执行 source ~/.bashrc 刷新配置

# Supervisor

有时候需要 go 持续运行不间断，但是用 crontab 并不方便，自己编写脚本也太麻烦，于是就可以用 Supervisor 了。

## 安装

	#安装
	sudo apt-get install python-pip python-m2crypto python-gevent supervisor
	pip install shadowsocks superlance

	#环境
	curl https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py | sudo python

	#生成配置文件
	echo_supervisord_conf /etc/supervisor/supervisor.conf

## 配置

安装好之后，就可以配置自动执行脚本了，脚本放在 /etc/supervisor/conf.d/ 目录下，示例：

	[program:web_hello]								#项目名
	command=/usr/local/go/bin/go run hello.go		#项目要执行的脚本
	autostart=true									#自动启动
	autorestart=true								#自动重启
	user=root										#执行的用户
	redirect_stderr=true							#有错误自动输出
	directory=/srv/go_root/src/web_hello/			#脚本执行的目录
	stderr_logfile=/srv/logroot/web_hello/error.log	#错误信息
	stdout_logfile=/srv/logroot/web_hello/debug.log	#日志信息

## 运行

执行下面的几个常用命令进行管理吧

	supervisorctl reload		#重新加载项目配置文件
	supervisorctl restart all 	#重启所有项目

## 出错

在执行 reload 命令的时候，有时候可能会出错，这时候就要执行下面的命令重新安装 Supervisor 了，不过放心项目配置文件还在。

	apt-get purge supervisor
	reboot
	apt-get install supervisor
	echo_supervisord_conf /etc/supervisor/supervisor.conf

# shadowsocks

## 安装

	# on server
	go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server

## 配置

	{
	    "server":"127.0.0.1",
	    "server_port":8388,
	    "local_port":1080,
	    "password":"barfoo!",
	    "method": "aes-256-cfb",
	    "timeout":600
	}

## 加入 Supervisor

	[program:shadowsocks]
	command=/usr/local/go/bin/shadowsocks-server -c /srv/approot/shadowsocks/config.json
	autostart=true
	autorestart=true
	user=root
	redirect_stderr=true
	stderr_logfile=/srv/logroot/shadowsocks/supervisor.log
	stdout_logfile=/srv/logroot/shadowsocks/supervisor.log

## 运行

	supervisorctl restart all
	supervisorctl reload
	supervisorctl restart all

# nginx

为了支持域名，现在开始 nginx 的安装

## 安装

	$ sudo apt-get install nginx

## 配置

在 /etc/nginx/sites-available 创建一个 ghost.conf 文件
使用文本编辑器打开这个文件 (e.g. sudo nano /etc/nginx/sites-available/ghost.conf) 把以下内容复制进这个文件

	server {
	    listen 80;
	    server_name example.com;

	    location / {
	        proxy_set_header   X-Real-IP $remote_addr;
	        proxy_set_header   Host      $http_host;
	        proxy_pass         http://127.0.0.1:2368;
	    }
	}

将 server_name 的值改为你的域名

把你的配置文件软链接到 sites-enabled 文件夹下:

	$ sudo ln -s /etc/nginx/sites-available/ghost.conf /etc/nginx/sites-enabled/ghost.conf

## 运行

	$ sudo service nginx restart

end.
