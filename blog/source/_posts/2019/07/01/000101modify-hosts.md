---
title: 修改hosts文件
date: 2019-07-01 00:01:01
categories:
- windows使用
tags:
- windows使用
---


## 1、完美解决Github访问缓慢问题

国内访问 GitHub 为什么很慢？

GitHub 的 CDN 域名遭到 DNS 污染，导致无法连接使用 GitHub 的加速分发服务器，才使得国内访问速度很慢。

如何解决 DNS 污染？

通过修改 Hosts 文件，将域名解析直接指向 IP 地址来绕过 DNS 的解析，以此解决污染问题。

解决步骤

1、访问 <https://www.ipaddress.com/> 获取 github 最新的 ip 地址

2、修改 host 文件

文件路径：C:\Windows\System32\drivers\etc\host

```log
192.30.253.112    github.com
199.232.5.194   github.global.ssl.fastly.net
99.84.240.40    d3c33hcgiwev3.cloudfront.net
```

3、更新dns缓存

```log
ipconfig /flushdns
```

## hosts 原始文件

```log
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
# 127.0.0.1       localhost
# ::1             localhost
```
