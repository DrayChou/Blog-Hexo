---
date: 2011-01-26
layout:  post
title:  "国外轻量级开源论坛系统vanilla Forums介绍"
tagline:
categories:
- web
tags:
- vanilla
---
<img title="vanilla Forums" src="http://www.latooni.cn/uploads/2010/12/screen-6.gif" alt="vanilla Forums" width="500" height="207"> <strong>简介</strong>
： <strong>vanilla Forums</strong>
是一套php+Mysql开源论坛。它的特点在于各种配置，功能，操作界面风格（
<strong>Themes</strong>
）都很简洁，素雅。另外vanilla默认会在首页中直接列出所有贴子，按照时间顺序，把最新的讨论贴放在最前面和概念中的论坛相比更加像博客。vanilla所有的功能和模块都是通过应用（
<strong>Applications</strong>
）和插件（
<strong>plugins</strong>
）来实现，是一款灵活的轻量级论坛程序。
<!--more-->
这两天都是在捣鼓这个东西，再加上家里有人来装修什么的，原本的计划都被打乱了。最初看到
<strong>vanilla Forums</strong>
（注目：不是吃的草莓……）是在煎蛋最初的论坛上面，当然那时还不知道这就是vanilla Forums，正式知道叫做vanilla Forums还是在09年的时候，当时在家无聊，于是就想搭个论坛玩玩什么的（当然后来并没有实行），当时国内的主流论坛程序大概有下面这些吧：phpwind 、Discuz、Dvbbs 、BBSMAX、BBSXP等，但一直以来都觉得这些论坛程序大多都是臃肿恶心的，尤其是当时SNS大行其道，有些论坛自然也连SNS也功能也整合进去了实在是无法忍受，现在回看，这些论坛带SNS的模式没有多少个是成功的。而我心中的论坛，外观上最起码应该是百度贴吧或者天涯或者水木清华或者小百合那样的，方便简单、明了直观。

于是就看看国外的开源程序，主流的有phpBB、MyBB、UseBB等，但这些离我心目中轻量级还有一段距离，于是就想到了早期在煎蛋看到过的讨论区，那时候再去煎蛋，煎蛋已经弃用了vanilla。不是很甘心，于是上php-open上面查看一下有什么收获没有，果然发现了vanilla Forums的踪迹，当时vanilla Forums的版本是1.1.9，界面如下，搭建后放了上一个空间商，发了一些帖子。但后来因为去了工作繁重的阿里同盟上班也就不了了之了。
<img title="vanilla Forums" src="http://www.latooni.cn/uploads/2010/12/screen-4.gif" alt="vanilla Forums" width="500" height="195">
两天前在网上看到有人在提及这个东东，于是就点上官网上看看。哈一上去就是惊喜vanilla Forums已经升级为2.0.16版本了，界面依然简介，虽说界面上比1.1.9版豪华了那么一点，但依然没有违背简约这个原则。最后还是将其下载下来摆弄了一两天，哈哈，最后分享一下这两天的中文配置经验和心得吧，不算完整也不完善，纯分享而已。vanilla Forums下载地址：
<a href="http://vanillaforums.org/download">http://vanillaforums.org/download</a>
安装环境，php4.1+和Mysql，这个不多说了。

新安装的vanilla Forums会自动开启两个应用， <em>vanilla</em>
和 <em>Conversations</em>
，其中vanilla是核心应用，禁用之后论坛不能被访问，看到有说官方有提供1.0版本和2.0版本vanilla应用，不过找过1.0版本的；Conversations是用户之间发私信的应用，禁用后不影响论坛使用，但用户之间则不能互发私信，而且Conversations可以提供多个用户之间相互聊天的功能，有点像多人聊天室。

中文语言包，国外的东西默认语言当然不会是中文了，但国内也有热心人士提供了中文语言包，下载地址是：
<a href="http://vanillaforums.org/addon/zh_cn-locale">点击这里</a>
。具体启用方法是：


