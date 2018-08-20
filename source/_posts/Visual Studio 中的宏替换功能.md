---
title: Visual Studio 中的宏替换功能
date: 2018-8-17 01:56:51
tags:
- VS
- CODE
categories:
- Code Skill
---


在VS中编辑属表的时候可以看到很多路径中带有“$”这个符号，例如：

```
$(projectpath)a.lib
```
#### 我们大概知道它代表一个路径，但是我们怎么知道具体路径是什么呢？

> 其实这是vs内部的宏替换功能
比如工程目录 ,vs会默认设置一个参数 projectpath,这里假设其值为 "C:\myproj\"。
而你想使用这个目录下的一个库文件的话,你就这么写$(projectpath)a.lib，那么就相当于 C:\myproj\a.lib 。

#### 如果想查看宏，随意打开一个属性表：
> 以VC++目录为例，右下角可以看到一个按钮“宏”，点开来可以看到这些宏对应的路径
比如解决方案目录在c盘aaa文件夹下，那么$(SolutionDir)代表c:\aaa\，$(SolutionDir)bbb就可以很方便地表达c:\aaa\bbb这个文件夹
(这些宏是没法修改的 )


![image](https://note.youdao.com/yws/public/resource/c6555434be43bcdee44e49ea613d8a7c/xmlnote/178FE714F032425C8238814ADCBA61F0/1178)

如上图所示，点击宏之后就可以看到各自对应的绝对路径是什么啦~