---
date: 2014-05-15
layout:  post
title:  "ubuntu 安装命令行自动补全"
tagline:
categories:
- linux
tags:
- linux
- bash
- completion
---

### ubuntu 安装命令行自动补全

	~# apt-get install bash-completion
	~# source /etc/bash_completion

编辑/etc/bash.bashrc，在最后加入如下代码

	[plain]
	if [ -f /etc/bash_completion ]; then  
		/etc/bash_completion  
	fi  

重新登录
