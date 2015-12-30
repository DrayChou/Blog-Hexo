---
date: 2011-04-26
layout:  post
title:  "Proxy Switchy! 可以打开https，打不开http的解决方法"
tagline:
categories:
- web
tags:
- proxy
---
之前的我Proxy Switchy!代理规则开启的时候，只能打开https的页面，比如https://www.google.com，但是打不开http的页面，比如：http://www.google.com。

这让我很困惑！

后来查了一些资料，自己做了一些测试发现了！

因为我用的是ssh的方式proxy的，所以我应该使用 “SOCKS 代理” ，但是我之前选的是 “HTTP 代理”，而且选了 “对所有协议均使用相同的代理服务器”，这样一来，我访问页面的时候，https还好说，突破性本来就强，但是http就被阻隔到本地了，而我的ssh是不不会proxy的，所以唉。。。。

删掉其他的http,https,ftp代理服务器，只留一个“SOCKS 代理”就可以了，记得选 <label>SOCKS v5 </label>

留此文以做纪念！
