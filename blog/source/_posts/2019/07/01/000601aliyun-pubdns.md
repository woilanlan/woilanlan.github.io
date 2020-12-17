---
title: 阿里云公共 DNS
date: 2019-07-01 00:06:01
categories:
- windows使用
tags:
- windows使用
---

## 基本概念

### DNS

DNS是域名系统（Domain Name System）的缩写，是因特网的一项核心服务，它作为可以将域名和IP地址相互映射的一个分布式数据库，能够使人更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。

### 域名

由于因特网的用户数量较多，所以因特网在命名时采用的是层次树状结构的命名方法。任何一个连接在因特网上的主机或路由器，都有一个唯一的层次结构的名字，即域名（domain name）。

## 阿里云公共DNS

[官网](https://www.alidns.com/)

[帮助文档](https://help.aliyun.com/product/162402.html?spm=a2c4g.11174283.6.98.1dd0923d9IFbNK)

是阿里云面向所有互联网用户的全球公共递归域名解析服务。和仅使用本地LocalDNS的传统解析服务相比，使用阿里云公共解析服务，能够帮助您的互联网访问更加“快速”、“稳定”、“安全”。

```log
IPv4地址：

223.5.5.5
223.6.6.6

IPv6地址：

2400:3200::1
2400:3200:baba::1
```

## 接入方式

### 直接更改公共DNS的地址

普通用户通过将DNS地址改成阿里云公共的DNS地址，就能实现快速接入。

参考：<https://www.alidns.com/setup>

Windows系统设置

- 打开 控制面板 ---> 网络和Internet ---> 网络和共享中心
- 点击左侧 更改适配器设置
- 选中正在联网的网络连接，右键选择 属性
- 选中 Internet 协议版本 4 (TCP/IPv4) ，点击 属性
- 选择使用指定的DNS，在DNS服务器地址中输入 223.5.5.5 和 223.6.6.6
- 点击 确定 ，设置完成。

## 域名检测工具

[帮助文档](https://help.aliyun.com/document_detail/155515.html?spm=a2c4g.11174283.6.722.1a58571f3l3mSi)

[工具网址](https://zijian.aliyun.com/?spm=a2c4g.11186623.2.16.3dd43deefoTZ4n#/domainDetect)
