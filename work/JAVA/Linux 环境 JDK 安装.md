# Linux 环境 JDK 安装

1、下载对应的 JDK 版本，可到官网去下载

2、接着就是解压 tar.gz 的文件，可将解压后的文件放到自定义路径下（名称也可以自定义，我这里就叫 java）

3、修改环境变量

```Linux
$ sudo vi /etc/profile

export JAVA_HOME=/data/java # 这里的路径就是解压后的 JDK 包
export JRE_HOME=${JAVA_HOME}/jre
exportCLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

$ source /etc/profile

可以在命令行运行 java，看是否安装成功。或者 java -version 查看 java 的版本
```

