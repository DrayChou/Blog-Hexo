---
date: 2014-04-11
layout:  post
title:  "关于通过 PushBullet API 推送信息的设想"
tagline:
categories:
 - web
tags:
- api
- PushBullet
- twitter
---

### 坑

我不喜欢 twitter 官方客户端 ，感觉官方客户端里 Timeline 乱乱的，平常都是使用 twidere 来用的。
但是 twidere 目前不支持推送，要实现推送必须有自己的服务器，自己的 google 注册应用，略麻烦了点，于是想到了 PushBullet ,如果她有 API 多好，查了下，果然有，然后一个“坑”出现了。

### PushBullet

PushBullet API 的官方介绍地址在这里 [戳我](https://www.pushbullet.com/api) ,她的 API 太简单了，简直是我见过的最简单的 API 了。通篇上下只有2个接口，简单看下文档就会了，现说下注意事项。

#### api key

1. 这个每个注册帐号都有一个，不区分开发账户，也没有开发账户，查看地址在：[登录后查看](https://www.pushbullet.com/account)
2. 查询的时候需要调用 http 默认的 BasicAuth 认证方式，用户名就是 api key ，密码为空。

#### 然后

然后你就可以不停的推送了，如果要推送给别人，也需要先得到对方的 api key ，至于推送给好友， 可以通过 get 的方式得到对方的 ID。

### GO

1. https://www.pushbullet.com/api
2. http://stackoverflow.com/questions/11361431/authenticated-http-client-requests-from-golang
3. http://golang.org/pkg/net/http/#Request.SetBasicAuth
