---
layout: post
title: "Docker加速器"
---

# Docker for Mac加速器

## DaoCloud加速器
`docker pull`命令在中国访问起来有点不稳定，一开始我用的[DaoCloud加速器](https://www.daocloud.io/mirror.html#accelerator-doc)，使用很方便，只要在Docker for Mac的preference->Advanced->Registry mirrors里添加一个镜像地址就好了，但仍然有问题，常会下载到一半就下载不下去了。

## Aliyun加速器
然后就尝试着使用[Aliyun加速器](https://cr.console.aliyun.com/?spm=5176.1971733.0.2.0EnIdt#/accelerator)，照着里面说的安装了Docker Toolbox，但是仍然没有用。而事实上，Docker for Mac的推出就是用来代替Docker Toolbox的，所以Aliyun上的文档估计是过时了。然后我把Aliyun提供的加速器地址也照着DaoCloud加速器的方法一起添加到Registry mirrors上，然后就好多了。![]({{ site.ur }}/images/Snip20161216_15.png)
