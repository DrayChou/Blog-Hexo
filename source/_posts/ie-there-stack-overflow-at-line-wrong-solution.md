---
date: 2011-02-25
layout:  post
title:  "IE中出现 \"Stack overflow at line\" 错误的解决方法"
tagline:
categories:
- web
tags:
- ie
---
出现该错误提示，主要有两种原因：

1. 使用系统的事件名称作为自定义函数名如：

onclick / onsubmit ... 都是系统保留的事件名称，不允许作为重定义函数名称。

2. 出现死循环 ：

如：在图片对象定义了 onerror 事件的循环处理、

<img src="http://www.hoocar.com/1.gif" onerror="this.src='/image/default.gif'" />

这里并不是说 1.gif 不存在， 可能是由于网络阻塞原因造成， 这时会执行 onerror 事件,

调用 /images/default.gif 去做当前图片的路径， 但如果当前 /image/default.gif 这个图片文件不存在，

再或者由于网络原因， 下载'/image/default.gif' 又出现错误， 这就出现了死循环。

通过<a href="http://chenchendefeng.javaeye.com/blog/456247">IE中出现 "Stack overflow at line" 错误的解决方法 - 小生学艺 - JavaEye技术网站</a>.
