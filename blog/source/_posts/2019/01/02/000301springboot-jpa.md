---
title: 整合Spring Data Jpa
date: 2019-01-02 00:03:01
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
    <artifactId>spring-boot-starter-data-jpa</artifactId>
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

spring.jpa.show-sql=true
spring.jpa.database=mysql
spring.jpa.database-platform=mysql
# 每次启动检查表和实体类是否一致，不一致则更新表。如果表不存在则创建表
spring.jpa.hibernate.ddl-auto=update
# 数据库方言
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
```

3、创建实体类

Book.java

```java
package top.woilanlan.jpa.bean;

/**
标识实体类和对应表名
*/
@Entity(name = "t_book")
@Data
public class Book {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;	//指定主键，设置自增长

    @Column(name = "name")
    private String name;	//指定列的相关属性

    private String author;

}
```

4、创建接口

BookDao.java

```java
package top.woilanlan.jpa.dao;

public interface BookDao extends JpaRepository<Book, Integer> {

}
```

继承关系

![20200926175141367](https://woilanlan.top/photo-gallery/blog/img/2020/05/07/20200926175141367.png)

5、测试

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class JpaApplicationTests {

    @Autowired
    BookDao bookDao;

    @Test
    public void contextLoads() {
        Book book = new Book();
        book.setName("三国演义");
        book.setAuthor("罗贯中");
        bookDao.save(book);
    }

    @Test
    public void update() {
        Book book = new Book();
        book.setAuthor("luoguanzhong");
        book.setName("sanguoyanyi");
        book.setId(1);
        //数据存在就更新，不存在就新增
        bookDao.saveAndFlush(book);
    }

    @Test
    public void delete() {
        bookDao.deleteById(1);
    }

    @Test
    public void find1() {
        Optional<Book> byId = bookDao.findById(2);
        System.out.println(byId.get());

        List<Book> all = bookDao.findAll();
        System.out.println(all);
    }

    @Test
    public void find2() {
        //排序
        List<Book> list = bookDao.findAll(
            new Sort(Sort.Direction.DESC, "id"));
        System.out.println(list);
    }

    @Test
    public void find3() {
        //分页
        Pageable pageable = PageRequest.of(0, 2);
        Page<Book> page = bookDao.findAll(pageable);
        System.out.println("总记录数："+page.getTotalElements());
        System.out.println("当前页记录数："+page.getNumberOfElements());
        System.out.println("每页记录数："+page.getSize());
        System.out.println("获取总页数："+page.getTotalPages());
        System.out.println("查询结果："+page.getContent());
        System.out.println("当前页（从0开始计）"+page.getNumber());
        System.out.println("是否为首页："+page.isFirst());
        System.out.println("是否为尾页："+page.isLast());
    }
}
```
