# SonarQube 代码测试工具安装

1. 下载 SonarQube 安装包，根据情况下载对应的版本

2. 下载到本地后并解压，进入` sonarqube/conf` 目录下，打开配置文件 sonar.properties

   ```Linux
   # 如果是其他数据库，将 mysql 改为相应的名称即可（注：需要去除这些配置前面的 #）
   sonar.jdbc.username=root
   sonar.jdbc.password=root
   sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance  
   sonar.web.host=0.0.0.0  
   sonar.web.context=/
   sonar.web.port=9090 # 端口号可自定义
   ```

3. 修改 wrapper.conf 中 `wrapper.java.command=java` 的 Java 路径改为绝对路径（我的是：`/data/java`）

4. 修改 `sonarqube/bin`  的读写权限 `chmod -R 777 bin` ,并启动 `./bin/linux-x86-64/sonar.sh start`

5. 中文语言包安装

   ```Linux
   # 从 GitHub 上下载语言包 https://github.com/SonarQubeCommunity/sonar-l10n-zh
   
   # 下载后放入到 extensions\plugins 下，重启
   ```


