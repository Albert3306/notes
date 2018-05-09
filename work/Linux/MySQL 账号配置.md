# MySQL 账号配置

```
# 授权用户任意主机以账号和密码连接到mysql服务器，若想限制 IP 则将 '%' 换为对应的 IP
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'pwd' WITH GRANT OPTION;
mysql> flush privileges;
```

