---
layout: blog
title: pi 安装 ssr，cow 备注
date: 2018-03-28 17:44:00
categories:
- linux
tags:
- pi
- ssr
- ss
- cow
---

偶尔一次使用的东西，记一下！

## ssr

### 安装 **python**
```
sudo apt-get install python-pip python3-pip git htop
```

### 安装 **ssr**
```
mkdir /srv/approot
git clone https://github.com/ToyoDAdoubi/shadowsocksr shadowsocksr-doubi
```

### 配置 **ssr**
```
nano /srv/approot/ssr-config/jp1.json
{
    "server": "0.0.0.0",
    "server_ipv6": "::",
    "server_port": 8388,
    "local_address": "127.0.0.1",
    "local_port": 1080,

    "password": "m",
    "method": "aes-128-ctr",
    "protocol": "auth_aes128_md5",
    "protocol_param": "",
    "obfs": "tls1.2_ticket_auth_compatible",
    "obfs_param": "",
    "speed_limit_per_con": 0,
    "speed_limit_per_user": 0,

    "additional_ports" : {}, // only works under multi-user mode
    "timeout": 120,
    "udp_timeout": 60,
    "dns_ipv6": false,
    "connect_verbose_info": 0,
    "redirect": "",
    "fast_open": true
}
```

### 启动 **ssr** 服务
```
sudo python3 /srv/approot/shadowsocksr-doubi/shadowsocks/local.py \
    -c /srv/approot/ssr-config/jp1.json \
    --pid-file /var/run/shadowsocks-rix.pid \
    -d start
```

这样的话，ssr 服务就起来了，需要启动多个的话，修改 Pid file 的路径就可以了。


## cow

### 安装 **golang**
```
mkdir /srv/approot
cd /srv/approot
wget https://dl.google.com/go/go1.10.linux-armv6l.tar.gz
tar -xzf go1.10.linux-armv6l.tar.gz
cd /usr/local
ln -s /srv/approot/go
cd /usr/local/bin
ln -s /srv/approot/go/bin/go
ln -s /srv/approot/go/bin/godoc
ln -s /srv/approot/go/bin/gofmt
```

### 安装 **cow**
```
go get github.com/cyfdecyf/cow
```

### 配置 **cow**
```
nano ~/.cow/rc

listen = http://127.0.0.1:7777

# SOCKS5 二级代理
proxy = socks5://127.0.0.1:1080
proxy = socks5://127.0.0.1:1081
```

### 配置 **cow** 启动脚本
```
sudo wget https://github.com/cyfdecyf/cow/blob/master/doc/init.d/cow /etc/init.d/cow
sudo /etc/init.d/cow

修改
USER=pi
GROUP=root
```

## 参考页面
https://doub.io/ss-jc45/
https://github.com/shadowsocksr-backup/shadowsocks-rss/wiki/Python-client-setup-(Mult-language)
https://golang.org/dl/
https://github.com/cyfdecyf/cow
https://www.wandianshenme.com/play/use-golang-build-iot-application-on-raspberry-pi/
