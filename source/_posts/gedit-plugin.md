---
date: 2013-04-15
layout:  post
title:  "gedit 插件"
tagline:
categories:
- ide
tags:
- gedit
---

SublimeText 在 ubuntu 下面中文输入有问题，所以先把 gedit 配置起来盯着吧。

 - 安装插件包

        sudo apt-get install gedit-plugins

 - 安装 Gmate

        sudo apt-add-repository ppa:ubuntu-on-rails/ppa
        sudo apt-get update
        sudo apt-get install gedit-gmate

 - 安装 TextMate 自动补全插件

    Download the latest version [gedit-tm-autocomplete-1.0.5.tar.gz](http://code.google.com/p/gedit-tm-autocomplete/downloads/detail?name=gedit-tm-autocomplete-1.0.5.tar.gz) from the downloads page
    Extract the archive and run install.sh
    Restart Gedit
    Enable "TextMate Style Autocompletion" in Edit->Preferences->plugins

好了，就暂时这样用着吧
