---
date: 2014-05-15
layout:  post
title:  "Centos 常用命令备录"
tagline:
categories:
- linux
tags:
- centos
---

- 安装包命令查找：

	yum whatprovides */lspci

- 查看主板型号：

	dmidecode |grep -A16 "System Information$"

- 内存槽及内存条：

	dmidecode |grep -A16 "Memory Device$"

- 硬盘：

	fdisk -l
	smartctl -a /dev/sda
	HP SmartArray (cciss) hardware RAID controllers：
	smartctl -d cciss,0 -a /dev/cciss/c0d0

- 网卡：

	mii-tool

- scsi/raid卡：

	lspci

- centos相关命令安装：

	yum -y install smartmontools
	yum install pciutils -y

- centos 安装 htop

	rpm 包下载地址: http://packages.sw.be/htop/
	安装命令： rpm –ivh htop-0.8.3-1.el4.rf.i386.rpm

- end
