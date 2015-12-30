---
date: 2014-04-11
layout:  post
title:  "记一次 wsdl 服务的调用"
tagline:
categories:
 - web
tags:
- wsdl
- soap
- php
- .net
---

公司业务要用到某 wsdl 的服务，使用 php5 自带的 soapclient 进行链接，屡次连不上，然后换 nusoap 包进行测试，还是不行，最后找到修改官方包 namespace 的方法才通过，记录下经验吧。

### soapclient

1. 官方推荐的调用对方函数的方法 _soapCall 函数调用如果失败，完全不输出任何信息。
2. 这个包无法查看对方返回的 http 状态。
3. 封装好的数据对方无法解析，直接报解析错误，需要继承并修改官方包，代码如下:

---

        class MSSoapClient extends SoapClient {
            function __doRequest($request, $location, $action, $version) {
                $namespace = "http://adc.ecinterface/";

                $request = preg_replace('/        $request = preg_replace('/        $request = str_replace(array('/ns1:', 'xmlns:ns1="' . $namespace . '"'), array('/', ''), $request);

                // parent call
                return parent::__doRequest($request, $location, $action, $version);
            }
        }

---

### nusoap

1. 发出去的数据因为不是系统级的封装，所以数据前会带上不少的噪音，对方完全无法识别。

### 总结
1. 对于不了解的还是要多祭拜谷歌大神。
2. 还是要多试。

### 参考地址
http://stackoverflow.com/questions/2456924/php-and-soap-change-envelope
