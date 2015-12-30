---
date: 2011-01-28
layout:  post
title:  php删除文件unlink
tagline:
categories:
- web
tags:
- unlink
---
本文章来讲讲用php的unlink函数来删除文件和文件夹吧,下面来看看unlink的实例教程<div dir="ltr">你知道如何建立一个档案。您知道如何打开一个文件中各种各样的方式不同。你甚至不知道如何读取和写入数据从一个文件！ <br><br>现在是时候了解如何摧毁（删除）文件。在php中删除的文件通过调用中断功能。 <br><br>php的-文件unlink <br>当您查看的内容目录，您可以看到所有的档案，存在于该目录，因为作业系统或应用程序，您使用的是显示一个列表文件名。你可以把这些文件名作为链接，加入档案的目录您正在浏览。 <br><br>如果您断开的文件，你是有效的制度造成忘记它或删除它！ <br><br>在您可以删除（断开）的文件，你首先必须确保它无法打开您的程序。使用fclose函数关闭一个开放的档案。 <br><br>php的-文件unlink <br>请记住从php文件创建的教训，我们创建了一个文件，名为testFile.txt 。

	$myFile = "testFile.txt";
	$fh = fopen($myFile, 'w') or die("can't open file");
	fclose($fh);

判断是否删除了.

	$myFile = "testFile.txt";
	unlink($myFile);

删除文件.注明,删除文件夹在php里面只有文件夹为空时才能用unlink 进行删除操作.
