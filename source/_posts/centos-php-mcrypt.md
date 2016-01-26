layout: post
title: CentOS下php安装mcrypt扩展
date: 2016-01-26 22:41:04
categories:
- linux
tags:
- linux
- php
- mcrypt
---

## 确认你的linux没有安装mcrypt库，如果已安装，跳过安装步骤

```
[root@test-206 ~]# yum list installed|grep mcrypt
libmcrypt.x86_64                          2.5.8-4.el5.centos           installed
libmcrypt-devel.x86_64                    2.5.8-4.el5.centos           installed
mcrypt.x86_64                             2.6.8-1.el5                  installed
```
以上显示已经安装过，若没有，则按以下两种方式安装

### yum命令懒人安装

```
yum install libmcrypt libmcrypt-devel mcrypt mhash
```

执行后会显示即将安装的相关库，你可以根据你的linux限定x86_64或者i386，如yum install libmcrypt.x86_64（如果yum命令无法连接仓库，请检查你的/etc/yum.repos.d/里的文件正确性，以及你的/etc/host是不是可达里面的域名）

```
Dependencies Resolved

================================================================================
 Package              Arch        Version                   Repository     Size
================================================================================
Installing:
 libmcrypt            i386        2.5.7-5.el5               epel          124 k
 libmcrypt            x86_64      2.5.8-4.el5.centos        extras        105 k
 libmcrypt-devel      i386        2.5.7-5.el5               epel          103 k
 libmcrypt-devel      x86_64      2.5.8-4.el5.centos        extras         10 k
 mcrypt               x86_64      2.6.8-1.el5               epel           88 k
 mhash                i386        0.9.2-6.el5               epel          141 k
 mhash                x86_64      0.9.9-1.el5.rf            rpmforge      161 k

Transaction Summary
================================================================================
Install       7 Package(s)
Upgrade       0 Package(s)

Total download size: 731 k
Is this ok [y/N]:
```

确定安装，最后显示

```
Installed:
  libmcrypt.x86_64 0:2.5.8-4.el5.centos
  libmcrypt-devel.x86_64 0:2.5.8-4.el5.centos
  mcrypt.x86_64 0:2.6.8-1.el5
  mhash.x86_64 0:0.9.9-1.el5.rf

Complete!
```

### 源码编译安装

#### 去http://www.sourceforge.net下载Libmcrypt,mhash,mcrypt安装包 
```
libmcrypt(libmcrypt-2.5.8.tar.gz )：
mcrypt(mcrypt-2.6.8.tar.gz ):
mhash(mhash-0.9.9.9.tar.gz ):
```
####先安装Libmcrypt

```
#tar -zxvf libmcrypt-2.5.8.tar.gz
#cd libmcrypt-2.5.8
#./configure
#make
#make install 说明：libmcript默认安装在/usr/local 
```

#### 安装mhash

```
#tar -zxvf mhash-0.9.9.9.tar.gz
#cd mhash-0.9.9.9
#./configure
#make
#make install
```

#### 安装mcrypt

```
#tar -zxvf mcrypt-2.6.8.tar.gz
#cd mcrypt-2.6.8
#LD_LIBRARY_PATH=/usr/local/lib ./configure
#make
#make install
```

最后，还是检查下，是否安装成功

## 安装php的mcrypt扩展(动态加载编译)

下载php下的mcrypt扩展或者直接下载php的完整安装包

http://cn.php.net/releases/ 网页下找到自己服务器的php版本，下载后tar解压（本人的是php5.3.3）

进入ext/mcrypt文件夹

```
[root@*_* 14:45 ~]# cd php-5.3.3/ext/mcrypt/
```

执行phpize命令（phpize是用来扩展php扩展模块的，通过phpize可以建立php的外挂模块，如果没有？yum install php53-devel里包含了，或者其他方法）

```
[root@*_* 14:48 mcrypt]# whereis phpize    //为了确定phpize存在
phpize: /usr/bin/phpize /usr/share/man/man1/phpize.1.gz
[root@*_* 14:48 mcrypt]# phpize
Configuring for:
PHP Api Version:         20090626
Zend Module Api No:      20090626
Zend Extension Api No:   220090626
```

执行完后，会发现当前目录下多了一些configure文件，最后执行php-config命令就基本完成了

执行以下命令，确保你的/usr/bin/php-config是存在的

```
[root@*_* 15:02 mcrypt]# whereis php-config
php-config: /usr/bin/php-config /usr/share/man/man1/php-config.1.gz
[root@*_* 15:02 mcrypt]# ./configure --with-php-config=/usr/bin/php-config
```
如果遇到以下错误，请先安装gcc，命令yum install gcc
```
configure: error: no acceptable C compiler found in $PATH
```
直到不报错，出现：config.status: creating config.h，执行以下命令

```
[root@*_* 15:06 mcrypt]# make && make install
```
最后的最后，会提示你如下，说明你大功告成了

```
Installing shared extensions:     /usr/lib64/php/modules/
```
顺便检查下/usr/lib64/php/modules/里的mrcypt.so扩展是否已经创建成功

然后的事就简单了，给你的php.ini添加一条extension=mcrypt.so

```
[root@*_* 15:09 mcrypt]# cd /etc/php.d
```
创建一个mrcypt.ini文件就行，里面写extension=mcrypt.so

```
[root@*_* 15:17 php.d]# echo 'extension=mcrypt.so' > mcrypt.ini
```

## 重启apache，查阅phpinfo，mcrypt模块扩展是不是加载了？