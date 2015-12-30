---
date: 2015-08-03 15:30:00
layout:  post
title:  "让域名邮箱支持通配符"
tagline:
categories:
-  web
tags:
- mail
- domain
---

目前手贱收了一个域名，想配置成支持泛域名解析的邮箱地址，即随便写名称都可以寄到的邮件。

之前有用 QQ 企业邮箱做过一个泛解析的域名，规则是错误的邮箱地址都转发到一个固定地址，参见地址 [什么是错误地址转发功能？](http://service.exmail.qq.com/cgi-bin/help?subtype=1&&id=23&&no=1000815)。

后来 Google Domails 推出后，推出了域名 EMAIL 服务，支持 * 通配符，于是开心了，参见地址[About wildcard email forwarding](https://support.google.com/domains/answer/3251241?hl=en_US#wildcard)。

但是，新入的域名 Google Domails 不支持这种后缀，于是在 @duyaoo 的推荐下，用了 [mailgun](https://mailgun.com/) 服务。

这个服务本身是作为商业邮件API使用的，自用算是小 case 。

按照教程设置玩 DNS 之后，添加一条 routes 规则，指定 什么地址的邮件发送到那个邮箱就可以了。

以后做小项目的时候也可以用 mailgun 来做邮箱地址托管了，赞一个。

注：

	添加 mx 地址解析的时候 name 为 @
	re 域名注册地址：[internetbs.net](https://internetbs.net/)