解压文件后，将
<em>zh_CN</em>
文件夹移动的网站
<em>locales</em>
里边；
然后修改
<em>config/config.php</em>
文件中
<em>$Configuration['Garden']['Locale']</em>
选项；
改成
<em>$Configuration['Garden']['Locale'] = ‘zh-CN’;</em>
，如没有看到改选项的话就自己添加；
然后进入管理后台启用中文语言，注意是先修改后启用。


评价，该语言包翻译了前台绝大部分语言，我发现有一两个是遗漏的，当然如果添加了一些插件，则可能会不能全部翻译，这是可以自己通过修改语言包来达到目的。后台作者并没有翻译完整，不过对于老手老说英文后台不是太碍事，实在不行的话Google翻译一下大概能知道真正的意思。

时区，程序是通过读取
<em>php.ini</em>
这个配置文件来确定时区的，所以用户可以通过修改
<em>php.ini</em>
来修改成东8时区，如果不能修改
<em>php.ini</em>
的话，可以通过修改
<em>bootstrap.php</em>
来改成东8时区


解压文件后，将
<em>zh_CN</em>
文件夹移动的网站
<em>locales</em>
里边；
然后修改
<em>config/config.php</em>
文件中
<em>$Configuration['Garden']['Locale']</em>
选项；
改成
<em>$Configuration['Garden']['Locale'] = ‘zh-CN’;</em>
，如没有看到改选项的话就自己添加；
然后进入管理后台启用中文语言，注意是先修改后启用。


中文用户名，论坛使用邮箱注册，可以自定义用户名，但默认只能是英文的，可以通过以下方法来实现定义中文用户名


解压文件后，将
<em>zh_CN</em>
文件夹移动的网站
<em>locales</em>
里边；
然后修改
<em>config/config.php</em>
文件中
<em>$Configuration['Garden']['Locale']</em>
选项；
改成
<em>$Configuration['Garden']['Locale'] = ‘zh-CN’;</em>
，如没有看到改选项的话就自己添加；
然后进入管理后台启用中文语言，注意是先修改后启用。


使用中文名之后会出现一些小问题，比如产看中文名用户资料页面会出现错误，原本@加上用户名之后可以通知被@的用户还有点击可以跳转到用户资料页面，但对中文名用户失效，原有#加上英文单词可以跳转到搜索页面，类似话题模式，但论坛本身本没有识别中文分词什么的，所以#之后加上中文内容不能点击进行搜索，下面提供解决方案

/profile/用户名 可以访问到用户资料


解压文件后，将
<em>zh_CN</em>
文件夹移动的网站
<em>locales</em>
里边；
然后修改
<em>config/config.php</em>
文件中
<em>$Configuration['Garden']['Locale']</em>
选项；
改成
<em>$Configuration['Garden']['Locale'] = ‘zh-CN’;</em>
，如没有看到改选项的话就自己添加；
然后进入管理后台启用中文语言，注意是先修改后启用。


@用中文名用户 和点击链接


解压文件后，将
<em>zh_CN</em>
文件夹移动的网站
<em>locales</em>
里边；
然后修改
<em>config/config.php</em>
文件中
<em>$Configuration['Garden']['Locale']</em>
选项；
改成
<em>$Configuration['Garden']['Locale'] = ‘zh-CN’;</em>
，如没有看到改选项的话就自己添加；
然后进入管理后台启用中文语言，注意是先修改后启用。


#中文话题 搜索


解压文件后，将
<em>zh_CN</em>
文件夹移动的网站
<em>locales</em>
里边；
然后修改
<em>config/config.php</em>
文件中
<em>$Configuration['Garden']['Locale']</em>
选项；
改成
<em>$Configuration['Garden']['Locale'] = ‘zh-CN’;</em>
，如没有看到改选项的话就自己添加；
然后进入管理后台启用中文语言，注意是先修改后启用。


