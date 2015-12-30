---
date: 2011-01-10
layout:  post
title:  "javascript 检查字符串是否是数字的几种方法"
tagline:
categories:
- web
tags:
- js
---
代码：

    //判断是否是正整数
    function IsNum(s)
    {
        if(s!=null){
            var r,re;
            re = /\d*/i; //\d表示数字,*表示匹配多个数字
            r = s.match(re);
            return (r==s)?true:false;
        }
        return false;
    }
    //判断是否为数字
    function IsNum(s)
    {
        if (s!=null && s!="")
        {
            return !isNaN(s);
        }
        return false;
    }
