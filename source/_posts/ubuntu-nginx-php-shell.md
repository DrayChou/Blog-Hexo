---
date: 2013-06-16
layout:  post
title:  "ubuntu nginx php shell"
tagline:
categories:
- linux
tags:
- vps
---

ubuntu 下一键安装 nginx php 的环境

<script src="https://gist.github.com/DrayChou/4763610598b68170d4cc.js"></script>

nginx 配置参考：

    server {

        listen 80;
        server_name 127.0.0.1 localhost;
        root /usr/share/nginx/html/www;
        index index.php index.html index.htm;

        location ~ .*\.php(\/.*)*$ {
            include fastcgi.conf;

            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            fastcgi_index index.php;
            fastcgi_connect_timeout 300;
            fastcgi_send_timeout 300;
            fastcgi_read_timeout 300;

            fastcgi_buffers 8 256k;
            fastcgi_buffer_size 256k;
            fastcgi_busy_buffers_size 256k;
            fastcgi_temp_file_write_size 256k;
            client_max_body_size 20M;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    }

主要是配置缓存大小
