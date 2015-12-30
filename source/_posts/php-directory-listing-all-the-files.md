---
date: 2011-02-14
layout:  post
title:  php列出目录下的所有文件
tagline:
categories:
- web
tags:
- dir
---


    function myDir($dir = __file__)
    {
        // 定于需要列出的目录地址
        //$dir = dirname(__file__);
        // 用 opendir() 打开目录，失败则中止程序
        $handle = @opendir($dir) or die("Cannot open " . $dir);
        echo "<b>Files in " . $dir . ":</b><br>";
        // 用 readdir 读出文件列表
        while ($file = readdir($handle)) {
            // 将 "." 及 ".." 排除不显示
            if ($file != "." && $file != "..") {
                echo "$file<br>";
            }
        }
        // 关闭目录读取
        closedir($handle);
    }
