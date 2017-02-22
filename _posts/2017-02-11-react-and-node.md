---
layout: post
title: 'React and Node'
---

### Node

node有两方面作用：

- http服务器：响应浏览器的http请求，根据url发送相应的数据
- data服务器：调用数据库

可以单纯用Node搭建网站，最好加上Express框架、ejs模版，Node制作的网站可以具备调用数据库的能力，但ejs没有React功能强大。不过ejs也是具有React没法取代的用处的，比如用ejs可以设置header.ejs、footer.ejs模版用于存放网页的头文件和css/js文件的url，这是React做不到的。但是这并不难，用React时，只要做一个包含所有头文件盒css/js文件的url的index.html就行了。

### React

功能：用于用户端页面的展示。

可以单纯用React搭建网站，但网站是静态的，没有数据库，内容不是活的。内容再多，用户也不能改变内容，只能使用。Gatsby生成的博客页面就是纯React，有index.html，有bundle.js。浏览器通过url请求文件，服务器做出响应。

在纯React页面的开发中，因为没有node的服务器功能，而直接打开html页面会有一些缺点。可以用npm安装live-server或webpack-dev-server插件，用npm script指定监测的目录，创建一个临时的服务器，并且浏览器能监测到文件改变自动刷新页面。

### Node + React

两者合用时的分工：

- node仍然负责http服务器和数据库服务器的功能
- React负责页面的展示

node根据url决定给浏览器发送什么文件。前端页面通过API请求数据时，node从数据库调用数据，生成JSON发送给前端页面，前端调用JSON生成view。