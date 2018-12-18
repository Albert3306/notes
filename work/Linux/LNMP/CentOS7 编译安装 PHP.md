# CentOS7 编译安装 PHP

[TOC]

## 1、安装前准备工作

```PHP
# 安装编译 PHP 需要的依赖包
yum install gcc autoconf gcc-c++
yum install libxml2 libxml2-devel openssl openssl-devel bzip2 bzip2-devel libcurl libcurl-devel libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel gmp gmp-devel readline readline-devel libxslt libxslt-devel
yum install systemd-devel
yum install openjpeg-devel

# 添加 php-fpm 用户
groupadd php-fpm
useradd -s /sbin/nologin -g php-fpm -M php-fpm
```

## 2、下载最新稳定版本 PHP，并安装

```PHP
# 下载最新 .tar.gz 安装包，官网地址：http://php.net/downloads.php
wget http://cn2.php.net/distributions/php-7.2.12.tar.gz

# 解压安装包
tar -zxvf php-7.2.12.tar.gz

# 进入安装包目录
cd php-7.2.12

# 加载配置文件
./configure \
--prefix=/usr/local/php \
--with-config-file-path=/usr/local/php/etc \
--with-zlib-dir \
--with-freetype-dir \
--enable-mbstring \
--with-libxml-dir=/usr \
--enable-xmlreader \
--enable-xmlwriter \
--enable-soap \
--enable-calendar \
--with-curl \
--with-zlib \
--with-gd \
--with-pdo-sqlite \
--with-pdo-mysql \
--with-mysqli \
--with-mysql-sock \
--enable-mysqlnd \
--disable-rpath \
--enable-inline-optimization \
--with-bz2 \
--with-zlib \
--enable-sockets \
--enable-sysvsem \
--enable-sysvshm \
--enable-pcntl \
--enable-mbregex \
--enable-exif \
--enable-bcmath \
--with-mhash \
--enable-zip \
--with-pcre-regex \
--with-jpeg-dir=/usr \
--with-png-dir=/usr \
--with-openssl \
--enable-ftp \
--with-kerberos \
--with-gettext \
--with-xmlrpc \
--with-xsl \
--enable-fpm \
--with-fpm-user=php-fpm \
--with-fpm-group=php-fpm \
--with-fpm-systemd \
--disable-fileinfo

# 编译并安装
make && make install
```

## 3、php.ini 配置

```PHP
# php.ini 配置，源码包中有两个：php.ini-development（测试开发环境） php.ini-production（生产环境）。根据自己需求复制一份到指定目录下
cp php.ini-production /usr/local/php/etc/php.ini

# 启动 php-fpm，并设置为开机自启动
systemctl start php-fpm.service
systemctl enable php-fpm.service
```

## 4、php-fpm.conf 配置

```PHP
# php-fpm 复制一份新的 php-fpm 配置文件
cd /usr/local/php/etc
cp php-fpm.conf.default php-fpm.conf
vim php-fpm.conf

# 配置错误日志
error_log = /usr/local/php/var/php-fpm.log

# 配置 pid 文件
pid = /usr/local/php/var/run/php-fpm.pid

# www.conf 文件配置
cd /usr/local/php/etc/php-fpm.d
cp www.conf.default  www.conf

# 管理 php-fpm 配置
cd /usr/local/src/php-7.2.12
cp ./sapi/fpm/php-fpm.service /usr/lib/systemd/system/php-fpm.service

# 添加环境变量，进入 /etc/profile 文件并在尾行增加代码
export PATH=$PATH:/usr/local/php/bin/

# 重新加载环境变量
source /etc/profile
```

## 5、php-fpm 常用命令

```PHP
# 启动
systemctl start php-fpm.service
	
# 停用
systemctl stop php-fpm.service
	
# 重启
systemctl restart php-fpm.service

# 版本号查看
php -v
```