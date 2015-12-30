---
date: 2011-01-28
layout:  post
title:  php检测用户是否使用代理上网的方法
tagline:
categories:
- web
tags:
- proxy
---


  获取用户IP地址的三个属性的区别(HTTP_X_FORWARDED_FOR,HTTP_VIA,REMOTE_ADDR)

一、没有使用代理服务器的情况：
实例：

      REMOTE_ADDR = 158.41.30.94
      HTTP_VIA = 没数值或不显示
      HTTP_X_FORWARDED_FOR = 没数值或不显示


二、使用透明代理服务器的情况：Transparent Proxies
下例中，实际IP=158.41.30.94，使用代理服务器IP=210.51.46.227

      REMOTE_ADDR = 210.14.65.69 (最后一个代理服务器 IP)
      HTTP_VIA = 1.1 shopex:80 (squid/2.6.STABLE4), 1.0 briage.shopex.cn:81 (squid/2.5.STABLE14)
      HTTP_X_FORWARDED_FOR = 158.41.30.94, 210.51.46.227


   这类代理服务器还是将您的信息转发给您的访问对象，无法达到隐藏真实身份的目的。


三、使用普通匿名代理服务器的情况：Anonymous Proxies
下例中，实际IP=158.41.30.94，使用代理服务器IP=210.51.46.227

      REMOTE_ADDR = 210.14.65.69
      HTTP_VIA = 1.1 shopex:80 (squid/2.6.STABLE4), 1.0 briage.shopex.cn:81 (squid/2.5.STABLE14)
      HTTP_X_FORWARDED_FOR = 210.51.46.227


   隐藏了您的真实IP，但是向访问对象透露了您是使用代理服务器访问他们的。


四、使用欺骗性代理服务器的情况：Distorting Proxies
下例中，实际IP=158.41.30.94，使用代理服务器IP=210.51.46.227

      REMOTE_ADDR = 210.14.65.69
      HTTP_VIA = 1.1 shopex:80 (squid/2.6.STABLE4), 1.0 briage.shopex.cn:81 (squid/2.5.STABLE14)
      HTTP_X_FORWARDED_FOR = ×××.××.××.××, 210.51.46.227

   告诉了访问对象您使用了代理服务器，但编造了一个虚假的随机IP ×××.××.××.×× 代替您的真实IP欺骗它。


五、使用高匿名代理服务器的情况：High Anonymity Proxies (Elite proxies)
下例中，实际IP=158.41.30.94，使用代理服务器IP=210.51.46.227，WEB服务器根本获取不到实际的IP地址

      REMOTE_ADDR = 210.51.46.227
      HTTP_VIA = 没数值或不显示
      HTTP_X_FORWARDED_FOR = 没数值或不显示


	完全用代理服务器的信息替代了您的所有信息，就象您就是完全使用那台代理服务器直接访问对象。
ss
