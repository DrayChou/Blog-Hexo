---
date: 2013-06-16
layout:  post
title:  "uWSGI+Nginx run flask twip"
tagline:
categories:
- linux
tags:
- vps
---

原文:http://ichon.me/post/999.html

twip.tar.gz:http://ichon.me/uploads/2013/02/twip.tar.gz

examples:https://github.com/yegle/flask_twip/tree/master/examples

安装uWSGI

使用pip：

    pip install uwsgi

安装Flask-Twip

Flask-Twip是作为Flask的一个插件来安装的，安装依然只需要使用pip：

    pip install Flask-Twip

配置Flask-Twip

由于 @yegle 湿兄并没有在examples中提供uWSGI运行的示例，所以只好自己动手，按照uWSGI运行的方式改写了示例程序，并且将其打包 twip.tar.gz

只需将其解压到网站的目录，比如/home/www

    tar zxvf twip.tar.gz -C /home/www

然后修改配置文件settings.py，填写好在dev.twitter.com申请到的TWITTER_CONSUMER_KEY和TWITTER_CONSUMER_SECRET，至于SECRET_KEY嘛，就随便填好了～
运行uWSGI

我写了个uWSGI运行Flask程序的脚本server(在twip.tar.gz中)，只需要给其增加可执行权限：

    chmod +x server

执行./server start就可以启动uWSGI，同理，执行./server restart和./server stop可以重启和停止uWSGI。

查看log文件/tmp/uwsgi-twip.log，如果没有任何错误，就说明uWSGI已经成功运行。
配置Nginx

光有uWSGI是不能够运行Flask-Twip的，我们还需要Nginx作为Web Server，只需要修改Nginx的配置文件，增加一个server，如下所示：

    server
    {
        listen 80;
        server_name www.example.com;
        location /
            {
                include     uwsgi_params;
                uwsgi_pass  unix:/tmp/uwsgi-twip.sock;
            }
        location ^~ /twip/static/
            {
                alias /home/www/twip/static/;
            }
    }

重启Nginx，如果一切顺利的话，就可以在 http://www.example.com/twip/ 看到熟悉的Twip界面了～

ps:之前的 server 文件有误，修改 -C 666 为 --chmod-socket=666
