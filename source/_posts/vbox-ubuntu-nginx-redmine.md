layout: post
title: virtualbox ubuntu 下面安装 redmine
date: 2016-03-12 15:40:12
categories:
 - linux
tags:
 - virtualbox
 - ubuntu
 - redmine
---

## 安装 ubuntu

### 配置网络
然后在 vb 中配置安装 ubuntu ，这里需要注意的是，把网络类型改为 桥接。

### 配置静态IP

    sudo vi /etc/network/interfaces

原有内容只有如下两行：

    auto lo
    iface lo inet loopback

如果是动态获取IP地址，那么就不需要添加如下内容
如果设置静态IP,向末尾追加以下内容：

    auto eth0
    iface eth0 inet static
    address 静态IP地址
    gateway 192.168.0.1
    netmask 255.255.255.0

然后保存退出；

### 更新源
更新源： /etc/apt/sources.list
阿里更新源（14.04）

    deb http://mirrors.aliyun.com/ubuntu/ trusty main multiverse restricted universe
    deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main multiverse restricted universe
    deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main multiverse restricted universe
    deb http://mirrors.aliyun.com/ubuntu/ trusty-security main multiverse restricted universe
    deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main multiverse restricted universe
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty main multiverse restricted universe
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main multiverse restricted universe
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main multiverse restricted universe
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main multiverse restricted universe
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main multiverse restricted universe

### vbox 组件

    sudo apt-get install virtualbox-guest-dkms

### 设置共享目录

    ln -s /media/sf_Downloads /srv/download

### 目录权限
使用以下命令添加当前用户到 vboxsf 组，以免权限不足编辑共享目录，重启虚拟机生效。

    sudo usermod -aG vboxsf $(whoami)
    sudo usermod -aG vboxsf www-data

## 配置 ssh

### 安装 ssh 服务端

    sudo apt-get install openssh-server

### 开启服务

    sudo server ssh restart

## 配置 mysql

### 安装 mysql

    sudo apt-get install mysql-server

### 创建数据库

    mysql -u root -p
    CREATE DATABASE redmine CHARACTER SET utf8;
    CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'my_password';
    GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
    EXIT

### 设置远程访问权限

    grant all privileges on *.* to 'root'@'%' identified by 'password' with grant option;
    flush privileges;

### 打開 my.conf

    sudo vim /etc/mysql/my.cnf

### 设置服务器地址

    bind-address            = 0.0.0.0

## 配置 ruby

### 安装 rvm

輸入指令安裝 RVM，過程中可能會出現一些錯誤訊息，因為我沒有預先使用 apt-get 安裝需要的套件。不過不要緊，跟著系統會告訴哪些還沒裝好，並且會給你安裝的指令，跟著系統指示很快的就可以完成。

    curl -L https://get.rvm.io | bash

重新登入 vps，輸入 rvm -v 查看 rvm 是否有裝好。

在 RVM 中安裝 Ruby

    rvm install 2.2.3

將 ruby 2.2.3 設定成預設的 Ruby 語言，這個動作很重要一定要做，因為預設的 Ruby 會是 Ubuntu 系統中預裝的版本，換成 RVM 的版本我們才好處理 Gem 之類的安裝問題

    rvm use 2.2.3 --default

檢查系統中的 ruby 是否使用 rvm 的 ruby

輸入ruby -v檢查版本
輸入which ruby 檢查路徑，路徑裡面有 rvm 的才是正確

### 修改 gem source

    gem sources -r https://rubygems.org/
    gem source -a https://ruby.taobao.org
    gem source -l   // 查看当前的source

### 修改 bundle source

    bundle config mirror.https://rubygems.org https://ruby.taobao.org

### 安裝 Rails

記得加上 --no-ri --no-rdoc ，意思是不要裝文件，因為我們上網查就好了。可以省下很多時間。

    gem install rails --no-ri --no-rdoc

### 把 Redmine 專案載下來，

    wget http://www.redmine.org/releases/redmine-3.2.0.zip

### 解壓縮

    unzip redmine-3.2.0.zip

現在你有一個 Redmine 的 Rails 專案了。

### 對 Rails 專案的一些處理

bundle 一下。可能會有一些 Ubuntu 的套件沒有裝會噴錯誤。不過都還滿簡單的。

    bundle install

缺少 imagemagick 的話可以下下面指令。

    sudo apt-get install imagemagick
    sudo apt-get install libmagickwand-dev

### Rails 資料庫處理

    rake db:create
    rake db:migrate

建之前要更新一下 config/database.yml 的內容，把 mysql 帳號密碼寫進去。

### 安裝 Passenger

    gem install passenger --no-ri --no-rdoc

使用 Passenger 安裝 nginx

    rvmsudo passenger-install-nginx-module

### 安装 Nginx init script

    cd ~/
    git clone git://github.com/jnstq/rails-nginx-passenger-ubuntu.git
    sudo mv rails-nginx-passenger-ubuntu/nginx/nginx /etc/init.d/nginx
    sudo chmod +x /etc/init.d/nginx

### 開機自動啟動

    sudo update-rc.d nginx defaults

## 設定 nginx.conf

### 打開 nginx.conf

    sudo vim /opt/nginx/conf/nginx.conf

### 添加 redmine 的配置

    server {
        listen       80;
        server_name  redmine.zhouw; # 请替换成你网站的域名
        rails_env    production;
        root         /srv/www/redmine/public;
        passenger_enabled on;

        location ~ ^(/assets) {
            access_log        off;
            # 设置 assets 下面的浏览器缓存时间为最大值（由于 Rails Assets Pipline 的文件名是根据文件修改产生的 MD5 digest 文件名，所以此处可以放心开启）
            expires           max;
        }
    }


### 重新啟動 Nginx

    sudo /etc/init.d/nginx start
