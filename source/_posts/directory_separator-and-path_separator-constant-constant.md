---
date: 2011-04-18
layout:  post
title:  DIRECTORY_SEPARATOR常量与PATH_SEPARATOR常量
tagline:
categories:
- linux
tags:
- seperator
---
DIRECTORY_SEPARATOR：路径分隔符，linux上就是’/’    windows上是’\’

PATH_SEPARATOR：include多个路径使用，在win下，当你要include多个路径的话，你要用”;”隔开，但在linux下就使用”:”隔开的。

这2个常量的使用能够避免不同平台的兼容性问题。

注意：

这两个常量并不是一直存在的，需要在编译的时候包含 Directory 库，或者在运行时被动态加载后才有效。

所以如果不敢确定这两个常量存在的话，可以用下面的语句：




    if(!defined('DIRECTORY_SEPERATOR')){
        if(strtoupper(substr(php_os, 0, 3)) === 'WIN')
        {
            define("DIRECTORY_SEPERATOR","\");
        }
        else
        {
            define("DIRECTORY_SEPERATOR","/");
        }
    }
