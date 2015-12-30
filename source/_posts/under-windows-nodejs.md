---
date: 2011-12-26
layout:  post
title:  "Windows 下的 Nodejs"
tagline:
categories:
- windows
tags:
- nodejs
---

<h2>为什么搞这个？</h2>
<ol>
<li>公司电脑的权限管理比较严，不能安装软件，不能常驻系统进程等，所以像 xampp 之类的都不能正常执行</li>
	<li>我又想在空闲的时候做点东西</li>
	<li>所以坑爹的我只能自己研究在windows下运行nodejs了<!--more-->
</li>
</ol>
<h2>怎么执行？</h2>
<ol>
<li>下载并解压到一个目录</li>
	<li>进入目录双击 Start.bat 执行</li>
	<li>在命令行下执行

node ex_project\jade\app.jse\app.js</li>
</ol>
你会看到

    E:\nodejs4win>node ex_project\jade\app.js Express server listening on port 3000 in development mode

这样的结果，那么打开浏览器输入：

    E:\nodejs4win>node ex_project\jade\app.js Express server listening on port 3000 in development mode

OK，这样一个 nodejs + express + jade 的项目就跑起来了
<h2>所有 windows 都可以执行吗？</h2>
<ol>
<li>在 Windows Xp 下可以直接执行，不需要权限</li>
	<li>在 Windows 7 下本地执行的话不需要 windows 权限，局域网内执行的话，需要开放局域网访问的权限。</li>
</ol>
<h2>都有什么？</h2>
<ol>
<li>nodejs.exe -- windows 版 nodejs</li>
	<li>npm -- nodejs 的模板库管理工具，但windows下很多库都不能直接安装使用</li>
	<li>express -- mvc framework
<ol>
<li>jade -- template</li>
	<li>dot -- template</li>
	<li>ejs -- template</li>
	<li>Tenjin -- template</li>
	<li>jst -- template ，有错误，还未修复</li>
</ol>
</li>
	<li>dirty -- 因为windows 下数据库还不支持，所以只能采用一些其他的工具替换了。这个是目前我找到的最好的工具了。</li>
	<li>n2Mvc -- 国人开发的一个独立的轻型的mvc架构</li>
</ol>
<h2>怎么用？</h2>
<ol>
<li>刚接触nodejs的建议先从project 目录下的代码看起，从最简单的hello_world，到n2mvc，可以让你对Nodejs有一个初步的了解</li>
	<li>然后可以在express的模板中选一套主攻吧</li>
</ol>
<h2>这套环境可以用来生产吗？</h2>
你开玩笑呢？哥，这个只是让你折腾玩的，想到生产环境还是用linux吧，虽然我现在是做.net的，但我还是觉得windows不适合做服务器。
<h2>这些都是你写的吗？</h2>
不是，我只是把他们拼在一起。我会在后面给出他们的项目地址。
<h2>有文档可以参考吗？</h2>
<ol>
<li>nodejs官方文档：
http://nodejs.org/docs/latest/api/process.html#process.platform</li>
	<li>国内社区的翻译版（未完成）：http://cnodejs.org/cman/all.html</li>
	<li>nodecn 翻译的文档（未完成）：http://www.nodecn.org/all.html</li>
	<li>Express JS 中文入门指引手册：http://www.csser.com/tools/express-js/express-guide-reference-zh-CN.html</li>
</ol>
<h2>有问题了问谁？</h2>
<ol>
<li>可以去cnodejs.org社区提问</li>
	<li>可以去各项目主页发 Issues</li>
	<li>也可以直接在我的项目主页留言等，我会尽量解答</li>
</ol>
<h2>项目【下载】地址</h2>
https://github.com/DrayChou/nodejs4win
<h2>引用到的项目地址</h2>
<ol>
<li>nodejs : http://nodejs.org/</li>
	<li>express : https://github.com/visionmedia/express</li>
	<li>dirty : https://github.com/felixge/node-dirty</li>
	<li>n2Mvc : https://github.com/QLeelulu/n2Mvc</li>
	<li>jade : https://github.com/visionmedia/jade</li>
	<li>dot : https://github.com/olado/doT</li>
	<li>nTenjin : https://github.com/QLeelulu/nTenjin</li>
	<li>ejs : https://github.com/visionmedia/ejs</li>
	<li>jst : https://github.com/shaunlee/node-jst</li>
</ol>
