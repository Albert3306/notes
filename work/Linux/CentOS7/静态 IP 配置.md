# 静态 IP 配置

```Linux
# vim /etc/sysconfig/network-scripts/ifcfg-eth0 (不同网络配置文件可能会不太，根据实际情况修改)

BOOTPROTO=static #dhcp改为static（修改）
ONBOOT=yes #开机启用本配置，一般在最后一行（修改）

IPADDR=192.168.1.204 # 静态IP（增加）
GATEWAY=192.168.1.2 # 默认网关（增加）
NETMASK=255.255.255.0 # 子网掩码（增加）
DNS1=192.168.1.2 # DNS 配置，虚拟机安装的话，DNS就网关就行，多个DNS网址的话再增加（增加）

systemctl restart network.service # 重启网络服务 
```

