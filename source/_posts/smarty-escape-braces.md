---
date: 2011-01-18
layout:  post
title:  "smarty 花括号转义"
tagline:
categories:
- web
tags:
- smarty
---
使用 smarty 模板的时候，通常都是用 ‘{’ 和 ‘}’ 作为定界符（delimiter）。

有时，我们需要在 html 代码里输出大括号，如果在模板里直接写出来，会被 smarty 的解析器认为是定界符，然后会报错：

smarty error : syntax error: unrecognized tag
无法识别的标签！

如何解决呢？有 2 种办法：

1：内置变量

ldelim, rdelim
ldelim and rdelim are used for displaying the literal delimiter, in our case “{” or “}”. The template engine always tries to interpret delimiters, so this is the way around that.
ldelim 和 rdelim 用于输出分隔符，也就是大括号 ‘{’ 和 ‘}’。如果只是输出很少的几个大括号，请使用此方法。

2： 文本转义

我们经常会在 html 里写 javascript 函数，就不可避免地写大量的大括号，这个时候上面的解决方法就不适用了，smarty 提供了一个转义一段代码的标签：

  {literal}…{/literal}

    {literal}
        <script type="”text/javascript”">
        function sayHello() {alert(‘Hello World!’)}
        </script>
    {/literal}

这样，就可以在里面随意写各种符号，不必担心 smarty 引擎会错误解析了！
