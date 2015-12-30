---
date: 2011-05-04
layout:  post
title:  清除页面中多余的css样式
tagline:
categories:
- web
tags:
- css
---
<strong>一、Dust-Me selectors</strong>

Dust-Me是一个很有用也很好用的Firefox插件，它可以分析到你的页面中调用的所有css文件并分析那些在页面中没有被用到。


- 支持本地和远程样式文件，包括使用`<link`>标签、`<?xml-stylesheet?`>处理指令、@import语句等方式引入的样式文件；(但是不支持页面中的`<style`>块和内联样式)

- 支持IE条件注释中引入的样式文件；

- 可以检查一个页面，也可以检查整个网站；

- 支持css1选择器、大部分css2和css3选择器；

- 理解通用的css hack，比如 “* html #fuck-ie”将会被认为是”html #fuck-ie”；

- 支持Firefox 3.5和Firefox 3.0，事实上得益于FF 3.5的js引擎的改进，FF 3.5中的性能比FF 3.0要高50%。

下载地址：https://addons.mozilla.org/en-us/firefox/addon/dust-me-selectors/

 

<strong>二、Page Speed</strong>

Page Speed是Google提供的一个前端性能分析工具，有些类似于YSlow，但是提供了一些比较个性且很有用的工具，比如Remove unused css：
Page Speed和YSlow一样依赖Firebug。

下载地址：http://code.google.com/intl/zh-CN/speed/page-speed/download.html

 

另附解除firefox版本兼容性限制的插件：https://addons.mozilla.org/zh-cn/firefox/addon/add-on-compatibility-reporter/