通过上面的修改，可以将中文话题以#话题#的形式点击跳转，类似各大微博，但对于中文搜索依然不可用。
<strong>- plugs</strong>
推荐
程序初期提供了16个插件，但并非感觉上并不是每个都用到，下面就写一写我这两天测试推荐使用插件。
<strong>adsense</strong>
，顾名思义，就是Google adsense的插件，将广告添加在主题帖之后。
<strong>EasyReply</strong>
，通过这个插件，帖子会提供一个链接，点击之后会在回复框自动添加@用户名 来提醒用户有人回帖了。
<strong>Emotify
  <img src="http://www.latooni.cn/wp-includes/images/smilies/icon_smile.gif" alt=":)"></strong>
，表情插件，再回复框左上角添加了既可爱又操蛋的表情按钮。
<strong>IE6 Update</strong>
，虽然官方说vanilla Forums是兼容IE 6的，但经过测试由JQuery实现的弹窗在IE 6下其实是不兼容的，所以用这个插件来提醒一下吧，貌似国外IE 6基本已经绝迹了，但国内用的还是很多。
<strong>Magic</strong>
，通过这个插件，jpg、jpeg、gif、png这四种格式的图片只要在文本框直接添加图片路径就会自动转换成图片了，要注意的是，这个插件的功能对主题帖是不起作用的，只对回帖起作用，你可以通过在
<em>$Sender->EventArguments['Comment']->Body = $this->MakeView($Sender->EventArguments['Comment']->Body);</em>
之后添加
<em>$Sender->EventArguments['Discussion']->Body = $this->MakeView($Sender->EventArguments['Discussion']->Body);</em>
这段语句，则插件对主题贴也起作用了。
<strong>Post Count</strong>
，有了这个插件，可以统计出用户的发帖数。
<strong>Quotes</strong>
，提供引用功能的插件，不过有一个不足，就是如果原帖有1000字，则如果引用的话会1000字全部引用，可以通过修改JS文件来实现只引用100字之类的，这个暂时没改。
<strong>HtmLawed</strong>
，用了屏蔽有害Html代码插件。
<strong>Embed vanilla</strong>
，通过这个插件，vanilla Forums允许使用js将整论坛嵌入到一个页面中，在选用一个合适的主题效果不错，如图所示。
<img title="wordpress-vanilla-1" src="http://www.latooni.cn/uploads/2010/12/wordpress-vanilla-1.png" alt="wordpress-vanilla-1" width="500" height="232">
<img title="wordpress-vanilla-2" src="http://www.latooni.cn/uploads/2010/12/wordpress-vanilla-2.png" alt="wordpress-vanilla-2" width="500" height="243">
备用插件：
<strong>Facebook</strong>
，用Facebook账号登陆论坛的插件。
<strong>Twitter</strong>
，用Twitter账号登陆的插件。
<strong>GoogleSignIn</strong>
，用Google账号登陆的插件。
天朝里边以上3个插件的作用不大。
<strong>FileUpload</strong>
，允许用户上传附件的插件。
<strong>Cleditor</strong>
，基于JQuery驱动的一款可视化编辑器，个人对可视化编辑器比较无爱。
<strong>Following</strong>
，用户互粉插件。
<strong>WhosOnline</strong>
，用户在线显示插件。
<strong>Gravatar</strong>
，这个插件可以使用户调用Gravatar头像，不过vanilla Forums本身允许用户上传自定义头像，所以作用不大。

嗯先写这么一些吧，毕竟插件还没全部用过，而且部分英文看不懂，Goggle翻译出来的也不是太靠谱。
vanilla Forums除了提供帖子讨论功能之外，还用动态分享和收藏帖子功能，动态分享功能有点像QQ空间和腾讯朋友的动态分享功能，就是简约一点吧。
<img title="wordpress-vanilla-3" src="http://www.latooni.cn/uploads/2010/12/wordpress-vanilla-3.png" alt="wordpress-vanilla-3" width="500" height="340">
最后总结一下，其实vanilla Forums并不是一款符合国情的程序，不过就是符合我自己口味罢了，程序控和代码控也不防下来看看。

from:
<a href="http://www.latooni.cn/?p=504">http://www.latooni.cn/?p=504</a>
