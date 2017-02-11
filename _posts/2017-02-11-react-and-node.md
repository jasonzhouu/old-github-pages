---
layout: post
title: 'React and Node'
---

### Node

node有两方面作用：

- http服务器：响应浏览器的http请求，根据url发送相应的数据
- data服务器：调用数据库

可以单纯用Node搭建网站，最好加上Express框架、ejs模版，Node制作的网站可以具备调用数据库的能力。但是仅仅用ejs，就没有了React的强大能力。不过ejs也是具有React没法取代的用处的，比如用header.ejs，footer.ejs模版。

### React

功能：用于用户端页面的展示。

可以单纯用React搭建网站，但网站是静态的，也就说没有数据库。比如Gatsby就是纯React，有html页面，有bundle.js。浏览器请求页面，根据url决定发送哪一个html文件。

在纯React页面的开发中，因为没有node的服务器功能，只能直接打开html页面，这样会有一些缺点。可以用npm安装live-server插件，从而能创建一个临时的服务器。

### Node + React

两者合用时的分工：

- node仍然负责http服务器和数据库服务器的功能
- React负责页面的展示

node通过路由决定给浏览器发送什么文件。然后，前端页面通过API请求数据时，node从数据库调用数据，并整理成JSON发送给前端页面，前端页面调用JSON并加入DOM中。