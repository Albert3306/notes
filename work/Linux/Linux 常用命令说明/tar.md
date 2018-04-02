# 命令详解

## 参数

-c ：建立一个压缩文件的参数指令(create 的意思)；
-x ：解开一个压缩文件的参数指令！
-t ：查看 tarfile 里面的文件！
特别注意，在参数的下达中， c/x/t 仅能存在一个！不可同时存在！
因为不可能同时压缩与解压缩。
-z ：是否同时具有 gzip 的属性？亦即是否需要用 gzip 压缩？
-j ：是否同时具有 bzip2 的属性？亦即是否需要用 bzip2 压缩？
-v ：压缩的过程中显示文件！这个常用，但不建议用在背景执行过程！
-f ：使用档名，请留意，在 f 之后要立即接档名喔！不要再加参数！
　　　例如使用『 tar -zcvfP tfile sfile』就是错误的写法，要写成
　　　『 tar -zcvPf tfile sfile』才对喔！
-p ：使用原文件的原来属性（属性不会依据使用者而变）
-P ：可以使用绝对路径来压缩！
-N ：比后面接的日期(yyyy/mm/dd)还要新的才会被打包进新建的文件中！

--exclude FILE：在压缩的过程中，不要将 FILE 打包！

范例一：查阅上述 /tmp/etc.tar.gz 文件内有哪些文件

[root@linux ~]# **tar -ztvf /tmp/etc.tar.gz**
\# 由於我们使用 gzip 压缩，所以要查阅该 tar file 内的文件时，
\# 就得要加上 z 这个参数了！这很重要的！

范例二：将 /etc/ 内的所有文件备份下来，并且保存其权限！

[root@linux ~]# **tar -zxvpf /tmp/etc.tar.gz /etc**
\# 这个 -p 的属性是很重要的，尤其是当您要保留原本文件的属性时！

范例三：在 /home 当中，比 2005/06/01 新的文件才备份
[root@linux ~]# **tar -N '2005/06/01' -zcvf home.tar.gz /home**

范例四：我要备份 /home, /etc ，但不要 /home/dmtsai
[root@linux ~]# **tar --exclude /home/dmtsai -zcvf myfile.tar.gz /home/\* /etc**