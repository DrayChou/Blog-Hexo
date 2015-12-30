---
date: 2011-02-24
layout:  post
title:  被冤枉的file_exists
tagline:
categories:
- web
tags:
- file_exists
---
我在做项目的时候需要把图片进行压缩，当然进行压缩之前要先检查一下原图在不在，压缩完后也要检查一下新图有没有被压缩出来，但是我使用 file_exists 进行检查的时候却一直给我false。 代码如下： <div class="cnblogs_code">

    if (file_exists($desimage)) {
        $ok_num += 1;
    } else {
       $fail_num += 1;
    }


</div>仔细检查了一下才发现，我拿到的图片url中包含 汉字 ，例如：<div class="cnblogs_code">

    if (file_exists($desimage)) {
        $ok_num += 1;
    } else {
       $fail_num += 1;
    }


</div>而这些汉字在拿到的时候都会转变成 已编码的 URL 字符串，如：<div class="cnblogs_code">

    if (file_exists($desimage)) {
        $ok_num += 1;
    } else {
       $fail_num += 1;
    }


</div>那么很明显我通过  已编码的 URL 字符串 去到服务器中找这个文件是肯定找不到的。唉，郁闷了。。解决方法很简单:<div class="cnblogs_code">

    if (file_exists($desimage)) {
        $ok_num += 1;
    } else {
       $fail_num += 1;
    }


</div>记下以示警示！
