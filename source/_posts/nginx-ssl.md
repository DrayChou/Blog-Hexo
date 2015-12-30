---
date: 2013-06-16
layout:  post
title:  "ubuntu nginx ssl"
tagline:
categories:
- linux
tags:
- ssl
- nginx
---

原文：http://www.douban.com/note/248058067/

安装应用并生成证书

    apt-get install ssl-cert
    make-ssl-cert /usr/share/ssl-cert/ssleay.cnf /etc/ssl/private/blog.crt

然后输入主机名

生成证书为

    cat /etc/ssl/private/blog.crt

编辑文件并在里面填入我们得到以上文件 的 —–BEGIN PRIVATE KEY—– 和 —–END PRIVATE KEY—- 之间的部分

    vi /etc/ssl/private/blog.key
    chmod 600 /etc/ssl/private/blog.key

编辑文件并在里面填入得到的文件的下半部分 ， —–BEGIN RSA PRIVATE KEY—– 跟 —–END RSA PRIVATE KEY—– 之间

    vi /etc/ssl/certs/blog.pem

现在我们就可以把 /etc/ssl/private/blog.crt 删除了 。

    rm -f /etc/ssl/private/blog.crt

修改 nginx 文件在  server {     和      } 之间 添加

    listen 443 ssl;
    listen [::]:443 ipv6only=on ssl;
    ssl_certificate /etc/ssl/certs/blog.pem;
    ssl_certificate_key /etc/ssl/private/blog.key;

或者

    listen 443 ;
    listen [::]:443 ipv6only=on ;
    ssl on;
    ssl_certificate /etc/ssl/certs/blog.pem;
    ssl_certificate_key /etc/ssl/private/blog.key;

完成之后重启 nginx
