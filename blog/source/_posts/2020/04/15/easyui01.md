---
title: 01EasyUI入门
date: 2020-04-15 15:22:15
categories:
- [前端知识,EasyUI]
tags:
- EasyUI
---

## EasyUI概述

[Jquery EasyUI中文网](http://www.jeasyui.net/)

推荐：

[EasyUI的下载与使用](https://blog.csdn.net/luoluozlb/article/details/53648705)

[Jquery EasyUI学习使用总结](https://www.cnblogs.com/xdp-gacl/category/571424.html)

[EasyUI 使用——基本概念](http://www.cnblogs.com/zjfjava/p/6836912.html)

## 一、解压包中各个目录的说明

1、demo

demo目录是EasyUI各个组件的演示例子。

2、demo-mobile

这个目录是EasyUI各个组件在移动端开发的演示例子。

3、locale

这个目录是EasyUI对于各个国家的语言包。

- 简体中文的语言包是：easyui-lang-zh_CN.js，
- 繁体中文的语言包是：easyui-lang-zh_TW.js，
- 英语的语言包（默认）：easyui-lang-en.js

4、plugins

此目录的EasyUI使用的插件js代码

5、src

此目录是部分EasyUI插件的js源码。

6、themes

此目录是EasyUI主题文件。

7、根目录

根目录下的文件有：

| 文件                        | 说明                                                                               |
| --------------------------- | ---------------------------------------------------------------------------------- |
| changlog.txt                | EasyUI版本更新说明。                                                               |
| easyloader.js               | EasyUI的模块加载器，用来自动帮助自动加载EasyUI文件。                               |
| jquery.easyui.min.js        | 全部easyui核心和插件的集合文件，一般可以直接加载这个文件而不用一个个加载那些插件。 |
| jquery.easyui.mobile.min.js | 同上，不同的是适用于移动端的。                                                     |
| jquery.min.js               | jQuery库文件，因为EasyUI是基于jQuery的，所以也得加载jQuery文件。                   |
| license_freeware.txt        | 免费使用EasyUI的声明（只能用于非盈利目的）。                                       |
| readme.txt                  | 商业用途许可说明。                                                                 |

## 二、加载EasyUI

通常情况下，我们只需要加载几个文件就够了：

```html
<link rel="stylesheet" type="text/css" href="easyui/themes/default/easyui.css">
<link rel="stylesheet" type="text/css" href="easyui/themes/icon.css">
<script type="text/javascript" src="easyui/jquery.min.js"></script>
<script type="text/javascript" src="easyui/jquery.easyui.min.js"></script>
```

第一个和第二个是主题的css样式文件，上面的代码是使用默认主题，我们也很容易切换到其他主题，只要修改defult即可。

第三个是jQuery库文件，一般使用EasyUI解压包里面的jQuery文件即可。

第四个是EasyUI核心和组件的集合js文件，加载这个文件会加载所有的EasyUI组件，就不需要一个个导入组件的js文件了。

我们也可以使用EasyUI的EasyLoader插件，这个插件可以帮助我们自定义加载EasyUI模块。

## 三、使用EasyUI的组件的方法

一般有两种方式来使用EasyUI组件。

1、通过在html元素直接设置class为EasyUI组件预定义的名称即可，EasyUI就会自动在页面加载时为元素渲染样式。

例子：我们来创建一个面板（panel）：

```html
<div class="easyui-panel" style="width:500px;height:200px;padding:10px"
    title="我的面板" data-options="iconCls:'icon-ok',collapsible:true">
    创建的第一个面板
</div>
```

2、通过js代码来使用EasyUI组件。使用方法：

```js
$('selector').plugin();
```

即先通过jQuery选定要渲染的元素，然后调用相应的组件即可，这里的plugin是组件的名字。

例子：用js使用EasyUI的面板组件：

```html
<div id="my-panel" style="padding:10px">
    创建的第一个面板
</div>
```

js代码：

```js
$(function(){
    $("#my-panel").panel({
        width:500,
        height:200,
        title:'我的面板',
        iconCls:'icon-ok',
        collapsible:true
    });
});
```

### 补充

1、collapsible

boolean 定义是否显示折叠按钮

2、modal: true

窗体分为模式的和非模式的。以模式方式打开一个窗口,你只能在将其关闭以后才能操作另外的窗口，但非模式窗口显示时,你可以同时操作这两个窗口。

3、icon.css

只有引入这个样式文件，才可以显示对应的图标。
