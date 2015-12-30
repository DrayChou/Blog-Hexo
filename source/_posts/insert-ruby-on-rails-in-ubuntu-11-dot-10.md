---
date: 2012-02-29
layout:  post
title:  "在 ubuntu 11.10 下安装 Ruby on Rails"
tagline:
categories:
- linux
tags:
- ruby
- linux
---

1. 安装常用到组件

        sudo apt-get install git curl

2. 安装 rvm

    1.配置

        bash < <(curl -s https://rvm.beginrescueend.com/install/rvm)

    2.修改控制台配置文件，将 rvm 添加到命令控制台

        gedit ~/.bashrc

    3.在 .bashrc 最后添加

        [[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*

    4.更新控制台配置：

        source ~/.bashrc

    5.测试 rvm 是否正确安装

        type rvm | head -1

    如果显示出来 `rvm is a function` 或者 `rvm 是个函数` 那么就证明 rvm 安装成功

    6.执行 rvm 命令，查看都需要安装那些组件

        rvm requirements

    然后安装提示的内容安装必须到一些组件。

3. 安装 ruby

        rvm install 1.9.2
        rvm use 1.9.2

    调用 `ruby -v` 参加 ruby 是否安装成功

4. 安装 rails

        gem install rails

    新建 ROR 项目

        mkdir myapp
        cd  myapp/
        rails new demo
        cd demo
        rails server

至此，ubuntu 下的 ruby on rails 安装完毕，可以开始编程了。
