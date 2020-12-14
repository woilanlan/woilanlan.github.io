---
title: IDEA常用配置
date: 2019-01-01 00:02:02
categories:
- java
tags:
- java
- idea
---

## 常见问题

1、java项目怎么引入自己的jar包

- 新建lib目录，复制对应的jar包
- 选中所有的jar，右键单击，add as Library

2、Maven项目的文件夹设置（目录无法新建java文件和包）

原因：maven中央仓库访问慢，项目生成时没有自动配置对应maven文件夹，需要手动进行设置。

选中项目，F4，打开模块设置，增加项目上下文，一般为工程的路径。

然后选中对应的文件夹，右键设置为源代码文件夹或资源文件夹

3、Maven插件打包

点击Maven模块，打开当前项目Lifecycle的，点击Toggle 'Skip Tests' Mode图标，双击package

在项目的target目录下就会生成对应的jar包

4、使用终端,执行java程序

点击Terminal模块，进入终端

```log
java -jar commandlinerunner-0.0.1-SNAPSHOT.jar longlong woilanlan.github.io
```

5、更改项目Properties文件的编码为UTF-8

File >> Settings >> Editor >> File Encodings

修改 Project Encoding , Properties Files 的编码格式为 UTF-8，勾选自动转为 ASCII 码

5、隐藏IDEA的项目配置文件

Editor >> File Types >> ignore files and folders >> ;.idea;*.iml;

6、编辑文件模板

选中文件夹右键 >> New >> Edit File Templates >> 打开 File and Code Templates 窗口

点击加号 >> 输入Name 和 Extension >> 输入模板内容 >> 选中 Enable Live Templates >> 点击 OK

7、代码重复提示

navigate to duplicate >> disable inspection

8、配置自动生成 serialVersionUID

File >> Settings >> Editor >> Inspections，勾选 Serializable class without 'serialVersionUID'

## 创建maven web项目

1、Maven项目，增加webapp目录

选中项目，F4，打开模块设置，选中项目名称，右键Add Web,添加Web Resource Directory文件夹

Web Resource Directories设置webapp目录：D:\springmvc\springmvc01\src\main\webapp

Web Module Deployment Descriptor设置web.xml文件：D:\springmvc\springmvc01\src\main\webapp\WEB-INF\web.xml

2、打开Artifacts设置

点击添加，Web Application:Exploded,From Modules,选中项目名称，完成添加

3、配置Tomcat

Run/Debug Configurations,点击添加，Tomcat Server,Local

打开Server设置，在Application server,点击configure,在Tomcat Home项，选择Tomcat的安装位置

打开Deployment设置，点击添加，添加我们的项目，在Application context项设置项目部署的名称

4、运行提示，找不到DispatcherServlet类

打开Artifacts设置，在右侧Output Layout右击项目名，选择Put into Output Root

​执行后，在WEB-INF在增加了lib目录，里面是项目引用的jar包

5、SpringMVC中配置了静态资源目录，但是找不到webapp目录下的图片文件。

检查输出目录:out\artifacts\项目名称\static\ 发现唯独缺少了图片的目录。

打开Artifacts设置，在右侧Output Layout里的```<output root>```上面点击加号，选择Directory Content,添加img的目录。

或者

点开Tomcat的配置，点击右侧的加号，选择External Source…选择你存图片的路径，然后在Application context中输入访问你静态图片的路径:/img
在浏览器里直接通过 localhost:8080/img/… 就可以访问你的图片了

[IDEA中创建maven web项目](https://www.cnblogs.com/hanszhao/p/9865098.html)

[IDEA使用Maven搭建web项目启动报找不到类](https://blog.csdn.net/zhang8907xiaoyue/article/details/82942822)

[idea用tomcat发布javaWeb项目中的存在的图片存储路径问题解决](https://blog.csdn.net/jacksonzhou88/article/details/62508188)
