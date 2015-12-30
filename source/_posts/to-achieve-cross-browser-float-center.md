---
date: 2011-02-16
layout:  post
title:  "跨浏览器实现float:center"
tagline:
categories:
- web
tags:
- float
---
我们都知道float:left和float:right，但是否想过float:center呢？居中浮动。。。  <div>

    <div id="<span style="color: #8b0000">macji</span>">
        <ul <span style="color: #0000ff">class</span>="<span style="color: #8b0000">macji-skin</span>">
            <li>列表一</li>
            <li>列表二</li>
            <li>列表三</li>
        </ul>
    </div><br>


</div>

我们希望实现li是浮动的，并且居中的（li个数不固定，ul宽度未知）。可以设置ul的text-align:center,再设置li的display，可以实现居中，但这样不是我们的初衷，我们需要实现float:center。
<!--more-->



这里我们得先重温一下position:relative，它将依据left，right，top，bottom等属性在正常文档流中偏移位置。那我们可以让ul为position:relative;left:50%，然后再让li像左浮动，在让它position:relative;right:50%（或者left:-50%），那么li就像向中间浮动一样居中了。废话不多说，先试试。

<div>


    <div id="<span style="color: #8b0000">macji</span>">
        <ul <span style="color: #0000ff">class</span>="<span style="color: #8b0000">macji-skin</span>">
            <li>列表一</li>
            <li>列表二</li>
            <li>列表三</li>
        </ul>
    </div><br>


</div>

<strong><a href="http://www.blueidea.com/articleimg/2008/08/6130/float-center.htm"><strong>查看演示</strong></a></strong>

扩展阅读：
  <br><a href="http://matthewjamestaylor.com/blog/beautiful-css-centered-menus-no-hacks-full-cross-browser-support">http://matthewjamestaylor.com/blog/beautiful-css-centered-menus-no-hacks-full-cross-browser-support</a>

原文：
  <br><a href="http://www.macji.com/blog/article/to-achieve-cross-browser-css-float-center/to-achieve-cross-browser-css-float-center/">http://www.macji.com/blog/article/to-achieve-cross-browser-css-float-center/to-achieve-cross-browser-css-float-center/</a>

链接：<a href="http://www.blueidea.com/tech/web/2008/6130.asp">http://www.blueidea.com/tech/web/2008/6130.asp</a>
