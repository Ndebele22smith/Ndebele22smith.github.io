---
layout: post
title: ubuntu上nginx+PHP7.1+mysql的安装及配置
categories: Linux
description: ubuntu上nginx+PHP7.1+mysql的安装和一些配置（php和nginx）
keywords: vagrant，ubuntu
---

ubuntu16.04上安装nginx+PHP7.1+mysql

## 初始工作——换源

换源就是更新软件的下载源，ubuntu如果没有换源的话，默认源是欧洲的，下载速度很慢，还有可能报一些404的错误，所以要换成国内的下载源，原来用的是清华的源，听学长说由于某大的原因清华源被墙了，并且推荐了较好的163源。

ubuntu的下载源在/etc/apt下的source.list中。

![sources.list](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/vim_sources.list.png)

把里面的内容备份后，换成163的源。

下面是ubuntu 16.04的163源

deb http://mirrors.163.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ xenial-backports main restricted universe multiverse

保存，退出后，执行下面的命令更新。

![update_apt](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/update_apt.png)

## 安装nginx

apt源更新好以后，就可以安装 nginx了

sudo apt-get install nginx

![install_nginx](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/install_nginx.png)

安装好以后可以 nginx -v 看一下nginx的版本

这时候启动nginx 并设置开机启动

![nginx_start](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/start_nginx.png)

然后访问192.168.33.10，可以看到welcome to nginx

![nginx](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/nginx.png)

## 安装PHP7.1

按以下命令安装PHP

![php_install](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/php_install.png)

安装后php -v 查看自己是否安装成

![](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/php-v.png)

这样PHP7.1就安装好了

## 安装mysql

然后安装mysql

![](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/mysql.png)

安装过程中会让输入root密码，切记啊！

![](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/mysql_install.png)

登录mysql以后 ```Ctrl+D ```退出mysql

## nginx和PHP的配置

### 设置php

```sudo  vim /etc/php/7.1/fpm/php.ini```

将```;cgi.fix_pathinfo=1```改成```cgi.fix_pathinfo=0```（```/```搜索）

### php-fpm

安装php-fpm

```sudo apt install php7.1-fpm```

重启php7.1-fpm

```sudo service php7.1-fpm restart```

### 配置nginx

Nginx的服务器配置文件在```  /etc/nginx/sites-available```的```default```

```sudo vim /etc/nginx/sites-available/default```

做以下修改

![](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/nginx_default.png)

然后重启 nginx

```sudo systemctl reload nginx```

在```/var/www```下增加test.php文件```sudo vim test.php```输入

```&amp;amp;lt;?php
<?php
    echo phpinfo();
?>
```

访问```192.168.33.10/test.php```可以看到

![](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/Linux/phpinfo.png)

说明配置成功啦！！！

