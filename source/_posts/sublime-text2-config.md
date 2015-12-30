---
date: 2013-04-16
layout:  post
title:  "ubuntu 下 sublime text2 配置"
tagline:
categories:
-  ide
tags:
- sublimetext
---

习惯了 sublime text 2 在 ubuntu 下面也装了一个，下面是记录了我的一些配置

## 开启插件

如果 Package Control 已经安装成功，那么 Ctrl+Shift+P 调用命令面板，我们就会找到一些以“Package Control:”开头的命令，我们常用到的就是几个 Install Package (安装扩展)、List Packages (列出全部扩展)、Remove Package (移除扩展)、Upgrade Package (升级扩展)。但如果你按照上面的方法确实搞不定，可以试试按键盘 Ctrl+~ （数字1左边的按键）调出控制台，然后拷贝下面的代码进去并回车，它会自动帮你新建文件夹并下载文件的，与上面的方法最终效果是一样的：

    import urllib2,os; pf='Package Control.sublime-package'; ipp=sublime.installed_packages_path(); os.makedirs(ipp) if not os.path.exists(ipp) else None; urllib2.install_opener(urllib2.build_opener(urllib2.ProxyHandler())); open(os.path.join(ipp,pf),'wb').write(urllib2.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read()); print 'Please restart Sublime Text to finish installation'

## 常用插件

- BracketHighlighter: 大括號、中括號、括號家族高亮匹配
- Clipboard History：剪切板历史
- ConvertToUTF8：ST2只支持utf8编码，该插件可以显示与编辑 GBK, BIG5, EUC-KR, EUC-JP, Shift_JIS 等编码的文件
- cssFormat: css 格式化
- cssTidy: 整理与排版css代码
- ctags: 函数跳转
- CTags for php: php 支持文件
- Format sql: sql 格式化
- Github Tools: github 工具
- Gits：可以轻松集成 GitHub
- HtmlTidy：清理与排版你的HTML代码
- jQuery: jQuery支持插件
- JsFormat: 格式化js代码
- Markdown Preview: markdown 预览插件
- phpTidy：整理与排版php代码
- PythonTidy: python 代码整理插件
- SFTP：直接编辑 FTP 或 SFTP 服务器上的文件
- SideBarEnhancements: 侧栏右键功能增强，非常实用
- SublimeLinter: 一个支持lint语法的插件，可以高亮linter认为有错误的代码行，也支持高亮一些特别的注释，比如“TODO”，这样就可以被快速定位。
- sublimemerge: 文件比较
- YUI Compressor：压缩JS和css文件

## 输入法问题

### 快捷键冲突

在 preferences->key bindings-default 中，找到与输入法默认快捷键 ctrl+space 冲突的配置，复制并修改一份存到 key bindings- user 中。

### 输入法载入

看到网上帖子有各种 scim fcitx 等与 st2 配置的文章，但是照着做了一下，发现都不能正常调出。没办法，搜。
于是，有了这个 小小输入法 , 按照教程上面安装重启，于是可以输入拉。虽然还是有问题，比如不能删除输入的拼音，有时会崩溃，但是起码可以输入了，哎

### 小小输入法

- [官方安装教程](http://yong.uueasy.com/read.php?tid=128)
- [ubuntu 论坛安装教程](http://forum.ubuntu.org.cn/viewtopic.php?t=226677)
