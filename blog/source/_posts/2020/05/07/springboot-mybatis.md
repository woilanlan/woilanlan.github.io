---
title: 整合MyBatis
categories:
- [JavaWeb,springboot]
tags:
- springboot
date: 2020-05-07 20:00:00
---


1、创建 springboot 项目，添加依赖

pom.xml

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
    <version>5.1.27</version>
</dependency>
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.0</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.1.10</version>
</dependency>
```

2、增加配置

application.properties

```properties
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
spring.datasource.username=root
spring.datasource.password=123
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/test

logging.level.top.woilanlan.mybatis.mapper=debug
```

3、创建类

User.java

```java
package top.woilanlan.mybatis.bean;

@Data
public class User {
    private Integer id;
    private String username;
    private String address;
}
```

4、创建 Mapper 接口，配置包扫描

UserMapper.java

```java
package top.woilanlan.mybatis.mapper;

//使用注解 @Mapper
public interface UserMapper {
    List<User> getAllUser();
}
```

推荐：

```java
package top.woilanlan.mybatis;

@SpringBootApplication
@MapperScan(basePackages = "top.woilanlan.mybatis.mapper")
public class MybatisApplication {

    public static void main(String[] args) {
        SpringApplication.run(MybatisApplication.class, args);
    }
}
```

5、创建对应 xml 文件

UserMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="top.woilanlan.mybatis.mapper.UserMapper">
    <select id="getAllUser" resultType="top.woilanlan.mybatis.bean.User">
        select * from user ;
    </select>
</mapper>
```

注意：在 Maven 项目中，建议将 xml 和 properties 放到 resources 目录下，如果放在包下面将会被忽略。

方式1：在 resources 建立对应目录：top/woilanlan/mybatis/mapper ，将 xml 文件放到该目录下。

方式2：在  pom.xml 增加配置

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
            </includes>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
        </resource>
    </resources>
    ...
</build>
```

方式3：放在 resources 下自定义 mapper 目录，在 application.properties 增加配置

```properties
mybatis.mapper-locations=classpath:/mapper/*.xml
```

6、测试

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MybatisApplicationTests {

    @Autowired
    UserMapper userMapper;

    @Test
    public void contextLoads() {
        List<User> allUser = userMapper.getAllUser();
        System.out.println(allUser);
    }
}
```
