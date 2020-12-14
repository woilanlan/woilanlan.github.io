---
title: springboot
date: 2019-01-02 00:01:01
categories:
- springboot
tags:
- springboot
---

## Spring Boot

官方文档：

<https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/reference/htmlsingle/>

Spring Boot可以轻松创建可以运行的独立的，生产级的基于Spring的应用程序。

可以使用Spring Boot创建可以使用java -jar或更传统的war部署启动的Java应用程序

## 一、开发您的第一个Spring Boot应用程序

在开始之前，打开终端并运行以下命令以确保安装了有效的Java和Maven版本：

```log
$ java -version
java version "1.8.0_102"
Java(TM) SE Runtime Environment (build 1.8.0_102-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.102-b14, mixed mode)
```

```log
$ mvn -v
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-17T14:33:14-04:00)
Maven home: /usr/local/Cellar/maven/3.3.9/libexec
Java version: 1.8.0_102, vendor: Oracle Corporation
```

### 1、构建一个maven项目：创建POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.3.RELEASE</version>
    </parent>

    <!-- Additional lines to be added here... -->

</project>
```

可以通过运行 mvn package 来测试它

### 2、添加类路径依赖关系

打印项目依赖项的树,可以看到 spring-boot-starter-parent 本身不提供依赖关系

```log
$ mvn dependency:tree

[INFO] com.example:myproject:jar:0.0.1-SNAPSHOT
```

要开发Web应用程序，我们编辑pom.xml添加了spring-boot-starter-web依赖项

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

如果再次运行mvn dependency:tree，您会发现现在有许多其他依赖项。

### 3、写代码

默认情况下，Maven编译源代码src/main/java，因此您需要创建该文件夹结构，然后添加一个名为src/main/java/Example.java

包含以下代码的文件：

```java
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.web.bind.annotation.*;

@RestController
@EnableAutoConfiguration
public class Example {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        SpringApplication.run(Example.class, args);
    }

}
```

注解说明：

@RestController：

这被称为构造型注释。它为阅读代码的人提供了提示，而为Spring提供了特定角色的提示。在这种情况下，我们的类是一个Web @Controller，因此Spring在处理传入的Web请求时会考虑它。

@RequestMapping：

注释提供“路由”的信息。它告诉Spring，任何带“/”路径的HTTP请求都应该映射到该home方法。该@RestController注解告诉Spring使得到的字符串直接返回给调用者。

@EnableAutoConfiguration：

这个注释告诉Spring Boot根据你添加的jar依赖关系“猜测”你想要如何配置Spring。自从spring-boot-starter-web添加了Tomcat和Spring MVC 以来，自动配置假定您正在开发Web应用程序并相应地设置Spring。

mian()方法：

遵循应用程序入口点的Java约定的标准方法。我们的main方法SpringApplication通过调用委托给Spring Boot的类run。 SpringApplication引导我们的应用程序，启动Spring，然后启动自动配置的Tomcat Web服务器。我们需要Example.class作为参数传递给run方法，以告诉SpringApplication哪个是主要的Spring组件。该args数组也被传递以公开任何命令行参数。

### 4、运行示例

在当前maven项目下运行

```log
$ mvn spring-boot:run

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.1.3.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.222 seconds (JVM running for 6.514)
```

打开Web浏览器访问地址：<http://localhost:8080>

您应该看到以下输出：

```log
Hello World!
```

正常退出程序，请按：Ctrl + C

### 5、创建一个可执行的Jar

要创建可执行jar，我们需要添加spring-boot-maven-plugin到我们的pom.xml

在dependencies部分下方插入以下内容：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

保存pom.xml并从命令行运行mvn package

```log
$ mvn package

[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] .... ..
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.1.3.RELEASE:repackage (default) @ myproject ---
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

如果你查看target目录，你应该看到myproject-0.0.1-SNAPSHOT.jar。该文件大小应为10 MB左右。如果你想查看内部，你可以使用jar tvf，如下：

```log
jar tvf target/myproject-0.0.1-SNAPSHOT.jar
```

您还应该看到目录中命名myproject-0.0.1-SNAPSHOT.jar.original的文件小得多target。这是Maven在Spring Boot重新打包之前创建的原始jar文件。

要运行该应用程序，请使用以下java -jar命令：

```log
java -jar target/myproject-0.0.1-SNAPSHOT.jar
```

正常退出程序，请按：Ctrl + C
