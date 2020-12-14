---
title: 整合JdbcTemplate
date: 2019-01-02 00:02:01
categories:
- springboot
tags:
- springboot
---


1、创建 springboot 项目，添加依赖

pom.xml

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
    <version>5.1.27</version>
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
```

3、创建类

User.java

```java
package top.woilanlan.jdbctemplate.bean;

@Data
public class User {
    private Integer id;
    private String username;
    private String address;
}
```

4、创建类

UserService.java

```java
@Service
public class UserService {
    @Autowired
    JdbcTemplate jdbcTemplate;

    public Integer addUser(User user) {
        String sql = "insert into user (username,address) values (?,?)";
        return jdbcTemplate.update(sql,
                                   user.getUsername(), user.getAddress());
    }

    public Integer updateUsernameById(User user) {
        String sql = "update user set username = ? where id = ? ";
        return jdbcTemplate.update(sql,
                                   user.getUsername(), user.getId());
    }

    public Integer deleteUserById(Integer id) {
        return jdbcTemplate.update("delete from user where id=?", id);
    }

    public List<User> getAllUsers() {
        return jdbcTemplate.query("select * from user", new RowMapper<User>() {
            @Override
            public User mapRow(ResultSet resultSet, int i) throws SQLException {
                User user = new User();
                int id = resultSet.getInt("id");
                String username = resultSet.getString("username");
                String address = resultSet.getString("address");
                user.setUsername(username);
                user.setId(id);
                user.setAddress(address);
                return user;
            }
        });
    }

    public List<User> getAllUsers2() {
        return jdbcTemplate.query("select * from user",
                                  new BeanPropertyRowMapper<>(User.class));
    }
}
```
