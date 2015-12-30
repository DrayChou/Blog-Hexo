---
date: 2011-03-19
layout:  post
title:  用刚买的VPS主机做了一个镜像站
tagline:
categories:
- web
tags:
- vps
---
前天在 vpsyou 买了一个虚拟主机VPS，但是因为在家里的连接速度不佳被我退了，昨天又买了遨游的虚拟主机，速度还可以。
以下是安装过程：

1.首先，交钱，拿到自己的VPS的IP

2.用拿到的账户名+密码使用SSH登录VPS

3.到<a href="http://lnmp.org/"></a><a href="http://lnmp.org/install.html">http://lnmp.org/install.html</a>按教程安装lnmp，也就是linux,nginx,mysql,php,标准的建站套装

4.安装完毕，就可以通过访问你的IP地址来查看效果了，如果能看到成功页面，那恭喜你

5.在<a href="http://www.dot.tk/zh/index.html">http://www.dot.tk/zh/index.html</a>申请一个免费域名，然后   <span style="font-size: 15px; line-height: 18px;">使用Dot TK的免费DNS服务器   绑定A记录的IP地址到你的VPS IP,等域名生效，就可以通过域名来进行访问了。</span>

<span style="font-size: 15px; line-height: 18px;">6.打包之前的站，用wget下载到VPS，解压放到wwwroot目录，导入mysql数据</span>

<span style="font-size: 15px; line-height: 18px;">完成安装</span>

<span style="font-size: 15px; line-height: 18px;">示例：<a href="http://zh-x.tk/">http://zh-x.tk/</a></span>

<span style="font-size: 15px; line-height: 18px;">探针：<a href="http://zh-x.tk/tools/p.php">http://zh-x.tk/tools/p.php</a></span>

<span style="font-size: 15px; line-height: 18px;">ps:格式明天有空再搞，好困，4点了。</span>
