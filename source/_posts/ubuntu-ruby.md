---
date: 2013-04-15
layout:  post
title:  "ubuntu 安装 Ruby, Rails 运行环境"
tagline:
categories:
- linux
tags:
- ruby
---

步骤0 － 安装系统需要的包

Ubuntu 请安装

    $ sudo apt-get install -y build-essential openssl curl libcurl3-dev libreadline6 libreadline6-dev git zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev libxslt-dev autoconf automake libtool imagemagick libmagickwand-dev libpcre3-dev libsqlite3-dev libmysql-ruby libmysqlclient-dev

步骤1 － 安装 RVM

RVM 是干什么的这里就不解释了，后面你将会慢慢搞明白。

    $ curl -L https://get.rvm.io | bash -s stable

等待一段时间后就可以成功安装好 RVM。

然后，载入 RVM 环境（新开 Termal 就不用这么做了，会自动重新载入的）

    $ source ~/.rvm/scripts/rvm

检查一下是否安装正确

    $ rvm -v
    rvm 1.17.3 (stable) by Wayne E. Seguin <wayneeseguin@gmail.com>, Michal Papis <mpapis@gmail.com> [https://rvm.io/]

步骤2 － 用 RVM 安装 Ruby 环境

    # 替换 Ruby 下载地址到国内淘宝镜像服务器
    $ sed -i 's!ftp.ruby-lang.org/pub/ruby!ruby.taobao.org/mirrors/ruby!' $rvm_path/config/db
    # 安装 readline 包
    $ rvm pkg install readline
    # 安装 Ruby 2.0.0
    $ rvm install 2.0.0 --with-readline-dir=$rvm_path/usr

或者可以安装 1.8.7 版本，也可以是 1.9.3，只要将后面的版本号跟换一下就可以了
同样继续等待漫长的下载，编译过程，完成以后，Ruby, Ruby Gems 就安装好了。
步骤3 － 设置 Ruby 版本

RVM 装好以后，首先修改 .bashrc，将

    [[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"  # This loads RVM
    PATH=$PATH:$HOME/.rvm/bin # Add RVM to PATH for scripting

替换

    PATH=$PATH:$HOME/.rvm/bin # Add RVM to PATH for scripting

重启控制台，再执行下面的命令将指定版本的 Ruby 设置为系统默认版本

    $ rvm 2.0.0 --default

同样，也可以用其他版本号，前提是你有用 rvm install 安装过那个版本

这个时候你可以测试是否正确

    $ ruby -v
    ruby 2.0.0p0 (2013-02-24 revision 39474) [x86_64-darwin12.3.0]
    $ gem -v
    2.0.0
    $ gem source -r https://rubygems.org/
    $ gem source -a http://ruby.taobao.org

步骤4 － 安装 Rails 环境

上面 3 个步骤过后，Ruby 环境就安装好了，接下来安装 Rails

    $ gem install bundler rails

然后测试安装是否正确

    $ bundle -v
    Bundler version 1.0
    $ rails -v
    Rails 3.2.13
