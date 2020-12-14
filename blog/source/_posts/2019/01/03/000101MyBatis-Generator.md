---
title: MyBatis Generator
date: 2019-01-03 00:01:01
categories:
- mybatis
tags:
- mybatis
---

官网：<http://mybatis.org/generator/index.html>

参考：<https://blog.csdn.net/gnail_oug/article/details/80404870>

## 1、下载

访问github地址：<https://github.com/mybatis/generator>

在 Release 页面下载 mybatis-generator-core-1.4.0-bundle.zip

解压下载的文件，创建目录test

复制 mybatis-generator-core-1.4.0.jar 到目录test
复制 mysql-connector-java-8.0.14.jar 到目录test

## 2、创建配置文件

generatorConfig.xml

```xml
<!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
  
  <classPathEntry location="./mysql-connector-java-8.0.14.jar" />

  <!-- 
  MyBatis3DynamicSql 默认值
  MyBatis3Simple MyBatis3 运行时的简化版本，javaClientGenerator的type="XMLMAPPER"才生效
  内部标签有顺序要求
  -->
  <context id="mysql" targetRuntime="MyBatis3Simple">

    <!-- 注释配置 -->
    <commentGenerator>
      <property name="addRemarkComments" value="true" />
      <property name="suppressDate" value="true" />
    </commentGenerator>

    <!-- 数据库连接 -->
    <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
      connectionURL="jdbc:mysql://127.0.0.1:3306/test?characterEncoding=UTF-8&amp;useSSL=false&amp;useUnicode=true&amp;serverTimezone=Asia/Shanghai"
      userId="root"
      password="root">
      <property name="nullCatalogMeansCurrent" value="true" />
    </jdbcConnection>

    <!-- 生成POJO对象，并将类放到top.woilanlan.example.bean包下 -->
    <javaModelGenerator targetPackage="top.woilanlan.example.bean" targetProject="src/main/java" />

    <!-- 生成mapper xml文件，并放到top.woilanlan.example.bean包下 -->
    <sqlMapGenerator targetPackage="top.woilanlan.example.mapper" targetProject="src/main/java"></sqlMapGenerator>

    <!-- 生成mapper xml对应dao接口，放到top.woilanlan.example.mapper包下-->
    <javaClientGenerator targetPackage="top.woilanlan.example.mapper" targetProject="src/main/java" type="XMLMAPPER" />

    <!-- table标签可以有多个，至少一个，tableName指定表名，可以使用_和%通配符 -->
    <table tableName="t_book">
        <!-- 是否只生成POJO对象 -->
        <!-- <property name="modelOnly" value="false"/> -->
        <!-- 数据库中表名有时我们都会带个前缀，而实体又不想带前缀，这个配置可以把实体的前缀去掉 -->
        <domainObjectRenamingRule searchString="^T" replaceString=""/>
    </table>
  </context>
</generatorConfiguration>
```

## 3、执行

在test目录，打开命令行工具执行

在windows环境下也可以将其写到run.bat脚本文件中，双击运行即可。

```log
java -jar .\mybatis-generator-core-1.4.0.jar -configfile .\generatorConfig.xml -overwrite
```
