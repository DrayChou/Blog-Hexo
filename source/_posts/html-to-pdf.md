---
date: 2017-06-02
layout:  post
title:  "html 转为 pdf"
tagline:
categories:
- linux
tags:
- vps
---

1. 使用 wkhtmltopdf
    1. 安装
        1. 下载地址：https://wkhtmltopdf.org/downloads.html
        2. Linux 环境下， 0.12.4 版本有问题，需要使用 0.12.3 版本。
        3. 不要使用 apt install 的方式安装，安装的为 0.12.4 版本。

    2. 示例代码
        1. python
```
    import pdfkit

    pdfkit.from_url('https://wkhtmltopdf.org/docs.html', 'out.pdf')
    # pdfkit.from_file('test.html', 'out.pdf')
    # pdfkit.from_string('Hello!', 'out.pdf')
```
        2. php
```
    <?php

    include './vendor/autoload.php';

    use mikehaertl\wkhtmlto\Pdf;

    if (empty($_GET['url'])) {
        die();
    }

    $pdf = new Pdf($_GET['url']);
    $pdf->send();
```
