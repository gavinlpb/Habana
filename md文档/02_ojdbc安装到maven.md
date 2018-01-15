# Maven 仓库安装 ojdbc8

​	oracle 12c 对应的的最新版 java 驱动下载地址 : [ojdbc8.jar](http://download.oracle.com/otn/utilities_drivers/jdbc/122010/ojdbc8.jar?AuthParam=1507889795_b1ca1f6a018d3a362dc04006bb114e29)

​	jar包解压后, 打开 `ojdbc8\META-INF\MANIFEST.MF` 文件 , 有如下内容 : 

```properties
  Manifest-Version: 1.0
  Ant-Version: Apache Ant 1.7.1
  Implementation-Title: JDBC
  Implementation-Version: 12.2.0.1.0
  sealed: true
  ............
```

​	其中 , `12.2.0.1.0` 为 jar 包的版本信息 . 下面说明安装过程 : 

1. ##### 下载 ojdbc8.jar

   下载连接见文章开头 , 这里我将下载的jar 包放在 d 盘下 , 即访问路径为 `d:\ojdbc8.jar`

2. ##### 进入 d 盘 ,  安装 jar 包到maven 仓库

   在 d 盘空白的地方 , 按住 `shift` + 鼠标右键 ,  选择  `再此处打开命令窗口`  , 然后输入如下内容 : 

```sh
mvn install:install-file -DgroupId=com.oracle -DartifactId=ojdbc8 -Dversion=12.2.0.1.0 -Dpackaging=jar -Dfile=d:\ojdbc8.jar
```

​	运行效果如下图 : 

```sh
D:\>mvn install:install-file -DgroupId
=com.oracle -DartifactId=ojdbc8 -Dversion=12.2.0.1.0 -Dpackaging=jar -Dfile=d:\o
jdbc8.jar
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- maven-install-plugin:2.4:install-file (default-cli) @ standalone-pom
---
[INFO] Installing d:\ojdbc8.jar to G:\01_MAVEN_RESPOTY\com\oracle\ojdbc8\12.2.0.
1.0\ojdbc8-12.2.0.1.0.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.902 s
[INFO] Finished at: 2017-10-14T09:17:57+08:00
[INFO] Final Memory: 6M/178M
[INFO] ------------------------------------------------------------------------
```

3. ##### 安装成功后 ojdbc 的坐标如下

```xml
		<dependency>
			<groupId>com.oracle</groupId>
			<artifactId>ojdbc8</artifactId>
			<version>12.2.0.1.0</version>
		</dependency>
```