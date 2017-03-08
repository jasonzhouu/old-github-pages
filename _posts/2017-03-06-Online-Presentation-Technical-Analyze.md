---
layout: post
title: 'Online Presentation 技术可行性分析'
---

目前知道的几种可以进行Online Presentation，而且只需要浏览器：

## Powerpoint Online／Powerpoint Web Apps

2009年微软发布PowerPoint Web Apps，2014年改名为PowerPoint Online。

**技术实现：**用户上传PPT，前端向后端发起POST请求到指定的URL，后端收到文件后将PPT重命名，放到指定的目录，并在数据库里记录文件名。在前端页面插入https://view.officessapps.live.com指定src的<iframe>，src的src参数为文件路径，这样即可在浏览器上观看并控制PPT。或者，在服务器安装Office Web Apps Server，配置好WOPI协议，或者作为SharePoint的app安装。

> The service can also be installed privately in enterprise environments as a [SharePoint](https://en.m.wikipedia.org/wiki/SharePoint) app, or through Office Web Apps Server.
>
> https://en.m.wikipedia.org/wiki/Office_Online

**优点：**

- 保留了PPT的动画效果；
- 支持Excel, Word, PowerPoint格式；

**缺点：**不能否实现广播。

1. #### 用view.officeapp.live.com

需要访问微软的服务器，访问速度很慢。

<iframe src='https://view.officeapps.live.com/op/embed.aspx?src=http%3A%2F%2Fvideo%2Ech9%2Ems%3A80%2Fbuild%2F2011%2Fslides%2FTOOL%2D532T%5FSutter%2Epptx&wdAr=1.7777777777777777' width='610px' height='367px' frameborder='0'>这是嵌入 <a target='_blank' href='https://office.com'>Microsoft Office</a> 演示文稿，由 <a target='_blank' href='https://office.com/webapps'>Office Online</a> 支持。</iframe>

2. #### 自建服务器

访问自己国内的服务器，对访问速度拥有更大的控制。

<iframe width="700px" height="385px" src="http://ppt.dongboke.com/p/PowerPointFrame.aspx?WOPISrc=http%3a%2f%2f192.168.164.1%3a888%2fwopi%2ffiles%2f1333197136400998400-1333535900816105472-1.ppt%3fa%3d1&amp;PowerPointView=SlideShowView"></iframe>

## PDF.js

**技术实现：**用户上传PPT，后端将其转成PDF，并存储。或者用户直接上传PDF，后端直接存储。前端使用PDF.js插件，渲染出PDF，可以通过参数控制PDF当前展示的页码，所以可以通过后端控制，并实现broadcast。

**优点：**可以实现broadcast。

**缺点：**

- 没有PPT的动画效果；

- 需要后端转码。

## [百度云文档服务 DOC](https://cloud.baidu.com/product/doc.html)

可以实现：

- 加载在线文档
- 加载文档时指定页码
- 文档阅读翻页事件

**优点：**

- 可以实现broadcast；
- 支持Excel, Word, PowerPoint格式；
- 实现方便；
- 云存储。

**缺点：**

- 后端的工具包使用Java语言；
- PPT没有动画效果；
- 需要付费，但价格便宜。

| 计费项         | 按月累计阶梯  | 单价          |
| ----------- | ------- | ----------- |
| 存储容量        | --      | 0.005元/GB/天 |
| 转码成功次数      | 0~1500次 | 0.15元/次     |
| 1501~3000次  | 0.12元/次 |             |
| 3001~30000次 | 0.1元/次  |             |
| 30001次以上    | 0.08元/次 |             |
| 外网下行流量      | --      | 0.5元/GB     |

