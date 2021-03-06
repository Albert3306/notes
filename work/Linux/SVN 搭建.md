# CentOS 7 SVN 环境搭建

[TOC]



## 1、检查是否安装了低版本的 SVN

```Linux
 [root@localhost /]# rpm -qa subversion
```

## 2、卸载旧版本 SVN

```Linux
[root@localhost modules]# yum remove subversion
```

## 3、安装 SVN

```Linux
 [root@localhost modules]# yum -y install subversion
```

## 4、检验已经安装的 SVN 版本信息

```Linux
[root@localhost modules]# svnserve --version
```

## 5、SVN软件安装完成后还需要建立 SVN 库 

```Linux
 [root@localhost modules]# cd /opt/svn
 [root@localhost modules]# svnadmin create /opt/svn/objects
```

## 6、权限控制 authz 配置

```Linux
[root@localhost modules]# vi /opt/svn/objects/conf/authz

# 文件内容
[groups]
admin = test01,test02

[/]
@admin = rw
```

## 7、用户密码 passwd 配置

```Linux
[root@localhost modules]# vi /opt/svn/objects/conf/passwd

# 文件内容
[users]
test01 = 123456 # 账号密码
test02 = 123456
```

## 8、服务 svnserve.conf 配置，去掉下面列出的前面的 #

```Linux
[root@localhost modules]# vi /opt/svn/objects/conf/svnserve.conf

# 文件内容
[general]
#匿名访问的权限，可以是read,write,none,默认为read
anon-access=none
#使授权用户有写权限 
auth-access=write
#密码数据库的路径 
password-db=passwd
#访问控制文件 
authz-db=authz
```

## 9、启动 SVN 服务器

```Linux
[root@localhost modules]# svnserve -d -r /opt/svn/repositories
```

## 10、同步更新

```Linux
[root@localhost modules]# cd /opt/svn/objects/hooks
[root@localhost modules]# cp post-commit.tmpl post-commit
[root@localhost modules]# chmod -R 777 post-commit
[root@localhost modules]# vim /opt/svn/objects/hooks/post-commit

# 文件内容
#!/bin/sh
export LANG=zh_CN.UTF-8      # 文件的编码，自己看着办啦
SVN_PATH=/usr/bin/svn          # svn的执行文件目录，默认滴
WEB_PATH=/data/wwwroot/objects  # 项目路径

$SVN_PATH co --username test01 --password 123456 svn://127.0.0.1/objects $WEB_PATH
```

## 11、其他的 SVN 的一些操作

```Linux
[root@localhost modules]# ps -ef|grep svn|grep -v grep // 查看进程
[root@localhost modules]# netstat -ln |grep 3690 // 检测端口
[root@localhost modules]# killall svnserve    //停止
[root@localhost modules]# svnserve -d -r /opt/svn/repositories  // 启动
```

