---
date: 2011-05-12
layout:  post
title:  webqq中自适应宽度的JS代码和隐藏页面横向滚动条的css样式
tagline:
categories:
- web
tags:
- js
---
webqq 中 自适应宽度的JS代码


    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.2.6/jquery.min.js"></script><script src="http://web.qstatic.com/jsapi/alloy.api.js"></script><script type="text/javascript">
        try {
            alloy.onReady(function(){
                if($(window).width()<1026){
                    alloy.window.setBodySize({width: 1026,height: $(window).height()})
                };
            });
        }catch(e){ }

        $(window).resize(function(){
            var w = $(window).width();
            var h = $(window).height();
            $("#iyaya_iframe").css({
                width: w>1026?w-16:1016,
                height: h,
            });
        });
    </script>


隐藏横向滚动条的方法：

	<span style="color: #ff0000;">给 html 设置 overflow-x: hidden</span>

 
