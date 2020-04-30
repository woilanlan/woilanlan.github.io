---
title: 02hexo
date: 2019-11-06 12:03:02
categories:
- 个人博客
tags:
- 个人博客
- hexo
---

## 指南

[Hexo官网](https://hexo.io/zh-cn/)

[GitHub页面入门](https://guides.github.com/features/pages/)

[最全Hexo博客搭建](https://www.simon96.online/2018/10/12/hexo-tutorial/)

[GitHub+Hexo（NexT主题）搭建博客](https://www.jianshu.com/p/7b5702d3f072)

## 一、全局安装和卸载

```sh
npm install hexo-cli -g

npm uninstall hexo-cli -g

# 查看版本，确认是否安装成功
hexo -version
```

## 二、创建和运行项目

在项目所在目录，打开Git Bash

```sh
# 初始化项目
hexo init blog

cd blog

# 安装依赖
npm install

# 生成静态页面（markdown文件转化为html文件）
hexo generate

# 网站预览（默认的主题风格landscape）
hexo server
```

## 三、配置SSH key

提交代码肯定要拥有你的github权限才可以，直接使用用户名和密码太不安全了，所以我们使用ssh key来解决本地和服务器的连接问题。

1、检查电脑是否已经有SSH KEYS

```sh
ls -al ~/.ssh
```

如果列出的文件有public和private钥匙对（例如id_ras.pub和id_rsa），证明已存在SSH keys。如果提示：No such file or directory 说明你是第一次使用git。

2、如果没有SSH KEY，则生成新的SSH KEY

```sh
ssh-keygen -t rsa -C "your_email@example.com"
```

然后连续3次回车，在```C:\Users\longlong\.ssh```目录下，找到.ssh\id_rsa.pub文件，记事本打开并复制里面的内容

3、打开github对应的仓库，添加SSH KEY

在Settings里选择Deploy keys,添加一个Deploy key,将复制的内容粘贴到key那里，title随便填，保存。

4、测试是否成功

```sh
ssh -T git@github.com
```

github设置添加SSH：<https://www.cnblogs.com/chuyanfenfei/p/8035067.html>

## 四、发布到Github

1、在站点目录下修改配置文件```_config.yml```

```yml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  #对应仓库的SSH地址（可以在GitHub对应的仓库中复制）
  repo: git@github.com:<Github账号名称>/<Github账号名称>.github.io.git
  branch: master
```

2、安装hexo-deployer-git插件

```sh
npm install hexo-deployer-git --save
```

3、推送到Github仓库

```sh
hexo g
hexo d
```

## 常用hexo命令

```sh
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo new draft "title" #新建草稿
hexo publish "title" #发布草稿
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo server --draft #预览草稿
hexo deploy #部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
```

缩写

```sh
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```

组合

```sh
hexo s -g #生成并本地预览
hexo d -g #生成并上传
```

## 升级

1、全局的 hexo-cli 更新：卸载重装

2、更新项目的 package.json

全局安装 npm-check

```sh
> npm install -g npm-check //全局安装。项目下安装可自行选择
> npm install npm-check    //项目下安装，项目根目录执行
```

进入项目所在目录,查看包更新信息

```sh
npm-check
```

更新包，分类别展示，使用空格选择包，然后enter开始更新。自动更新package.json内的相关包信息

```sh
> npm-check -u
```

npm-check指令列表

```sh
-u, --update       显示一个交互式UI，用于选择要更新的模块，并自动更新"package.json"内包版本号信息
-g, --global       检查全局下的包
-s, --skip-unused  忽略对未使用包的更新检查
-p, --production   忽略对"devDependencies"下的包的检查
-d, --dev-only     忽略对"dependencies"下的包的检查
-i, --ignore       忽略对指定包的检查.
-E, --save-exact   将确切的包版本存至"package.json"(注意，此命令将存储'x.y.z'而不是'^x.y.z')
```

## 问题

1、hexo不是内部或外部命令，也不是可运行的程序

原因：在hexo模块的bin文件夹下，没有放置对应的cmd命令脚本，所以要将对应的cmd命令脚本添加到系统变量中

参考：<https://blog.csdn.net/qq_27093465/article/details/72954725>

2、部署到GitHub时，执行命令```hexo d```没反应

在站点目录下修改配置文件```_config.yml```，冒号后面少了空格

3、如何在文章中插入图片

```log
# 开启资源文件夹
![](01.png)

{% asset_img 01.png 图片1 %}

# 使用标签插件，引用资源，图片放在source/img文件夹
![](/img/01.png)

{% img /img/01.png 100 100 "图片1" %}
```

## 拓展

[使用hexo+github搭建免费个人博客详细教程](http://blog.haoji.me/build-blog-website-by-hexo-github.html?from=xa)

[从jekyll到hexo](https://blog.csdn.net/u011475210/article/details/79023429)

[如何优雅地发布Hexo博客](https://www.jianshu.com/p/68e727dda16d)
