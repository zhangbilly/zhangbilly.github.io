---
layout:     post
title:      "Windows 资源管理器已停止工作"
subtitle:   "软件冲突导致的问题"
date:       2016-08-12
author:     "ZhangBilly"
header-img: "img/in-post/windows_explorer_is_not_working/bg.jpg"
tags:
    - windows
---

# Windows 资源管理器已停止工作
某一天开机后点击快速启动栏启动程序，发现弹出了下面的错误。之前遇到过只是杀进程，然后再重新启动进程就可以，但是这次不行。

![资源管理器已停止工作](http://obrw4fa70.bkt.clouddn.com/windows_explorer_is_not_working.png)

后来查了一下，发现可能是软件冲突造成的。解决方法如下： 
   
1. 打开运行（win+R），输入eventvwr，回车，打开事件管理器
2. 在左侧依次点击windows日志，应用程序，即下图中标注1
3. 在中间区域找到资源管理器的错误，即下图中标注2
4. 在中间下方查看具体错误，在错误模块路径发现是adSafe的问题，即下图中的标注3
5. 关闭adSafe，再点击果然没有问题了。

升级一下adSafe或许就没有问题了。

![事件管理器](http://obrw4fa70.bkt.clouddn.com/event_mgr.png)