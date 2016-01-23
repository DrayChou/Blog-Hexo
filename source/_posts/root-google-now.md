layout: post
title: "[root]一条命令开启 Google Now & 位置报告"
date: 2016-01-23 14:18:57
categories:
 - linux
tags:
 - linux
 - android
 - google now
---

使用 root 权限运行以下命令(重启后失效)

    setprop gsm.sim.operator.alpha "AT&T" && 
    setprop gsm.sim.operator.iso-country "us" && 
    setprop gsm.sim.operator.numeric "310090"

一段时间（几小时）后 Google Now 就能打开了