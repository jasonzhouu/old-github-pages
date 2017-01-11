---
layout: post
title: "【占坑帖】搭建开发环境"
---

搭建环境的方法有很多种，MAMP，虚拟机，容器，或者像jekyll/gatsby这样自带创建模拟服务器的功能。仅创建虚拟机的软件就有很多种，我所知道的有：

- VMware
- Virtual box -> Vagrant (CLI) -> Vagrant Manager
- Veertu Desktop

通过命令行快速实现：

- 用python可以很简便的创建服务器，在文件目录执行命令行`python -m SimpleHTTPServer`，然后shell会提示`Serving HTTP on 0.0.0.0 port 8000 ...`，打开服务器，输入URL：`localhost:8000/文件名`，就可以了。
- 用Node：进入项目目录执行命令行`node 文件名.js`，就会创建在`localhost:3000`的服务器

mark一下，后面补上