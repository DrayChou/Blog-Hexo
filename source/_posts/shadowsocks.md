---
date: 2014-06-02
layout:  post
title:  "Shadowsocks 新手指南"
tagline:
categories:
- linux
tags:
- Shadowsocks
- cow
---


#Shadowsocks

shadowsocks 簡稱 ss 是一套的代理協議，包含服務端應用和客戶端應用。使用 ss:// 格式的鏈接協議來標識服務器地址。

## 客戶端
如果你已經有了服務器地址，那麼我們就直接來配置客戶端吧，如果沒有，那麼你需要去找IT男要一個，或者去 [ShadowSocks公益组织](https://www.shadowsocks.net/) 找一個吧。

參見： [Shadowsocks 客戶端列表](https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients)

## Windows && Linux && OSX
鄙人平常主用 [cow](https://github.com/cyfdecyf/cow) ,這個客戶端用 golang 語言編寫，是一个简化穿墙的 HTTP 代理服务器。它能自动检测被墙网站，仅对这些网站使用二级代理，支持 http,ssh 轉發 直接支持 ss ，所以可以用 cow 做二級代理來支持本地其他類型的代理。
比如： 用 cow 轉發 http,ssh,ss 到 pac 代理，讓本地的瀏覽器手機等可以無憂翻牆。

### 快速開始
OS X, Linux (x86, ARM): 执行以下命令（也可用于更新）

	curl -L git.io/cow | bash

Windows: [点此下载](http://dl.chenyufei.info/cow/)

熟悉 Go 的用户可用 go get github.com/cyfdecyf/cow 从源码安装
编辑 ~/.cow/rc (Linux) 或 rc.txt (Windows)，简单的配置例子如下：

	#开头的行是注释，会被忽略
	# 本地 HTTP 代理地址
	# 配置 HTTP 和 HTTPS 代理时请填入该地址
	# 或者在自动代理配置中填入 http://127.0.0.1:7777/pac
	listen = http://127.0.0.1:7777

	# SOCKS5 二级代理
	proxy = socks5://127.0.0.1:1080
	# HTTP 二级代理
	proxy = http://127.0.0.1:8080
	proxy = http://user:password@127.0.0.1:8080
	# shadowsocks 二级代理
	proxy = ss://aes-128-cfb:password@1.2.3.4:8388
	# cow 二级代理
	proxy = cow://aes-128-cfb:password@1.2.3.4:8388
	使用 cow 协议的二级代理需要在国外服务器上安装 COW，并使用如下配置：

	listen = cow://aes-128-cfb:password@0.0.0.0:8388
	完成配置后启动 COW 并配置好代理即可使用。

然後修改IE瀏覽器設置， internet 選項 -> 連接 -> 局域網設置 -> 使用自動配置腳本，填入：http://127.0.0.1:7777/pac ，然後就OK了。

## 服務端

Shadowsocks 服務端本身支持 c, go, nodejs, python, erlang 等語言，如果你需要配置服務端，那麼說明你是有一定技術基礎的，請參見官方介紹吧。[Shadowsocks 服務端](https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients)
