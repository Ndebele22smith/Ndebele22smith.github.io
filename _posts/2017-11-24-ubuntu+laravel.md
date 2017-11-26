---
layout: post
title: ubuntu上安装composer和laravel
categories: laravel
description: ubuntu上laravel开发环境的安装（php和nginx）
keywords: vagrant, ubuntu, laravel
---

ubuntu上安装PHP框架laravel。

## 准备

### 服务器要求

laravel框架对系统的要求可以用Laravel Homestead 虚拟机满足，如果不使用Homestead作为开发环境需要服务器符合以下要求：

> PHP >= 7.0.0
>
> PHP OpenSSL 扩展
>
> PHP PDO 扩展
>
> PHP Mbstring扩展
>
> PHP Tokenizer 扩展
>
> PHP XML 扩展

### 安装PHP扩展

![](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/laravel/php_laravel.png)

### 安装配置composer

#### 安装composer

依次输入下面命令安装composer

```
php -r "copy('https://install.phpcomposer.com/installer','composer-setup.php');"下载安装脚本 － composer-setup.php － 到当前目录。
```

```
php composer-setup.php执行安装过程
```

```
php -r "unlink('composer-setup.php');"删除安装脚本
```

全局安装

```
sudo mv composer.phar /usr/local/bin/composer
```

安装完以后```composer -v```

![composer](https://raw.githubusercontent.com/Dielizhijie/Dielizhijie.github.io/master/images/posts/laravel/composer.png)

说明安装成功了。

#### 配置composer

修改composer的全局配置文件

```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

然后执行```composer selfupdate```

## 安装配置laravel

安装laravel

```
composer global require "laravel/installer=~1.1"
```

配置laravel

```export PATH="~/.config/composer/vendor/bin:$PATH"```添加环境变量

并填加在```/etc/bash.bashrc```执行```source ~/.bashrc```让环境变量立即生效

然后就去```/var/www```新建一个laravel项目

```laravel new laravel```
在laravel new的时候会报几个文件没有权限，直接给777权限就OK了。


修改laravel目录权限

```
sudo chown -R :www-data /var/www/laravel
sudo chmod -R 775 /var/www/laravel/storage
```

然后laravel就弄好了，跑起来吧。

