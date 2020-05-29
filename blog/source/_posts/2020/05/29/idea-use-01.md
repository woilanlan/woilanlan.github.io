---
title: IDEA快捷键01
date: 2020-05-29 14:36:47
categories:
- java
tags:
- java
- IDEA
---

[这样配置：让你的 IDEA 好用到飞起来](https://mp.weixin.qq.com/s/3Ij-jPPbF2R-Un0lNKzOOg)

## 常用快捷键

1、快速查找

- 快速搜索类：Ctrl + N
- 快速搜索文件：Ctrl + Shift + N
- 替换当前文件中的内容：Ctrl + R
- 查看某一个方法或者变量在哪里被使用：Alt + F7
- 查看代码提示及内容：Ctrl + Q
- 查看类的定义：Ctrl + B 或者 按下Ctrl再鼠标左键单击
- 列出类中的所有方法: Ctrl + F12
- 查看接口或者抽象类的子类：Ctrl + Alt + B
- 查看类的层级关系：Ctrl + H
- 光标的 上/下一个位置（查看源码）：Ctrl + Alt + ←/→

2、代码编辑

- new对象补全：Alt + Enter
  - new User().var代表新增一个局部变量
  - new User().field代表新增一个全局变量
- 类型强转：ctx.getBean("user1").cast
- 代码复制到新的一行：Ctrl + D
- 删除当前行：Ctrl+Y
- 代码向上或者向下移动：Shift + Alt + ↑/↓
- 在当前行的上面创建新的一行：Ctrl + Alt + Enter
- 在当前行的下面新建一行：Shift + Enter
- 行注释：Ctrl + /
- 块注释：Ctrl + Shift + /
- 代码补全：Ctrl + Alt + 空格
- 查看方法参数：Ctrl + P
- 移除无效import：Ctrl + Alt + O

3、代码重构

- 新建文件：Alt + Insert
- 生成get/set等方法：Alt + Insert
- 变量或者类名重命名: Shift + F6
- 打开模块设置：选中项目，F4
- 切换项目的JDK版本：Ctrl + shift + Alt + /
- 提取全局变量：Ctrl + Alt + F
  - 选中变量右键 --> Refactor --> Extract --> Field
- 代码包裹，选中代码后，可以被 for/if/trycache 等代码块包裹：Ctrl + Alt + T

4、编译运行

## 便捷的功能

1、智能的选取

从某个变量到表达式到方法甚至到类，扩充者选取：Ctrl + W

2、丰富的导航模式

显示最近打开过的文件: Ctrl + E

打开类名搜索框：Ctrl + N 或者连按两下Shift

3、历史记录功能

在当前文件的编辑界面 --> 右键 --> Local History

4、辅助编码

自动在Java Bean中生成 toString()、hashCode()、equals() 以及所有的get/set 方法

Windows是 Alt + Insert，Mac是 Command + N

5、XML的完美支持

引入Spring依赖之后，就会有Spring的XML模板，可以直接用。

new --> XML Configuration File --> Spring Config

6、列编辑模式

按住Alt键下拉同时编辑多行

7、预置模板

显示代码模板提示：Ctrl + J

**main方法的生成**：psvm

System.out.println的快捷输出

```log
"abc".sout => System.out.println("abc");
```

**for循环**:

```log
List<String> list = new ArrayList<String>();

输入: list.for 即可输出

for(String s:list){}
```

**SQL语句**：

ins、upd

在设置中新增：Live Templates

8、对Git的友好支持

IDEA集成了目前大部分的版本工智工具插件

9、智能代码

自动检查代码，发现与预置规范有出入的代码给出提示，自动完成修改

10、html相关操作

在html文件中快速引入js文件，直接拖动js文件到html的对应位置。

输入

```html
div#header+div.page+div#footer.class1.class2.class3
```

按下TAB键

```html
<div id="header"></div>
<div class="page"></div>
<div id="footer" class="class1 class2 class3"></div>
```

[IDEA快捷键以及emmet插件的自动补全](https://blog.csdn.net/Black1499/article/details/81515301)
