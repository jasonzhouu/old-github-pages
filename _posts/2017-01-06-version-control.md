---
layout: post
title: "【占坑帖】Git"
---

主要因为以下几个原因而要用到Git:

- Github Pages
- 在Github上看别人的源代码。虽然可以直接download，不怎么需要看历史版本，但是如果想认真学习，可以从源代码最开始的版本开始看。最开始的版本会比较简单。
- 对自己的代码进行版本管理。因为现在能写的代码还很少，这个需要还不怎么强。但随着知识系统的建立，代码量也许会很快
- 参与开源项目。同样暂时还不会用到。

了解Git的历程：

- 2016.06.14 注册Github
- 2016.12.04 在宁皓网看Git的教学视频
- 2016.12.10 建立第一个repositoriy---jasonzhouu.github.io，作为个人博客
- 2017.01.06 阅读*Pro Git*

有待加强的知识点:

- pull request
- branch

常见命令：

| 任务            | 命令                                       |
| ------------- | ---------------------------------------- |
| 查看本地分支        | git branch                               |
| 删除本地分支        | git branch -d + 分支名                      |
| 推送到远程分支       | git push origin + 远程分支名                  |
| 查看远程分支        | git remote show origin                   |
| 删除远程分支        | git push origin  --delete + 远程分支名        |
| 查看所有分支（本地+远程） | git branch -a                            |
| 添加远程          | git remote add + 自定义远程名 + https://github.com/###/###.git |
| 查看添加的远程       | git remote (-v) 添加后缀，结果更详细               |
| 获取远程的更新       | git fetch                                |
| 合并            | git merge 远程名/本地分支名                      |
| 本地分支改名        | git branch -m + 原分支名 + 目标分支名             |

占坑，其余的逐渐补上。