---
layout: post
title: 'Presentation Online 技术构思'
---

# redux

#### actions

- 微信登录、提交个人资料
- 上传文件、打开文件、切换文件
- 开始 online presentation、加入 online presentation
- 微博、微信、朋友圈分享
- 新建画板、删除画板
- 打开话筒、打开摄像头、申请话筒权限

#### reducers

实现各 actions 的功能

- 打开话筒：新建直播频道并进入新建的直播频道
- 上传文件、打开文件：百度云DOC上传文件、阅读文件

#### store

在 reducers 的基础上创建 store

#### Provider

包裹 components，传递 store

#### container components

给 UI components 传递参数

#### UI components

渲染 UI，向上事件