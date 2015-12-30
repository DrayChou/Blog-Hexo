---
date: 2013-06-24
layout:  post
title:  "樹莓派加裝攝像頭"
tagline:
categories:
-  linux
tags:
- pi
---

樹莓派買回來好久，一直也沒什麼地方用得上。這次折騰下攝像頭監控的東東。
首先，找一個樹莓派支持的攝像頭。我的是很久以前用過的一個，像素質量已經很差了。幾乎看不清東西，先將就用一下吧。

首先，插上攝像頭，執行下面命令查看是否已識別：

	ls /dev

看看有沒有列出來 video1 這樣的設備，有的話就是支持的，沒有的話請自行查找驅動了。

上網查了下，大概有3種方法是比較常用的。

1. fswebcam

    	sudo apt-get install fswebcam
    	sudo fswebcam -d /dev/video0 -r 320x240 --bottom-banner --title "RaspberryPi" --no-timestamp /home/pi/yeelink.jpg

2. motion

		sudo apt-get install motion
		sudo vi /etc/motion/motion.conf

	找到”control_localhost on “和”webcam_localhost on“这两行，改为以下两行后，保存退出

		control_localhost off
		webcam_localhost off

	运行motion软件，输入

		motion -n

	在pc上用IE浏览器打开，下面網址進行監控設置
	配置网页：http://192.168.1.114:8080
	觀察网页：http://192.168.1.114:8081

3. mplayer

    	sudo apt-get install mplayer
    	sudo mplayer  tv://

裝好之後就是在遠程查看了。motion 有網頁端，在局域網可以觀看，另外的兩個就可以配合 crontab 和 btsync 或者 dropbox 來進行遠程觀察。或者直接放到開放平臺Yeelink上共享出來。
