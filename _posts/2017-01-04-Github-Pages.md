---
layout: post
title: "Github Pages和React"
---

Github Pages给我们提供了免费的托管静态网站的服务，但它只能提供静态文件。如果想用来动态生成页面的网站，那是实现不了的。不过它支持一种动态生成页面的服务，Jekyll。你把文章写在markdown里，放在制定的文件夹，jekyll会自动将这篇文章的链接添加到主页。别人点击链接时，jekyll能在服务器上运行，生成html页面，传给浏览器。

## Gatsby
最近学习React，为了练习，正在用Gatsby制作博客。Gatsby是用React制作的，React在浏览器、服务器上都能运行。结合Webpack, Babel等工具，它能在服务器上将相关的js文件打包、编译、压缩好，然后发给浏览器，但这是Github Pages所不支持的。

## gatsby build
但这也有解决办法，那就是在本地完成这些步骤，运行`gatsby build --prefix-links`命令行工具，Gatsby集成了这些打包工具，将html, css, js和图片等所有的文件打包到`/public`文件夹。这些是静态文件，可以直接用浏览器打开，从而可以托管在Github Pages上。

## branch
一般的做法是，将源文件和编译好的文件放在不同的分支：Gatsby源文件放在Gatsby分支，编译好的文件放在gh-pages分支，博客通过gh-pages分支进行访问。这样既有一个远程版本库用来管理代码、多人协作、开源，又能利用免费的Github Pages托管博客。

## Gatsby和Jekyll的比较
访问用Gatsby制作的博客时，可以发现，打开一个站内链接，访问速度很快，并没有整个网页刷新。但是访问Jekyll制作的博客，每打开一个页面，都要整页刷新。

这就体现了React的优势所在，React在浏览器上运行时，利用DOM diff算法，只向服务器请求改变的那部分。引用[阮一峰写的React入门教程](http://www.ruanyifeng.com/blog/2015/03/react.html)：

>组件并不是真实的 DOM 节点，而是存在于内存之中的一种数据结构，叫做虚拟 DOM （virtual DOM）。只有当它插入文档以后，才会变成真实的 DOM 。根据 React 的设计，所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上，这种算法叫做 `DOM diff`，它可以极大提高网页的性能表现。

虽然因为Github Pages只能托管静态文件的缘故，不能在服务器上用webpack动态生成html文件，必须提前打包、编译、压缩好，使得每一篇博客都有一个完整的html页面。但是打包好的React文件传到浏览器后，React的`DOM diff`算法就会发挥它的优势，只改变变动的DOM，而不是刷新整个页面。