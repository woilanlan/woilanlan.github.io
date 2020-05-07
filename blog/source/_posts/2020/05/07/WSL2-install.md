---
title: WSL2的安装
categories:
  - Windows使用
tags:
  - Windows使用
date: 2020-05-07 17:16:01
---


WSL 2 的安装说明：<https://docs.microsoft.com/zh-cn/windows/wsl/wsl2-install>

## 1、Windows 10 进行版本升级

升级到18917版本或更高版本

打开命令提示符并运行 ver 命令来检查 Windows 版本。

打开“Windows 设置”，选择“更新和安全”，在“Windows 更新”，点击检查更新，更新到新版本。

## 2、加入Windows 预览体验计划

如果没有版本升级的更新，选择“Windows 预览体验计划”，点击开始，登录Windows账号，并选择 "快速" 环或 "慢速" 环，即可收到新版本更新的提示

## 3、启用 "虚拟机平台" 可选组件，并确保已启用 WSL

通过在 PowerShell 中运行以下命令来执行此操作

```log
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

请重新启动计算机以完成两个组件的安装。

## 4、启用 WSL

网址：<https://docs.microsoft.com/zh-cn/windows/wsl/install-win10>

请在 Powershell 提示符下以具有管理员权限的身份运行此命令

```log
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

出现提示时，重启计算机。

## 5、安装所选的 Linux 分发版

打开 Microsoft Store，并选择你偏好的 Linux 分发版。

在分发版的页面中，选择“获取”

## 6、完成分发版的初始化

网址：<https://docs.microsoft.com/zh-cn/windows/wsl/initialize-distro>

下载并安装分发版后，需要对新的分发版完成初始化

### 启动分发版

若要完成新安装的分发版的初始化，请启动新实例。 为此，可以单击 Microsoft Store 应用中的“启动”按钮，或者从“开始”菜单启动分发版

首次运行新安装的分发版时，会打开一个控制台窗口，其中指出需要等待一两分钟时间来完成安装。

### 设置新的 Linux 用户帐户

安装完成后，系统会提示创建新的用户帐户（及其密码）。

此用户帐户用于启动分发版时默认登录的非管理员用户。

打开新的分发版实例时，系统不会提示你输入密码，但如果使用 sudo 提升了进程的权限，则需要输入密码，因此请确保选择一个容易记住的密码！

### 更新和升级分发版的包

大多数分发版随附了一个空的/精简的包目录。 我们强烈建议定期更新包目录，并使用分发版的首选包管理器升级已安装的包。 在 Debian/Ubuntu 上使用 apt：

```bash
sudo apt update && sudo apt upgrade
```

## 7、使用命令行设置要由 WSL 2 支持的发行版

1、查看每个发行版使用的 WSL 版本：

```log
wsl --list --verbose 或 wsl -l -v
```

2、设置发行版

```log
wsl --set-version Ubuntu 2
```

Ubuntu为你的发行版的实际名称

可以随时更改回 WSL 1，方法是运行与上面相同的命令，但将“2”替换为“1”。

3、设置 WSL 2 成为你的默认体系结构

```log
wsl --set-default-version 2
```

使你安装的任何新发行版均初始化为 WSL 2 发行版。

## 问题

1、由于虚拟磁盘系统限制，无法完成请求的操作。虚拟硬盘文件必须是解压缩和未加密的，并且不能是稀疏的。

网址：<https://github.com/microsoft/WSL/issues/4103>

```log
打开个人资料文件夹中的Ubuntu目录

％USERPROFILE％\ AppData \ Local \ Packages \ CanonicalGroupLimited ...

右键单击“ LocalState”，“属性”，“高级”，取消选择“压缩内容”。

当它询问您是要仅应用于此文件夹还是应用于所有子文件夹和文件时，您可以说“仅此文件夹”，因为您要做的只是清除“ compress”标志。

之后，该wsl --set-version命令应该起作用。
```

2、在计算机的 BIOS 内已启用虚拟化

网址：<https://jingyan.baidu.com/article/ab0b56305f2882c15afa7dda.html>

打开任务管理器，选择“性能”标签，点击左侧的“CPU”，查看“虚拟化”状态是否为已启用。

启用

- 开机时按F2、F12、DEL、ESC等键就可以进入到BIOS
- 找到Configuration选项或者Security选项，
- 然后选择Virtualization，或者Intel Virtual Technology
- 将其值设置成：设置为Enabled
- 保存BIOS设置，重启计算机
