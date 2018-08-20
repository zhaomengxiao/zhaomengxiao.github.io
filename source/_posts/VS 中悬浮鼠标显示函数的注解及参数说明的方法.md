---
title: VS 中悬浮鼠标显示函数的注解及参数说明的方法
date: 2018-8-17 01:56:51
tags:
- VS
- CODE
categories:
- Code Skill
---


> 之前自己开发了一段时间的ASUS Xtion2，觉得自己的代码拼凑能力又提升了不少。最近老师又有一个项目想做，skeleton的获取Kinect真的方便准确的多了，又拿出来研究官方的范例，没想到发现了一个之前没注意的细节，我觉得如果加入自己之后的代码也会让自己的代码易读性提升很多，那就是本文想要介绍的：Visual Studio（2017） 中悬浮鼠标显示函数的注解及参数说明的方法。

### Example:

```
/// <summary>
/// Handles window messages, passes most to the class instance to handle
/// </summary>
/// <param name="hWnd">window message is for</param>
/// <param name="uMsg">message</param>
/// <param name="wParam">message data</param>
/// <param name="lParam">additional message data</param>
/// <returns>result of message processing</returns>
static LRESULT CALLBACK MessageRouter(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam);
```

可以看到当你把鼠标放到函数名上的时候会显示注解：
![image](https://note.youdao.com/yws/public/resource/c6555434be43bcdee44e49ea613d8a7c/xmlnote/F88B0FAD8AC2428195E267A94C014B14/1149)