# CentOS 7 防火墙、端口号配置

[TOC]

	CentOS 7 默认使用的是firewall作为防火墙，默认是没有开启 80、3306 端口的，这两个端口分别是网页和数据库所需要的端口。以下教程是把 firewall 改为 iptables 防火墙，同时开启 80 端口、3306 端口。这是在 CentOS 7 系统中布署 LNMP 或都 LAMP 环境必须做的一步设置，否则 Web 环境无法使用。

        当然，如果你不想安装 iptables 防火墙，那直接做关闭 firewall 这一步既可。现在一般 VPS 都应该有硬件防火墙了的。文章后面带有使用 firewall 作为防火墙开启 80、3306 端口教程。

## 1、关闭firewall

```Linux
systemctl stop firewalld.service # 停止 firewall
systemctl disable firewalld.service # 禁止 firewall 开机启动
```

## 2、安装 iptables 防火墙

```Linux
yum install iptables-services # 安装
vim /etc/sysconfig/iptables # 编辑防火墙配置文件

# Firewall configuration written by system-config-firewall
# Manual customization of this file is not recommended.
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT

:wq!  # 保存退出

systemctl restart iptables.service # 最后重启防火墙使配置生效
systemctl enable iptables.service # 设置防火墙开机启动

```

## 3、给 firewall 添加 80 和 3306 端口

在firewall正常运行的情况下输入以下命令。

```Linux
firewall-cmd --zone=public --add-port=80/tcp --permanent # 添加 80 端口
firewall-cmd --zone=public --add-port=3306/tcp --permanent  # 添加 3306 端口
```

显示 success 的话就代表已成功加入，重启 VPS 既可。

如果想检查相应端口是否开启，请输入以下代码：

```Linux
firewall-cmd --query-port=80/tcp --zone=public  # 查询 80 端口是否开启
```

返回 no 既未开启，显示 Yes 为已开启。

```Linux
systemctl start firewalld # 启动 firewall
systemctl enable firewalld # 开机启动 firewall
```



