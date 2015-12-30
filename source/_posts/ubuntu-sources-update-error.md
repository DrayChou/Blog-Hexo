---
date: 2013-04-15
layout:  post
title:  "ubuntu sources update error"
tagline:
categories:
- linux
tags:
- sources
---

今天在执行 apt-get update 的时候报错，报错内容如下：

    W: Duplicate sources.list entry http://extras.ubuntu.com/ubuntu/ precise/main amd64 Packages (/var/lib/apt/lists/extras.ubuntu.com_ubuntu_dists_precise_main_binary-amd64_Packages)
    W: Duplicate sources.list entry http://extras.ubuntu.com/ubuntu/ precise/main amd64 Packages (/var/lib/apt/lists/extras.ubuntu.com_ubuntu_dists_precise_main_binary-amd64_Packages)
    W: Duplicate sources.list entry http://extras.ubuntu.com/ubuntu/ precise/main i386 Packages (/var/lib/apt/lists/extras.ubuntu.com_ubuntu_dists_precise_main_binary-i386_Packages)
    W: Duplicate sources.list entry http://extras.ubuntu.com/ubuntu/ precise/main i386 Packages (/var/lib/apt/lists/extras.ubuntu.com_ubuntu_dists_precise_main_binary-i386_Packages)
    W: You may want to run apt-get update to correct these problems

在网上搜索后得知，这是因为以上几条，与

    deb http://extras.ubuntu.com/ubuntu precise main
    deb-src http://extras.ubuntu.com/ubuntu precise main

冲突了，于是修改这部分源代码为：

    # deb http://security.ubuntu.com/ubuntu quantal-security main restricted
    # deb-src http://security.ubuntu.com/ubuntu quantal-security main restricted
    deb http://security.ubuntu.com/ubuntu quantal-security universe
    deb-src http://security.ubuntu.com/ubuntu quantal-security universe
    deb http://security.ubuntu.com/ubuntu quantal-security multiverse
    deb-src http://security.ubuntu.com/ubuntu quantal-security multiverse

    ## Uncomment the following two lines to add software from Canonical's
    ## 'partner' repository.
    ## This software is not part of Ubuntu, but is offered by Canonical and the
    ## respective vendors as a service to Ubuntu users.
    # deb http://archive.canonical.com/ubuntu quantal partner
    # deb-src http://archive.canonical.com/ubuntu quantal partner

    ## This software is not part of Ubuntu, but is offered by third-party
    ## developers who want to ship their latest software.
    deb http://extras.ubuntu.com/ubuntu quantal main
    deb-src http://extras.ubuntu.com/ubuntu quantal main

注释掉两条重复的，于是，ok了
