---
date: 2011-01-08
layout:  post
title:  bluehost下主域名和附加域目录路径的自定义
tagline:
categories:
- web
tags:
- bluehost
---

<span style="line-height: 18px;">bluehost在默认情况下，主域名和附加域目录路径如下：<br style="line-height: normal;"><br style="line-height: normal;">/home/youraccount/public_html/ (主域名对应目录)<br style="line-height: normal;">/home/youraccount/public_html/subfolderB (附加域名B)<br style="line-height: normal;">/home/youraccount/public_html/subfolderC (附加域名C)<br style="line-height: normal;"><br style="line-height: normal;">从上面的路径结构可以看出：主域名所对应的目录/public_html中包含有“附加域名B”和“附加域名C”这两个文件夹，如果你希望让上述三者成为并列关系，可以使用.htaccess命令来灵活定制。<br style="line-height: normal;"><br style="line-height: normal;">例如实现这种目录结构：<br style="line-height: normal;"><br style="line-height: normal;">/home/youraccount/public_html/subfolderA (主域名对应目录)<br style="line-height: normal;">/home/youraccount/public_html/subfolderB (附加域名B对应目录)<br style="line-height: normal;">/home/youraccount/public_html/subfolderC (附加域名C对应目录)<br style="line-height: normal;">用文本编辑器编辑.htaccess文件，内容修改和参照下面的代码：<!--more-->

<strong>具体的写法如下</strong></span>
<span style="line-height: 18px;">说明：将yourmaindomain.com替换成你的主域名；subfolder是你更改后的主域名的根目录名；最后将该.htaccess文件放到public_html目录即可。现在开始清理你的public_html目录吧，还你一个干干净净的主目录。[<a style="text-decoration: none; color: #6495ed;" title="参考" href="http://helpdesk.bluehost.com/index.php/kb/article/000347" target="_blank">参考</a>]

<strong>英文版</strong></span>
<span style="line-height: 18px;">subfolder替换你在public_html/下建立的目录,yourmaindomain.com替换为你的域名。</span>
