---
date: 2015-01-30
layout:  post
title:  "laravel 部署"
tagline:
categories:
-  web
tags:
- laravel
---

看最近 laravel 好像蛮流行的，部署一个玩玩。

## 基础环境

### composer

    $ curl -sS https://getcomposer.org/installer | php
    $ mv composer.phar /usr/local/bin/composer

这个就是传说中的 php 的包管理器了，之前没怎么用过。

### PEAR

Download PEAR

    curl -O http://pear.php.net/go-pear.phar
    sudo php -d detect_unicode=0 go-pear.phar

Configure and Install PEAR

You should now be at a prompt to configure PEAR.

Type 1 and press return .
Enter:

    /usr/local/pear

Type 4 and press return .

Enter:

    /usr/local/bin

Press return

Verify PEAR

You should be able to type:

    pear version

### json

    apt-get install php5-json

### mcrypt

    sudo rm /etc/php5/mods-available/mcrypt.ini
    sudo apt-get purge php5-mcrypt
    sudo apt-get install mcrypt
    sudo apt-get install php5-mcrypt
    sudo php5enmod mcrypt
    sudo service php5-fpm restart

## 安装 Laravel

首先，通过 Composer 下载 Laravel 安装器。

    composer global require "laravel/installer=~1.1"

请确保把 ~/.composer/vendor/bin 路径添加到 PATH 环境变量里, 这样laravel 可执行文件才能被命令行找到, 以后您就可以在命令行下直接使用 laravel 命令.
安装成功后, 可以使用命令 laravel new 在您指定的目录下创建一份全新安装的 Laravel。例如，laravel new blog 将会在当前目录下创建一个叫 blog 的目录, 此目录里面存放着全新安装的 Laravel 以及其依赖的工具包。这种安装方法比通过 Composer 安装要快许多。

## 配置路由

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

这样访问地址就更好看了。

## 配置版本控制

进到 Laravel目录，执行 git init 初始化 git 项目，然后执行下面的命令链接到远程仓库：

    git remote add origin git@123.com
    git checkout master -f
    git pull
    git add .
    git commit -m 'update'
    git push

于是，可以远程修改了。

## 常见错误

### Error in exception handler

出现如题错误 先开启laravel的调试模式:
app/config/app.php 文件中

    'debug' => flase,修改成 'debug' => true,

开启调试模式后就能非常清楚的知道出错的原因了,app/storage 目录的权限问题,运行apache服务器的默认用户是www-data所以解决如下

    sudo chown -R www-data:www-data app/storage

原因是文件夹目录没有写权限。
