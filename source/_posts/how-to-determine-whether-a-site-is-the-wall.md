---
date: 2011-02-16
layout:  post
title:  如何判断一个网站是否被墙
tagline:
categories:
- web
tags:
- gfw
---
大家都知道GFW 平日作恶多端，一旦有网站不能访问，很多人都把矛头直指它了…. 虽然一般都是它干的，但实际上也不排除一些人别有用心…. 那么下面就来简单判断一下吧…  方法是用windows的tracert（<strong>打开命令提示符，输入tracert 域名</strong>）命令追踪路由，也可以直接用<a href="http://tool.chinaz.com/Tracert/">http://tool.chinaz.com/Tracert/</a>， 这个能显示ip所在地理位置，比windows自带的好。一般来说，无论是被GFW屏蔽的还是网站封IP的，我们总是能查到这个网站的IP地址，比如 Facebook，因为域名指向的ip是域名注册机构的dns服务器保留的，一般不会被封，所以，使用tracert命令就可以追踪路由了。 <!--more-->    如果网站被GFW封掉了，那么就是在中国国际出口被阻挡了，路由过不去，只能走其他地方，比如，我们追踪Facebook的路由，因为在大陆国际出口被阻 挡，所以不可能从出口结点（如北京，上海，广州等地）直接到达美国，而是在出口结点处断开或者尝试绕道，这样就基本可以判定是被k了。 如图所示：  <img height="307" src="http://hiphotos.baidu.com/9422e/pic/item/156160f299c151890a46e0da.jpg" width="430">  <strong>我们可以看到，在第四处超时了。至于原因就是上面所说的。大陆国际出口被阻挡，所以不可能从出口结点直接到达美国</strong>..  如果是网站封大陆IP，比如美国的一个网站封了大陆ip，tracert命令追踪，tracert命令发现被追踪网站在美国，肯定从国际出口出去，走美国 线路，但是在最后一跳超时，因为网站封了你的IP，但是前面多少跳都是可以访问的，能看到前面有美国的路由线路…  我没找到封大陆ip的网站，大个比方把，<strong>比如xxx.com 封了大陆ip，你用tracert命令追踪的时候，发现前面的都是正常的，等到最后一次，就会发现超时了… 这样也基本肯定这个网站是封了大陆ip…</strong>  from:http://www.heavenalex.com/?p=476
