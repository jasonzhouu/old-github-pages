---
layout: post
title: 'Online Presentation 技术可行性分析'
---

目前知道的几种可以进行Online Presentation，而且只需要浏览器的技术：

### Powerpoint Online

**技术实现：**用户上传PPT，前端向后端发起POST请求到指定的URL，后端收到文件后将PPT重命名，放到指定的目录，并在数据库里记录文件名。在前端页面插入https://view.officessapps.live.com指定src的<iframe>，src的src参数为文件路径，这样即可在浏览器上观看并控制PPT。

**优点：**方便，用Office的API轻松实现在浏览器上观看PPT。

**缺点：**无法通过后端控制前端PPT当前展示的页码，实现broadcast。

<iframe src='https://view.officeapps.live.com/op/embed.aspx?src=http%3A%2F%2Fvideo%2Ech9%2Ems%3A80%2Fbuild%2F2011%2Fslides%2FTOOL%2D532T%5FSutter%2Epptx&wdAr=1.7777777777777777' width='610px' height='367px' frameborder='0'>这是嵌入 <a target='_blank' href='https://office.com'>Microsoft Office</a> 演示文稿，由 <a target='_blank' href='https://office.com/webapps'>Office Online</a> 支持。</iframe>

## Powerpoint Web Apps

**技术实现：**上传文件的方式和前面Powerpoint Online一样，在服务器安装Sharepoint Server。

**优点：**后端**也许可以**（还没有对Sharepoint深入了解，暂时不确定）对PPT的<iframe>有更多的控制，实现broadcast。

**缺点：**后端需要做的事情更多，需要学习和使用Sharepoint，及C#语言和ASP.NET框架。

<iframe width='630px' height='367px' id="fullframe" src="http://ppt.dongboke.com/p/PowerPointFrame.aspx?WOPISrc=http%3a%2f%2f192.168.164.1%3a888%2fwopi%2ffiles%2f1333197136400998400-1333535900816105472-1.ppt%3fa%3d1&amp;PowerPointView=SlideShowView" frameborder="0"></iframe>

### PDF.js

**技术实现：**用户上传PPT，后端将其转成PDF，并存储。或者用户直接上传PDF，后端直接存储。前端使用PDF.js插件，渲染出PDF，可以通过参数控制PDF当前展示的页码，所以可以通过后端控制，并实现broadcast。

**优点：**可以实现broadcast。

**缺点：**没有PPT的动画效果。