---
date: 2012-02-17
layout:  post
title:  "上传文件夹"
tagline:
categories:
- web
tags:
- upload
---

最近公司的产品要用到上传目录的功能，所以查了一些资料，现记录下来。

现有的方案：

    http://www.cnblogs.com/xproer/archive/2010/10/24/1859895.html
        国内的收费版本，支持大部分微软的脚本语言，实用 Activex 控件实现

    http://slickupload.com/
        国外的，社区版免费，只支持最新版的浏览器，应该是html5的方式实现的

资料：

    http://blog.sina.com.cn/s/blog_4c6e822d0102dsma.html
        遍历上传目录的 asp.net 版本

    http://www.cnblogs.com/qingyuan/articles/1519057.html
        压缩目录上传再解压的例子 asp.net

    http://www.example-code.com/vbdotnet/ftpUploadTree.asp
        ftp 的方式上传文件 vb.net

    http://topic.csdn.net/t/20061110/15/5148605.html
        csdn 讨论贴

    http://q.cnblogs.com/q/24221/
        cnblog 讨论贴

    http://www.aurigma.com/docs/iu7/uploading-folders-in-aspnet.htm
        Uploading Folders in ASP.NET

    http://www.cnwing.net/u/catinnight/200982111713.shtml
        upload 说明

发现基本实现的思想基本上分以下几种：

 1. 使用组件，比如 Activex 组件或者 java 组件，这些组件都是需要客户端下载并同意使用的。例如，网易相册，QQ相册等。可惜，我不会写这些东西。
 2. asp.net 貌似可以通过遍历查询传递过来的目录下的内容，来批量将文件加入上传列表，来实现上传目录的功能。
 3. 使用zip等压缩工具压缩之后再上传，但是需要先授权调用外部的压缩程序，貌似也只有.net能做到这个吧。
 4. 使用ftp的方式上传，需要服务器开启ftp权限。

好吧，就这样，不知道经理怎么选，不过使用.net开发windows专用的网站看来还是比较简单的啊。
