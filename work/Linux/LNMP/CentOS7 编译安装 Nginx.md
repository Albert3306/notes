# CentOS7 编译安装 Nginx

[TOC]

## 1、安装前准备工作

```PHP
# gcc 安装
#安装 nginx 需要先在官网下载的源码进行编译，编译依赖 gcc 环境，如果没有 gcc 环境，则需要安装
yum install gcc-c++

# PCRE pcre-devel 安装
# nginx 的 http 模块使用 pcre 来解析正则表达式，pcre-devel 是使用 pcre 开发的一个二次开发库
yum install -y pcre pcre-devel

# zlib 安装
# zlib 库提供了很多种压缩和解压缩的方式。因为我是最小安装，所以需要安装这些库。如果已经安装了解压工具则不需要安装
yum install -y zlib zlib-devel

# OpenSSL 安装
# OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用
yum install -y openssl openssl-devel

# 创建组
groupadd nginx 

# 创建账号到组
useradd -g nginx -d /home/nginx nginx

# 创建密码
passwd nginx
```

## 2、下载最新稳定版的 Ningx，并安装

```PHP
# 下载最新 .tar.gz 安装包，官网地址：https://nginx.org/en/download.html 
wget https://nginx.org/download/nginx-1.14.1.tar.gz

# 解压安装包
tar -zxvf nginx-1.14.1.tar.gz

# 进入安装包目录
cd nginx-1.14.1

# 加载配置文件
./configure \
--user=nginx --group=nginx \          #安装的用户组
--prefix=/usr/local/nginx \           #指定安装路径
--with-http_stub_status_module \         #监控nginx状态，需在nginx.conf配置
--with-http_ssl_module \             #支持HTTPS
--with-http_sub_module \             #支持URL重定向
--with-http_gzip_static_module          #静态压缩

# 编译并安装
make && make install
```

## 3、nginx 命令全局执行设置

```HTML
cd /usr/local/nginx/sbin/
ln -s /usr/local/nginx/sbin/nginx /usr/local/bin/nginx
```

## 4、设置开机自启动

```HTML
cd /etc/rc.d
sed -i '13a /usr/local/nginx/sbin/nginx' /etc/rc.d/rc.local
chmod u+x rc.local
```

## 5、关闭防火墙

```HTML
systemctl stop firewalld.service
systemctl disable firewalld.service
```

## 6、Nginx 常用命令

```PHP
# 启动
systemctl start nginx.service
	
# 停用
systemctl stop firewalld.service
	
# 重启
systemctl restart firewalld.service

# 测试配置文件 nginx.conf 正确性
nginx -t

# 版本号查看
nginx -v
```