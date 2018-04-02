# Git 仓库、账号创建和配置

[TOC]

## 1、创建 Git 的用户组、用户

```
groupadd git
useradd albert -g git
```

## 2、进入 /home/albert 创建 .ssh

```
mkdir .ssh  # 创建证书
chmod 700 .ssh  # 设置 700 权限
touch .ssh/authorized_keys  # 存放公钥
chmod 600 .ssh/authorized_keys  # 设置 600 权限
```

## 3、创建仓库

```
mkdir /data/git/repository
cd /data/git/repository

git init --bare xiaozhu.git
chown -R albert test.git
chgrp -R git test.git
chmod -R 755 test.git
chmod g+s -R test.git
```

## 4、开启服务，进入/etc/ssh 目录，编辑 sshd_config，打开以下三个配置的注释

```
cd /etc/ssh
vim sshd_config  # 去除下面三项的注释

RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysfile .ssh/authorized_keys

/etc/rc.d/init.d/sshd restart  # 重启 sshd
```

## 5、创建公钥，并将生成的公钥复制到 .ssh/authorized_keys

```
ssh-keygen -t rsa -C "youremail@example.com" 
```

## 6、上传同步到项目地址

```
# 进入仓库
cd /data/git/repository/xiaozhu.git/hooks
# 创建 post-receive 文件，并写入一下内容
vim post-receive

#!/bin/bash
git --work-tree=/home/www checkout -f
# 保存退出后，将该文件用户及用户组都设置成git
chown git:git post-receive
# 设置可执行权限
chmod +x post-receive
```

## 7、给 git 账号赋予 /data/www 文件的读写权限

```
vim /etc/passwd

chown -R git:git /data/www
```