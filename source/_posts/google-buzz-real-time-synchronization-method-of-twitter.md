---
date: 2011-03-12
layout:  post
title:  "Google Buzz实时同步Twitter的方法"
tagline:
categories:
- web
tags:
- buzz
---
<div>
<div id="artibody">

相比Twitter而说，Buzz目前还可以从国内访问，因此昨天<a href="http://www.williamlong.info/archives/2085.html" target="_blank">我那篇文章</a>的后面就有人咨询，是否能实现Buzz的微博同步到Twitter上，经过我的研究发现，这是可以实现的，而且同步几乎是实时的。

这主要归功于PubSubHubBub，可以实现RSS Feed的实时更新，而Google Buzz的RSS Feed和Google Reader一样，从一开始就支持PubSubHubBub，这使得Buzz的Feed变成实时的Feed，而恰好Google的另一个产品FeedBurner也支持PubSubHubBub的Feed，因此就可以通过这个来实现微博的实时同步。

具体同步Google Buzz到Twitter的方法是：在个人Profile页面找到自己Buzz的Feed，通常使用IE或Firefox进入 <a href="https://www.google.com/profiles/me" target="_blank">https://www.google.com/profiles/me</a> 后，会看到地址栏的RSS图标，点击后可看见RSS地址，这个地址格式类似：http://buzz.googleapis.com/feeds/112646999948608559077/public/posted 。

登录<a href="http://www.feedburner.com/" target="_blank">FeedBurner</a>，将上述Feed烧录，然后在Publicize里面，点Socialize，加入自己的Twitter帐号，格式选项中，选Body Only，不加Link，不留retweets空间，保存后就可以实现同步。设置界面如下图所示：

<img src="http://www.williamlong.info/upload/2086_1.jpg" alt="Google Buzz实时同步Twitter的方法">

同步的内容只有140个字，虽然Buzz是不限制字数的，但如果你想把Buzz当作微博客同步Twitter，那么还是将字数限制在140个字好一些。注意同步Twitter后，就不要再Buzz中再连接Twitter了，否则就搞成死循环了。

经过我的测试，使用FeedBurner将Google Buzz的Feed发布到Twitter，消息同步时间在一分钟内，基本是实时的，如果你想以Buzz为自己主要的微博客，那么就可以采用这种方法同步信息到Twitter，简单而快速。

从技术的角度我很喜欢Google Buzz，因为它支持PubSubHubBub，可以聚合其他网站内容（连新浪微博都支持同步博客信息），这些东西Twitter至今也不支持。有了实时的RSS，信息的快速传递就可以不依赖于某个平台（如Twitter），这大概就是Twitter至今也不想支持PubSubHubBub的原因吧。

</div>
</div>
<div>

除非注明，<a href="http://www.williamlong.info/">月光博客</a>文章均为原创，转载请以链接形式标明本文地址

本文地址：<a href="http://www.williamlong.info/archives/2086.html">http://www.williamlong.info/archives/2086.html</a>

</div>
 
