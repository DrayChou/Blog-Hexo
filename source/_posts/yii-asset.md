---
layout: blog
title: yii2 用 asset 压缩js,css文件
date: 2017-07-10 17:44:00
categories:
- linux
tags:
- yii2
- asset
---

偶尔一次使用的东西，记一下！

## 安装 **java**
```
sudo apt-get install default-jre
```

## 安装压缩工具

### compiler
Yii 压缩 JavaScript 默认使用名为 compiler.jar 的 Google Closure compiler 压缩工具。
https://developers.google.com/closure/compiler/

### yuicompressor
Yii 压缩 CSS 使用名为 yuicompressor.jar 的YUI Compressor 压缩工具。
https://github.com/yui/yuicompressor/

## 生成默认配置脚本
```
yii asset/template asset.php
```

生成的模板如下:
```
<?php
/**
 * "yii asset" 控制台命令的配置文件
 * 注意控制台环境下有些路径别名可能不存在，如 '@webroot' 和 '@web'
 * 请先定义找不到的路径别名
 */

// In the console environment, some path aliases may not exist. Please define these:
Yii::setAlias('@webroot', __DIR__ . '/backend/web/');
Yii::setAlias('@web', '/backend/web/');

return [
    // 为 JavaScript 文件压缩调整 command/callback 命令：
    'jsCompressor' => 'java -jar compiler.jar --js {from} --js_output_file {to}',
    // 为 CSS 文件压缩调整 command/callback 命令：
    'cssCompressor' => 'java -jar yuicompressor.jar --type css {from} -o {to}',
    // 要压缩的资源包列表：
    'bundles' => [
        'backend\assets\AppAsset',
        // 'yii\web\YiiAsset',
        // 'yii\web\JqueryAsset',
    ],
    // 输出的已压缩资源包：
    'targets' => [
        'app\config\AllAsset' => [
            'basePath' => 'path/to/web',
            'baseUrl' => '',
            'js' => 'js/all-{ts}.js',
            'css' => 'css/all-{ts}.css',
        ],
    ],
    // 资源管理器配置：
    'assetManager' => [
        'basePath' => "@webroot",
        'baseUrl' => '@web',
    ],
];
```

## 执行脚本压缩生成配置文件
```
php yii asset/compress assets_backend.php backend/config/assets_compressed.php
```

## 把生成的配置文件加到主配置中
修改 config/main.php 添加下面的代码
```
'components' => [
    // ...
    'assetManager' => [
        'bundles' => require 'assets_compressed.php',
    ],
],
```

## 参考页面
http://www.yiifans.com/yii2/guide/structure-assets.html
http://www.cnblogs.com/zergling9999/p/6097783.html
http://mayi.so/article/4
