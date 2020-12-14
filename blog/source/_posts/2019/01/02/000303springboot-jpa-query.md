---
title: Spring Data Jpa 自定义查询和更新
date: 2019-01-02 00:03:03
categories:
- springboot
tags:
- springboot
---


## 自定义查询SQL

1、创建接口

BookDao.java

```java
package top.woilanlan.jpa.dao;

public interface BookDao extends JpaRepository<Book, Integer> {

    @Query(value = "select * from t_book where id=(select max(id) from t_book)",
           nativeQuery = true)
    Book getMaxIdBook();
}
```

2、测试

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class JpaApplicationTests {

    @Autowired
    BookDao bookDao;

    @Test
    public void find6() {
        Book book = bookDao.getMaxIdBook();
        System.out.println(book);
    }

}
```

## 自定义更新 SQL

1、创建接口

BookDao.java

```java
package top.woilanlan.jpa.dao;

public interface BookDao extends JpaRepository<Book, Integer> {

    @Query(value = "insert into t_book(name,author) values(?1,?2)",
           nativeQuery = true)
    @Modifying
    @Transactional
    Integer addBook(String name, String author);

    @Query(value = "insert into t_book(name,author) values(:name,:author)",
           nativeQuery = true)
    @Modifying
    @Transactional
    Integer addBook2(@Param("name") String name, @Param("author") String author);
}
```

2、测试

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class JpaApplicationTests {

    @Autowired
    BookDao bookDao;

    @Test
    public void test1() {
        Integer r1 = bookDao.addBook("朝花夕拾", "鲁迅");
        System.out.println(r1);
        Integer r2 = bookDao.addBook2("呐喊", "鲁迅");
        System.out.println(r2);
    }
}
```
