---
date: 2011-05-17
layout:  post
title:  利用jquery自动生成导航目录
tagline:
categories:
- web
tags:
- jquery
---

翻译自：<a target="_blank" href="http://www.jankoatwarpspeed.com/post/2009/08/20/Table-of-contents-using-jQuery.aspx">http://www.jankoatwarpspeed.com/post/2009/08/20/Table-of-contents-using-jQuery.aspx</a>
原文提供了3种样式，但是基本思想都是一样，那就是利用jquery选择器找到文章中的h1,h2,h3标签，修改这个标签的ID并生成对应的锚点链接地址。

第一种：

文章内容应该类似这样，由h1,h2,h3等标签分隔：

    <div id="toc"></div>
        <div id="content">
        <h1>Title goes her</h1>
        <h2>Subtitle goes here</h2>
        Text goes here...
    </div>

JS部分

    $("#toc").append('In this article:')
    $("h1, h2, h3").each(function(i) {
        var current = $(this);
        current.attr("id", "title" + i);
        $("#toc").append("<a id='link" + i + "' href="#title%22%20+%0A%20%20%20%20%20%20%20%20i%20+%20%22" title='" + current.attr("tagName") + "'>" +
            current.html() + "</a>");
    });

JS替换后的结果

    <div id="toc">
    In this article:
    <a id="link0" title="H1" href="#title0">Article title</a>
    <a id="link1" title="H2" href="#title1">Header Level 2</a>
    <a id="link2" title="H3" href="#title2">Header Level 3</a>
    <a id="link3" title="H3" href="#title3">Header level 3 again</a>
    <a id="link4" title="H3" href="#title4">Header level 3 once again</a>
    </div>
