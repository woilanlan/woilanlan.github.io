---
title: python环境配置
categories:
- python入门
tags:
- python
---

## 1、下载

进入 python 官网，点击 Downloads 下载

<https://www.python.org/downloads/>

<!-- more -->

## 2、安装

2.1 双击python的安装程序

![01.png](https://woilanlan.top/photo-gallery/blog/img/2019/11/28/01.png)

2.2 弹出安装界面

![02.png](https://woilanlan.top/photo-gallery/blog/img/2019/11/28/02.png)

![03.png](https://woilanlan.top/photo-gallery/blog/img/2019/11/28/03.png)

![04.png](https://woilanlan.top/photo-gallery/blog/img/2019/11/28/04.png)

![05.png](https://woilanlan.top/photo-gallery/blog/img/2019/11/28/05.png)

2.3 验证安装成功

打开 cmd 并运行以下命令：

```py
py -3 --version
```

## 3、创建虚拟环境

默认情况下，您安装的任何Python解释器都在其自己的全局环境中运行，该环境并不特定于任何一个项目。您安装或卸载的任何程序包都会影响全局环境以及在该上下文中运行的所有程序。

虚拟环境是项目中的子文件夹，其中包含特定解释器的副本。

激活虚拟环境时，您安装的所有软件包仅安装在该环境的子文件夹中。然后，当您在该环境中运行Python程序时，就会知道该程序仅针对那些特定的程序包运行。

要创建虚拟环境，请使用以下命令，其中“.venv”是环境文件夹的名称

```py
# macOS/Linux
# You may need to run sudo apt-get install python3-venv first
python3 -m venv .venv

# Windows
# You can also use py -3 -m venv .venv
python -m venv .venv
```

## 4、VS Code中的Python入门

### 4.1 安装 python 插件

![06.png](https://woilanlan.top/photo-gallery/blog/img/2019/11/28/06.png)

### 4.2 创建项目文件夹

创建一个名为“hello”的空文件夹，导航至该文件夹，在该文件夹中打开VS Code

```log
mkdir hello
cd hello
code .
```

### 4.3 选择一个Python解释器

默认情况下，Python扩展会查找并使用它在系统路径中找到的第一个Python解释器,如果找不到解释器，则会发出警告。

打开命令面板（Ctrl + Shift + P），使用 ```Python: Select Interpreter``` 选择特定python环境

### 4.4 编写 python 程序

新建文件：hello.py

```py
msg = "Hello World"
print(msg)
```

### 4.5 运行

点击编辑器右上角的“在终端中运行Python文件”按钮
