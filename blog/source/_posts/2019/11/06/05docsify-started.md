---
title: 05docsify快速入门
date: 2019-11-06 12:00:05
categories:
- 个人博客
tags:
- 个人博客
- docsify
---

## 快速入门

官方文档：<https://docsify.js.org/>

建议全局安装 ```docsify-cli``` ，这有助于在本地初始化和预览网站

```sh
npm i docsify-cli -g
```

如果要在 ```./docs``` 子目录中编写文档，则可以使用 ```init``` 命令

```sh
docsify init ./docs
```

目录 ```./docs``` 的文件如下

- ```index.html``` 作为入口文件
- ```README.md``` 作为主页
- ```.nojekyll``` 防止GitHub Pages忽略以下划线开头的文件

运行查看

使用 ```docsify serve``` 运行本地服务器。在浏览器中预览站点：<http://localhost:3000>

```sh
docsify serve docs
```

## 创建多个页面

如果需要更多页面，只需在目录中创建更多markdown文件即可。

例如：

创建一个名为 ```guide.md``` 的文件，通过 ```/#/guide``` 即可访问该文件

目录结构

```log
└── docs
    ├── README.md
    ├── guide.md
    └── zh-cn
        ├── README.md
        └── guide.md
```

匹配路线

```log
docs/README.md        => http://domain.com
docs/guide.md         => http://domain.com/#/guide
docs/zh-cn/README.md  => http://domain.com/#/zh-cn/
docs/zh-cn/guide.md   => http://domain.com/#/zh-cn/guide
```

## 侧边栏

在 ```index.html``` 文件中设置 ```loadSidebar: true``` 属性

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

创建文件 ```_sidebar.md```

```log
<!-- docs/_sidebar.md -->

* [Home](/)
* [Guide](guide.md)
```

### 嵌套侧边栏

_sidebar.md从每个级别目录加载。如果当前目录没有_sidebar.md，它将退回到上级目录。

```log
<!-- docs/zh-cn/_sidebar.md -->

* [首页](zh-cn/)
* [指南](zh-cn/guide.md "The greatest guide in the world")
```

### 设置页面标题

页面的 ```title``` 标签是根据所选的侧边栏项目名称生成的。为了获得更好的SEO，您可以通过在文件名后指定字符串来自定义标题。

### 目录

创建完成后```_sidebar.md```，边栏内容将根据markdown文件中的标题自动生成。

可以通过设置 ```subMaxLevel: 2``` 来配置生成目录的层级。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
    subMaxLevel: 2
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

## 导航栏

设置 ```loadNavbar: true``` 

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadNavbar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

创建 ```_navbar.md``` 来自定义导航,通过缩进创建父子关系

```log
<!-- _navbar.md -->

* [Translations](/)
  * [English](/)
  * [中文](/zh-cn/)
```
