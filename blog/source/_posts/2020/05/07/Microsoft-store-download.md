---
title: 微软商店点下载没反应
categories:
  - Windows使用
tags:
  - Windows使用
date: 2020-05-07 17:05:06
---


## 本人解决方案

注销微软商店登录账号，重置 Microsoft Store 缓存，搜索应用，点击下载，重新登录，一般就会显示下载。

如没有出现下载，请检查以下相关配置是否正常，可重复几次（可能和本地的网络有关系）

## 方案1

- 下载及安装微软官方的应用商店检测工具，完成后重启电脑。
- 网址：<http://aka.ms/diag_apps10>

## 方案2

网址：<https://support.microsoft.com/zh-cn/help/13765/microsoft-store-cant-find-or-install-app>

### 重置 Microsoft Store 缓存（推荐）

按 Windows 徽标键 + R 以打开“运行”对话框，键入“wsreset.exe”，然后选择“确定”。

注意：

将打开一个空白的“命令提示符”窗口，在大约 10 秒钟后，该窗口将关闭并自动打开 Microsoft Store。

### 重置您的应用商店(慎用)

在打开的“管理员：Windows Powershell”窗口中输入以下命令：

```log
get-appxpackage *store* | remove-Appxpackage
```

再次安装：

```log
add-appxpackage -register "C:\Program Files\WindowsApps\*Store*\AppxManifest.xml" -disabledevelopmentmode
```

## 方案3

恢复原来的hosts文件，并在命令行中刷新DNS

## 方案4

网址：<https://www.pconline.com.cn/win10/1113/11135679.html>

1、重新登录Win10商店

打开商店后，点击你的头像；
点击你的账户名称，进入账户页面；
点击你的账户名，然后点击“注销”；
再次点击头像图标，然后点击“登录”

2、检查Windows Update服务是否启动

## 方案5

搜索IE，点击“设置”图标，点击“Internet 选项”，高级，确定勾选了“使用 TLS 1.2”，点击还原高级设置。重启电脑。
