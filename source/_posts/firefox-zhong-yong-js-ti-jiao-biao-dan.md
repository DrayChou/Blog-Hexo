---
date: 2011-01-20
layout:  post
title:  firefox中用js提交表单
tagline:
categories:
- web
tags:
- js
---
<div class="postcontent">
    <span class="Apple-style-span">
        1.document.forms.from.submit();
        <!--more-->
        <br>
        document.form.sumbit();
        <br>
        document.form.submit.click();
        <br>
        this.form.submit();
        <br>
        以上几种形式的js表单提交在firefox浏览器下是不起作用的
        <br>
        2.必须遵循w3c标准：
        <br>
        1).获得form时应使用getElementById()方法
        <br>
        2).用.submit()方法提交表单
        <br>
        3).button的name/id绝对不能命名为”submit”
        <br>4).form中所有的组件（按钮，文本框等）的name/id也不能命名为”submit”
    </span>
    <span class="Apple-style-span">
        # 当提交按钮的name 或者 id为submit时候，用js 提交表单，表单名.submit()时候会报一个错误，提示对象不支持此属性或办法。
        <br>
        解决方法是修改提交按钮的 name 或者 id 不要与 submit或者action同名即可。
        <br>
        那么，请问为什么 当提交按钮的 name 或者 id为submit或者 action的时候 js提交表单会报错呢？这难道是 一个bug？
        <br>高手们请指教。。。。
    </span>
    <span class="Apple-style-span">
        因为”表单名.submit()提交”这种写法本身就是不符合W3C标准的规定的，在IE下没有报错因为IE支持这种写法，但是如果在FF下就会报错，要写成”document.getElementById(‘form id’).submit()”的？
    </span>
    <span class="Apple-style-span">
        <span class="Apple-style-span">
            我在项目中发现
            <input type=”submit”/>
            与
            <img src=”123.gif” onclick=”submit();”>
            <br>
            得出的效果截然不同， 谁能告诉我这两着有合不同
            <br>我又如何能用图片来替代原有的提交按钮
        </span>
    </span>
    <span class="Apple-style-span">
        是说这是一个按钮,它的是一个提交按钮.当点击它时,它会自动将它所在的表单进行提交.
    </span>
    <h2 class="related_post_title">相关阅读</h2>

</div>
