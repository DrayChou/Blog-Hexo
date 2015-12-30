---
date: 2012-02-06
layout:  post
title:  "Hello Octopress"
tagline:
categories:
- web
tags:
- Octopress
---

Octopress 是一个很不错的 blog 程序，好处我就不说了，自己查文档，现在把我安装时碰到的问题记录下来，供后来的朋友参考。

## 从wordpress导出数据 ##

我参考前面诸位写出来的ruby代码：[wordpress2Markdown](https://gist.github.com/1796343 "wordpress to Markdown")

这个ruby脚本的功能：

 - 循环匹配多种代码块，替换为 octopress 格式的代码块
 - 替换url中的汉字为拼音，并去掉不能转换的标点符号等
 - 输出文件到 ansi as utf-8 格式的文件中，避免中文字符乱码

## 我碰到的问题 ##

第一个:

    rake aborted!
    You have already activated rake 0.9.2.2, but your Gemfile requires rake 0.9.2. U
    sing bundle exec may solve this.
    (See full trace by running task with --trace)

解决：

    bundle exec rake

用上面的语句替代 rake 执行命令

第二个:

    * * Invoke generate (first_time)
    * * Execute generate
    # # Generating Site with Jekyll
    Unchanged sass/screen. Scss
    D: / RailsInstaller/Ruby1.9.2 / lib/ruby / 1.9.1 / psych. Rb: 148: in ` parse ': peasants' t par
    Se YAML at line 68 column 0 (Psych: : SyntaxError)

解决：

    _config.yml ':' 后面必须要有空格

第三个：

    D:\Dray\U\Git\MyOctopressBlogTest>bundle exec rake preview
    Starting to watch source with Jekyll and Compass. Starting Rack on port 4000
    [2012-02-10 09:24:37] INFO  WEBrick 1.3.1
    [2012-02-10 09:24:37] INFO  ruby 1.9.2 (2011-07-09) [i386-mingw32]
    [2012-02-10 09:24:37] INFO  WEBrick::HTTPServer#start: pid=7672 port=4000
    Configuration from D:/Dray/U/Git/MyOctopressBlogTest/_config.yml
    Auto-regenerating enabled: source -> public
    [2012-02-10 09:24:42] regeneration: 1730 files changed
    >>> Compass is polling for changes. Press Ctrl-C to Stop.
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml
    Liquid Exception: incompatible character encodings: UTF-8 and CP850 in atom.xml

解决：

    这个错误是因为 windows 下 cmd 默认用 ansi 格式的字符串来调用命令，解决的方法是：
    打开 shell|cmd 之后，先执行

        set LC_ALL=en_US.UTF-8
        set LANG=en_US.UTF-8

    然后再执行 rake 的命令。
    或者，在 d:\RailsInstaller\Ruby1.9.2\setup_environment.bat 的最后面加上这两句。

第四个：

    ## copying public to _deploy
    rake aborted!
    unknown file type: public/./blog/categories/??

解决：

这个就很郁闷了,categories 分类不能有中文的，现在嘛还无解

## 常用的编译提交命令 ##

    bundle exec rake generate && bundle exec rake deploy

## 常用的官方文档 ##

 - [Blogging Basics](http://octopress.org/docs/blogging "how to create blog posts and pages")
 - [Deploying Octopress](http://octopress.org/docs/deploying "simple deploy instructions for Rsync and Github pages")
 - [Sharing Code Snippets](http://octopress.org/docs/blogging/code "share code snippets with ease")
 - [Blogging With plugins](http://octopress.org/docs/blogging/plugins "overview of plugins for blogging")
 - [Theming & Customization](http://octopress.org/docs/theme "guide to making changes to your Octopress theme")
 - [Updating Octopress](http://octopress.org/docs/updating "a guide to help you stay current with Octopress")
