---
title: Java环境配置
categories:
- Java入门
tags:
- java
---

## 1、JDK下载

进入java SE的下载页面，找到JDK，点击下载。

<http://www.oracle.com/technetwork/java/javase/downloads/index.html>

## 2、环境变量配置

<https://blog.csdn.net/ZZQ928000/article/details/80373354>

从jdk-9之后就已经没有tools.jar和dt.jar了，也不需要在classpath里面配置这些jar了，配置可参考：

- JAVA_HOME=jdk安装路径
- JRE_HOME=jre安装路径
- PATH= ;%JAVA_HOME%\bin;%JRE_HOME%\bin
- CLASSPATH=.;%JAVA_HOME%\lib;%JRE_HOME%\lib

## 3、验证是否安装成功

Win + R --> 输入cmd -->进入控制台

```sh
java -version

where java

javac -version
```

## 4、安装Eclipse

<http://www.eclipse.org/>

点击Download，在Get Eclipse模块选择Download Packages，找到Eclipse IDE for Java EE Developers

选择Neon Packages版本，在右边找到下载链接，点击下载。

## 5、安装Tomcat9

<https://tomcat.apache.org/>

1、在左侧Download点击Tomcat 9,找到Core选择：64-bit Windows zip进行下载。

```sh
Binary Distributions

Core:

zip (pgp, sha1, sha512)
tar.gz (pgp, sha1, sha512)
32-bit Windows zip (pgp, sha1, sha512)
64-bit Windows zip (pgp, sha1, sha512)
32-bit/64-bit Windows Service Installer (pgp, sha1, sha512)
```

2、前提：正确安装jdk，并配置好系统变量例如：JAVA_HOME=jdk安装路径

3、打开cmd移动到tomcat安装目录的bin目录：

输入 service.bat install 安装服务，自动帮你配置好tomcat环境变量,如下图为正确安装：

```sh
C:\Users\longlong>d:

D:\>cd java/tomcat/apache-tomcat-9.0.10/bin

D:\java\tomcat\apache-tomcat-9.0.10\bin>service.bat install
Installing the service 'Tomcat9' ...
Using CATALINA_HOME:    "D:\java\tomcat\apache-tomcat-9.0.10"
Using CATALINA_BASE:    "D:\java\tomcat\apache-tomcat-9.0.10"
Using JAVA_HOME:        "D:\java\Java\jdk-10.0.1"
Using JRE_HOME:         "D:\java\Java\jre"
Using JVM:              "D:\java\Java\jdk-10.0.1\bin\server\jvm.dll"
The service 'Tomcat9' has been installed.
```

查看服务：按住win+R，打开运行，输入：services.msc

4、启动tomcat，有四种方法：

- 双击bin目录下的startup.bat批处理运行tomcat（这样的好处是可以看到运行状态，推荐使用）
- 以管理员运行cmd运行net start tomcat9命令（9是版本号）
- 通过任务管理器里面的服务运行
- 双击bin目录下的tomcat9w.exe打卡并点击start运行tomcat

5、浏览器中可以正常打开网页：<http://localhost:8080/>

6、卸载Tomcat:

```log
service.bat remove to Tomcat9
```
