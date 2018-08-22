# WampServer3.0.6 PHP 多版本安装

##1、下载需要安装的 PHP 版本 ，我这里以 7.1.21 为例

```
# 首先需要清楚自己已有 WAMP 中 PHP 是 NTS 还是 TS，可以用 phpinfo() 函数查看，并下载对应版本的 PHP
下载地址：https://windows.php.net/download/

# 下载完成后，解压到 /bin/php/ 目录下，并更名为 php7.1.21
```

## 2、配置 php.ini 文件

```
# 进入到 /bin/php/php7.1.21 目录，复制 php.ini-development 更名为 php.ini

# 在 php.ini 文件第 747 行添加如下代码
; http://php.net/extension-dir
; extension_dir = "./"
; On windows:
; extension_dir = "ext"
extension_dir ="E:/wamp64/bin/php/php7.1.21/ext/" // 这里的地址为实际安装的绝对路径

# 复制 php.ini 更名为 phpForApache.ini
```

## 3、配置 wampserver.conf 

```
# 从已有的 PHP 版本目录中复制一份 wampserver.conf，我复制的是 php7.0.10，如果安装的是 php5.* 的版本的话，则复制 php5.6.25 目录下的
```

## 4、修改 WAMP 配置文件 wampmanager.ini 

```
# 进入 WAMP 安装根目录，找到 wampmanager.ini 并打开

# 搜索 `phpVersion` 大概在 482 行，添加如下代码
Type: item; Caption: "5.6.25"; Action: multi; Actions:switchPhp5.6.25
Type: item; Caption: "7.0.10"; Action: multi; Actions:switchPhp7.0.10; Glyph: 13
Type: item; Caption: "7.1.21"; Action: multi; Actions:switchPhp7.1.21

# 找到下面的代码，并复制到后面
[switchPhp7.0.10]
Action: service; Service: wampapache64; ServiceAction: stop; Flags: ignoreerrors waituntilterminated
Action: run; FileName: "E:/wamp64/bin/php/php5.6.25/php-win.exe";Parameters: "switchPhpVersion.php 7.0.10";WorkingDir: "E:/wamp64/scripts"; Flags: waituntilterminated
Action: run; FileName: "E:/wamp64/bin/php/php5.6.25/php.exe";Parameters: "switchMysqlPort.php 3306";WorkingDir: "E:/wamp64/scripts"; Flags: waituntilterminated
Action: run; FileName: "E:/wamp64/bin/php/php5.6.25/php-win.exe";Parameters: "refresh.php";WorkingDir: "E:/wamp64/scripts"; Flags: waituntilterminated
Action: run; FileName: "net"; Parameters: "start wampapache64"; ShowCmd: hidden; Flags: waituntilterminated
Action: resetservices
Action: readconfig;

# 更为
[switchPhp7.1.21]
Action: service; Service: wampapache64; ServiceAction: stop; Flags: ignoreerrors waituntilterminated
Action: run; FileName: "E:/wamp64/bin/php/php5.6.25/php-win.exe";Parameters: "switchPhpVersion.php 7.1.21";WorkingDir: "E:/wamp64/scripts"; Flags: waituntilterminated
Action: run; FileName: "E:/wamp64/bin/php/php5.6.25/php.exe";Parameters: "switchMysqlPort.php 3306";WorkingDir: "E:/wamp64/scripts"; Flags: waituntilterminated
Action: run; FileName: "E:/wamp64/bin/php/php5.6.25/php-win.exe";Parameters: "refresh.php";WorkingDir: "E:/wamp64/scripts"; Flags: waituntilterminated
Action: run; FileName: "net"; Parameters: "start wampapache64"; ShowCmd: hidden; Flags: waituntilterminated
Action: resetservices
Action: readconfig;

# 退出 WAMP 并重新启动，就可以自由切换 php7.1.21 版本了

```

