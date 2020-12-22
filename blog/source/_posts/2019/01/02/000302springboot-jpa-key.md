---
title: Spring Data Jpa 使用关键字定义查询
date: 2019-01-02 00:03:02
categories:
- springboot
tags:
- springboot
---


1、创建接口

BookDao.java

```java
package top.woilanlan.jpa.dao;

public interface BookDao extends JpaRepository<Book, Integer> {

    //根据id查询
    Book findBookById(Integer id);

    //查询id大于 ?1 的所有记录
    List<Book> findBookByIdGreaterThan(Integer id);

    //查询id小于 ?1 或者名称中包含 ?2 的所有记录
    List<Book> findBookByIdLessThanOrNameContaining(Integer id, String name);
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
    public void find4() {
        Book book = bookDao.findBookById(3);
        System.out.println(book);
    }

    @Test
    public void find5() {
        List<Book> list = bookDao.findBookByIdGreaterThan(3);
        System.out.println(list);
        List<Book> list1 = bookDao.findBookByIdLessThanOrNameContaining(3, "故事");
        System.out.println(list1);
    }
}
```

3、查询关键字

![20200926164408138](https://photo.woilanlan.top/blog/img/2020/05/07/20200926164408138.png)

![20200926171052390](https://photo.woilanlan.top/blog/img/2020/05/07/20200926171052390.png)

![20200926171627901](https://photo.woilanlan.top/blog/img/2020/05/07/20200926171627901.png)
