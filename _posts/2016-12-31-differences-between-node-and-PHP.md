---
layout: post
title: "node和PHP的不同"
---

node缺乏使用PHP过程中的一些便利，比如：

 - PHP可以将代码和标记输出无缝结合起来，Node需要借助模版引擎
 - PHP可以使用现成的Web服务器（Apache, Ngingx），Node则提供了构建Web服务器的框架，需要自己写服务器，但是很简单。

如下代码实现创建一个Web服务器，并输出Hello World!

```
var http = require('http');

http.createServer(function(req, res) {
	res.writeHead(200, {'Content-Type': 'text/html' });
	res.end('<h1>Hello World!</h1>');
}).listen(3000);

console.log('Server started on localhost:3000; press Ctrl-C to terminate...');
```
但是让我们取得了对程序的控制权。