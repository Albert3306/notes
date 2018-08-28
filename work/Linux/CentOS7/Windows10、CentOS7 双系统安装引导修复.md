# Windows10、CentOS7 双系统安装引导修复

	先安装 Windows10 再安装 CentOS7 后，重启后默认是进入的 CentOS7 的，必须要进入 grup 修复启动引导修复，才能自由切换两个系统。

## 修复方式

```Linux
# vim /boot/grub2/grub.cfg

定位到 ### BEGIN /etc/grub.d/30_os-prober ### 于###END###之间，输入以下命令
menuentry 'Windows 10' {    
set root=(hd0,msdos1)
chainloader +1
}

说明：
	并不是所有的电脑都是 set root='hd0,msdos1'，如果重启后选择新添加的启动项无法正常启动，那么可能就是这里的问题，解决的方法就是找到自己电脑对应的。重启在选择启动项时按 c 键便可以进入 grub 终端，然后输入命令：
# cat (hd0      然后按 tab 键 看到原win系统的Partition为 hd0,msdos1，如果不是，那么在修改grub.cfg文件时，改成对应的OK了！

```

