---
date: 2011-02-18
layout:  post
title:  Notepad++去除代码行号的几种方法
tagline:
categories:
- web
tags:
- notepad
---
<strong>问：</strong>在网页中复制代码时，常常遇到高亮程序自动给代码加上行号或字符“#”，如何格式化？如下：  

    #1 //去除首字符或行号
    #2 & lt; ? php#100 echo '再长点';#............#2010 echo '无语了吧';#2012 ? >

<strong></strong>
<!--more-->

<strong>解1：</strong>手动删除，才2012行~~~不多不多.LOL

<strong>解2：</strong>打开 Notepad++，按住 Alt，鼠标点击拖出选择框，这个是<strong> 列选</strong> 方法，相当拉风；

<strong>解3：</strong>正则表达式（又是这个万能的东西）。

      打开 Notepad++，Ctrl+H，[查找目标] 输入 下面对应正则表达式 [查找模式] 选择 正则表达式 ，之后 Alt+A，搞定！

#+空格+行号  \S\s\d+
  <br>行号+空格      ^[0-9]+

  <br>行号+.+空格   \s*\d*\.\s

<strong>解4：</strong>使用 TextFX 工具

      打开 Notepad++，[全选代码]–点击 工具栏中的 [TextFX] –[TextFX Tools]–[Delete Line Numbers or First word] ，OK！

【补充给6楼<cite> kamal  </cite>同学】加行号的方法：[全选代码]–点击 工具栏中的 [TextFX] –[TextFX Tools]–[Insert Line Numbers] OK！

<strong>解5：</strong>编写 宏 命令

      打开 Notepad++，Alt+O 选择宏，开始录制：（光标初始在文首）<strong>注：</strong>全部键盘操作

<em><strong>宏流程</strong>：</em>[Home 键]—[Ctrl+Shift+方向键*右]—[Backspace]–[方向键*下]

<strong><em>释义：</em></strong>光标顶格—按单词字段选择–删除行首–下一行  //第二步根据情况操作N次。

以上是NP++中我用过的方法，至于其他编辑器应该还有解法，欢迎分享！

PS: 复制代码的时候，先观察下这个网站是不是有 [copy按钮] 可以避免复制到行号的！

版权所有© HzlzH | 本文采用 <a href="http://www.hzlzh.com/#copyright">BY-NC-SA</a> 进行授权

  <br>转载需注明 转自: 《<a href="http://www.hzlzh.com/notepad-delete-line-number/">Notepad++去除代码行号的几种方法</a>
