---
date: 2011-05-20
layout:  post
title:  "彻底解决sysfader: IEXPLORE.EXE应用程序错误"
tagline:
categories:
- web
tags:
- bug
---
今天碰到一个用户出现  sysfader: IEXPLORE.EXE应用程序错误，
<img src="/images/uploads/2011/05/3ca0bb3a49e2e6cac7829amp.jpg" alt="" title="sysfader: IEXPLORE.EXE应用程序错误" width="457" height="141" class="aligncenter size-full wp-image-2114">
这个用户的浏览器是IE8，这个错误只在IE8下出现，换了别的浏览器或者兼容模式都没问题，老大提醒说是JS有问题，但是。。。
<!--  more  -->
我检查了一下代码，别的用户怎么没这个问题，要知道JS都一样的啊，而且用户也没有自己引用JS啊【我们的产品允许用户用html代码编辑自己的主页】。。。

笨方法：一段一段删掉，看看还会不会报错，最后锁定了这段代码：

奇怪为什么单单IE8过滤不了这个，看来IE8也不咋地啊，对微软的产品真是印象很差啊。。。
看网上好多用户怎么怎么折腾的方法，其实这个问题还是要问网站的，要是网站代码写的很规范的话就不会出这个问题啦。。。\

	<font color="#00ff00" size="\"\'\\\"">
		<span>
			<span>
				<span>
					<span style="FONT-FAMILY: 宋体; COLOR: #0000ff; FONT-SIZE: 18px">
						<span style="COLOR: #00ffff">
							<span style="COLOR: #00ff00; FONT-SIZE: 18px">
								<span style="COLOR: #ff00ff; FONT-SIZE: 14px">
									<strong>
										百度空间地址：
									</strong>
								</span>
								<a href="http://hi.baidu.com/%C3%97%C3%97%C3%97%C3%97/space">
									<span style="COLOR: #00ff00; FONT-SIZE: 18px">
										<em>
											<strong>
												http://hi.baidu.com/××××/space
											</strong>
										</em>
									</span>
								</a>
							</span>
						</span>
					</span>
				</span>
			</span>
		</span>
	</font>



好嘛，你们看到了什么？
    size="\"\'\\\""
没错，就是它，看看你把自由给了用户，他们就会放些奇怪的东西进来，就是这句话    "\"\'\\\""    quot;"

，删掉所有的这些不能被IE8识别并编译的怪语句之后，搞定。。。

奇怪为什么单单IE8过滤不了这个，看来IE8也不咋地啊，对微软的产品真是印象很差啊。。。
看网上好多用户怎么怎么折腾的方法，其实这个问题还是要问网站的，要是网站代码写的很规范的话就不会出这个问题啦。。。
