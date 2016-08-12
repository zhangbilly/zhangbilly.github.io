---
layout:     post
title:      "Windows 上安装 Jekyll"
subtitle:   "install Jekyll on Windows"
date:       2016-04-19
author:     "ZhangBilly"
header-img: "img/post_bg/jekyll-blog.jpg"
tags:
    - Jekyll
    - Windows
---
### 什么是 Jekyll
>Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。
    
主要的特点：

* 静态页面，也就是说无需数据库。但是这样的坏处就是每次需要遍历所有的文件。
* 支持HTML、Markdown、Textile。

### 为什么要用 Jekyll
第一次接触到 Jekyll 是因为在 github 上看到的 github pages，可以利用 github pages 搭建个人的博客，在我看来，使用github pages + Jekyll 的好处还是非常多的：

* 免费，无限流量。
* 享受git的版本管理功能，在本地有所有文章的备份。
* 自己的注意力只需集中在文章上，别的事情都不需要考虑。
* 无需考虑购买域名，搭建服务器什么的，轻松获得自己的个人博客。
* 可以自己定制网站样式

### 如何在 Windows 下安装 Jekyll

#### 安装 ruby
Jekyll 是基于ruby 的，所以需要先安装 ruby。前往 [ruby 官网](http://rubyinstaller.org/downloads/ "ruby 官网") 下载对应的版本，我这里下载的版本是Ruby 2.3.0 (x64)，安装中需要注意的只有两点：

* 路径中不要带空格，这个不只是安装 ruby 的时候需要注意，安装其他软件的时候最好也这样。
* 安装的时候有个选项是把 ruby 加入path 中，最好勾选这个选项，这样直接在命令行就可以使用 ruby 的命令了。

![安装ruby](/img/in-post/post-install-jekyll/install_ruby.png)

安装完成后可以在命令行中输入 `ruby -v` 检查是否安装成功。

#### 安装 DevKit
>DevKit 是一个在 Windows 上帮助简化安装及使用 Ruby C/C++ 扩展如 RDiscount 和 RedCloth 的工具箱。 详细的安装指南可以在程序的 [wiki](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit#installation-instructions) 页面 阅读。

再次前往前往 [ruby 官网](http://rubyinstaller.org/downloads/ "ruby 官网") 下载，	版本的选择如下：

* Ruby 1.8.6 to 1.9.3: tdm-32-4.5.2
* Ruby 2.0.0 and above (32bits): mingw64-32-4.7.2
* Ruby 2.0.0 and above x64 (64bits): mingw64-64-4.7.2

根据之前的ruby,我这里下载的是 DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe，下载完成后解压到一个文件夹，如E:\portable\DevKit。
    
打开命令行，运行以下命令：
    
`
ruby dk.rb init
`
    
根目录下会出现一个**config.yml**文件，打开文件，在末尾添加新的一行 - E:\Program64\Ruby23，路径需为 ruby 的安装路径，保存文件并退出。
    
运行`ruby dk.rb install`，安装即可。

####安装 Jekyll
其实到了这一步应该就很简单了，运行`gem install jekyll` 就可以了，
