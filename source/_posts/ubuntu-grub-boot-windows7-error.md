---
date: 2013-04-15
layout:  post
title:  "ubuntu grub boot windows7 error"
tagline:
categories:
- linux
tags:
- grub
---

手贱，我修改了双系统中 win7 的启动顺序，修改的时候，用的是下面的方法：

    在Ubuntu终端下输入：
    $sudo vim /etc/default/grub
    sudo是使用root权限，vim是用vi文本编辑器打开etc文件夹下的default文件夹下的grub文件。
    在打开的文本中修改“GRUB_DEFAULT=0”这一项。比如win7在启动项列表中为第5项，则将0改为4。就是win7在启动项列表中的项数减1。
    （这里还可以修改该在启动项列表等待的时间，即修改“GRUB_TIMEOUT=所要等待的秒数”，-1表示不倒计时。）
    修改完后按[Ctrl]+X，会提示是否保存，输入Y，提示保存的文件名，还是原来的grub文件，所以直接回车确定。
    $sudo update-grub，更新一下grub。

然后重启的时候，默认的选项确实也变成了 win7 ，但是进入后确提示：

    a disk read error occurred Press Ctrl+Alt+del

这个问题折腾了一下午加一晚上才修复，这里顺手记下，省得以后再犯错。

因为出错的时候事实上，我的 windows7 有一个独立的 100mb boot 引导分区，这个分区正常来说应该可以引导我的 windows7 进入系统的。
但是，不知道为什么，就是不行，后来我修改启动文件，把 windows7 的引导指向 c 盘的那个分区，还是不行。再后来，我直接把那 100mb 的引导分区，update grub 还是不行。
没辙，google 之，搜到 boot-repair[https://help.ubuntu.com/community/Boot-Repair]。下载下来，修复一次，然后用 windows cd 修复一次引导，ok,完好如初。
