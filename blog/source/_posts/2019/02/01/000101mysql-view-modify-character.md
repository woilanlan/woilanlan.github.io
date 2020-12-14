---
title: MySQL查看和修改字符集
date: 2019-02-01 00:01:01
categories:
- mysql
tags:
- mysql
---

## 查看字符集编码

查看MYSQL数据库服务器和数据库字符集

```sql
show variables like '%character%';
```

如下图：

![20200706112049](https://photo.woilanlan.top/blog/img/2020/07/06/20200706112049.png)

## 修改字符集编码

在服务中找到 Mysql 对应的服务

![20200706113513](https://photo.woilanlan.top/blog/img/2020/07/06/20200706113513.png)

双击 MySQL57 查看对应属性

可执行文件的路径：

```log
"D:\tool\mysql\MySQL57\bin\mysqld.exe" --defaults-file="D:\tool\mysql\MySQL57\my.ini" MySQL57
```

关闭服务，修改 my.ini 文件

在 [mysqld] 下面添加 character-set-server=utf8

![20200706114142](https://photo.woilanlan.top/blog/img/2020/07/06/20200706114142.png)

保存文件，重启 Mysql 服务。

## 参考

<https://blog.csdn.net/kai666ling/article/details/79790374>

<https://www.cnblogs.com/xiaowie/p/12020839.html>
