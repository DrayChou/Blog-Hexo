---
date: 2011-01-28
layout:  post
title:  "XML CDATA"
tagline:
categories:
- web
tags:
- xml
---
<h2 align="left">CDATA</h2>
<strong>CDATA 内部的所有东西都会被解析器忽略。</strong>假如文本中包含了大量的 "<" 和 "&" 字符 - 就像编程代码中经常出现的情况一样 - 那么这个 XML 元素就可以被定义为一个 CDATA 部分。CDATA 区段开始于 <em>"<![CDATA["</em>，结束于 <em>"]]>"</em>：<!--more--><div align="left">

<script><![CDATA[function matchwo(a,b){if (a < b && a < 0)   {   return 1   }else   {   return 0   }}]]></script>

</div>在上面的例子中，在 CDATA 区段中的所有东西都会被解析器忽略。<h3 align="left">关于 CDATA 区段的注释：</h3>CDATA 区段不能包含字符串 "]]>"，所以，CDATA 区段的嵌套是不被允许的。同时也需要确保在 "]]>" 字符串中没有空格或折行。<div><a title="Wiz，个人知识管理，PKM。" href="http://wiz.cn">通过Wiz发布</a></div>
