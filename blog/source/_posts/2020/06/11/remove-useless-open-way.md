---
title: 删除无用的打开方式
date: 2020-06-11 11:30:42
categories:
  - Windows使用
tags:
  - Windows使用
---

问题描述：

选中PDF文件 --> 右键 --> 打开方式

在打开方式列表里，出现了一个已经卸载的软件，但是无法删除。

解决方案：

快捷键 Win + R 打开 运行 命令窗口，输入 regedit

找到如下注册表路径：

```log
# 系统版本：Windows 10
计算机\HKEY_CLASSES_ROOT\.pdf\OpenWithProgids
```

右侧的区域中，选中找到你想要删除的项，右键删除即可。

参考：

<https://jingyan.baidu.com/article/ca41422fc54e481eae99edbd.html>
