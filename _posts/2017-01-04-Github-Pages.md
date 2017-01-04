---
layout: post
title: "Github Pages和Gatsby"
---

Github Pages给我们提供了免费的托管静态网站的服务，但它有个限制：只能用静态文件，不能动态生成页面。它只支持一种动态生成页面的工具——用Ruby编写的Jekyll。

## Gatsby
Gatsy是什么？是一个模块，引用[Scott Nonnenberg](https://blog.scottnonnenberg.com/static-site-generation-with-gatsby-js/)的解释：

>It’s a node module which weaves together React.js, React-Router, webpack, and webpack-static-site-generator. You get a nice development experience with hot-reload for page contents, styles and page structure, and you’re working with the same markup as what is generated to disk for production builds. It’s as simple as running `gatsby develop` or `gatsby build` on the command-line.
>
>Gatsby configures everything for you, resulting in the same benefits with a lot less work setting up a new project.

Gatsby是一个node模块，它集成了react, webpack，而且配置好了，只需要运行`gatsby build`就可以将各种组件打包成静态文件，以便托管在Github Pages上。

Gatsby会将整个网站打包、压缩到bundle.js，通过index.html访问主页时会加载这个文件。markdown文件也会被转换成JSON文件，并被包含在bundle.js里。

>Gatsby uses Webpack loaders to convert Markdown into something a React.js component can handle. So a loader is basically a conversion script, it takes any sort of raw input and loads it into a JSON file so it turns something into JavaScript objects

bundle.js包含了整个网站要用到的数据，点击站内链接链接时会直接从中获取，反应非常迅速，就像本地应用一样。

不过这样的缺陷也很明显，如果网站的页面很多，bundle.js文件会很大，第一次加载网站时会很花时间。Gatsby的作者Kyle Mathews在演讲[DEVELOPING WITH REACT: GATSBYJS](http://www.staticwebtech.com/presentations/developing-with-react-gatsbyjs/)里是这样回应的：
>Right now you’d probably top out at around 500 to 1000 pages is where Gatsby could easily do.
>
>The main bottleneck is Gatsby turns all your content, combines all your content into the JavaScript bundle so that you have kind of that single page app experience once it’s loaded, all the content’s there in your browser and you just click around and it’s all there. But at 500,000 pages, that JavaScript bundle is starting to get pretty big. More than you’d normally want to load into your site and so but there’s a process where, with Webpack where you can split up the bundle and asynchronously load different bundles as you navigate around the site. You’d only need to load one of those bundles when you first open the site and then if you navigate to another section of the site it would then load in the background the JavaScript you need for that section of the site. 

通过限制webpack打包的bundle.js文件大小的上限，将网站打包成多个bundle.js，当访问到加载的第一个bundle.js文件外的页面时会自动加载对应的bundle.js。



## 打包成静态文件
Gatsby的核心是React框架，React在浏览器、服务器上都能运行，结合Webpack，将整个网站打包、编译、压缩。运行`gatsby build --prefix-links`命令行就能完成，Gatsby集成了这些要用到的打包工具。将html, css, js和图片等所有的文件打包生成静态文件，放到`/public`文件夹。

## branch
一般的做法是，将源文件和编译好的文件放在github不同的分支：Gatsby源文件放在gatsby分支，编译好的文件放在gh-pages分支，博客通过gh-pages分支进行访问。这样既有一个远程版本库用来管理代码、多人协作、开源，又能利用免费的Github Pages托管博客。

## Gatsby和Jekyll的比较
### 访问速度
访问用Gatsby制作的博客时，可以发现，打开一个站内链接，访问速度很快，并没有刷新整个网页。但是访问Jekyll制作的博客，每打开一个页面，都要整页刷新。

这正体现了React的优势所在，React在浏览器上运行时，利用DOM diff算法，从而优化了访问的性能。引用[阮一峰——React入门教程](http://www.ruanyifeng.com/blog/2015/03/react.html)里的文字：

>根据 React 的设计，所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上，这种算法叫做 `DOM diff`，它可以极大提高网页的性能表现。

虽然因为Github Pages只能托管静态文件的缘故，导致不能发挥React完整的优势。否则可以通过组件动态生成html文件，用`DOM diff`算法以减少网络请求。我们必须提前将文件打包、编译、压缩好，给每一篇博客都生成一个完整的html页面。但是打包好的React文件传到浏览器后，React的`DOM diff`算法还是能发挥它的部分优势，即只改变变动的DOM，而不是刷新整个页面。

### 上传步骤
Gatsby比Jekyll多一个步骤，运行命令行`gatsby build`。如果用Github Desktop的话需要切换一次界面，反倒不如也用git的命令行工具执行上传命令。
