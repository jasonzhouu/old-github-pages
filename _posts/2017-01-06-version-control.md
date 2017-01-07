---
layout: post
title: "【占坑帖】Git"
---

## 用到Git的原因

- Github Pages
- 在Github上看别人的源代码。虽然可以直接download，不怎么需要看历史版本，但是如果想认真学习，可以从源代码最开始的版本开始看。最开始的版本会比较简单。
- 对自己的代码进行版本管理。因为现在能写的代码还很少，这个需要还不怎么强。但随着知识系统的建立，代码量也许会很快
- 参与开源项目。同样暂时还不会用到。

## 了解Git的历程

- 2016.06.14 注册Github
- 2016.12.04 在宁皓网看Git的教学视频
- 2016.12.10 建立第一个repositoriy---jasonzhouu.github.io，作为个人博客
- 2017.01.06 阅读*[Pro Git](https://git-scm.com/book/zh/v2)*

## 有待加强的知识点

- pull request
- branch

## 常见命令

| 任务      | 命令                                       |
| ------- | ---------------------------------------- |
| 查看本地分支  | git branch (-a)添加后缀，结果会包括远程分支            |
| 删除本地分支  | git branch -d + 分支名                      |
| 推送到远程分支 | git push origin + 远程分支名                  |
| 查看远程分支  | git remote show origin                   |
| 删除远程分支  | git push origin  --delete + 远程分支名        |
| 添加远程    | git remote add + 自定义远程名 + https://github.com/###/###.git |
| 查看添加的远程 | git remote (-v) 添加后缀，结果更详细               |
| 获取远程的更新 | git fetch                                |
| 合并      | git merge 远程名/本地分支名                      |
| 本地分支改名  | git branch -m + 原分支名 + 目标分支名             |

## 应用实例

### 一、Gatsby

**问题：**Gatsby源文件在Github Pages无法运行，Github Pages只支持静态文件。命令行`>gatsby guild`可以编译出静态文件放在`/public`目录，将`/public`目录下的文件放到Github上。但最好有两个分支，分别用于管理Gatbsy源文件和`/public`文件夹。

**解决办法：**将Gatsby源文件放在master分支，通过.gitignore文件忽略`/public`文件夹。将`/public`文件夹放在gh-pages分支。

**步骤：**

1.在Gatsby源文件目录下：

在.gitignore文件下添加`public`，Git将忽略这个目录，推送到远程分支时也不会推送这个文件夹，`node_modules`目录也是通过这个方法被忽略的。

```CLI
> git init
> git add .
> git commit -m "..."
> git remote add origin http://github.com/###/###.git	添加远程
> git push origin master	推送到远程的master分支
> gatsby build	编译成静态文件
```

2.在`/public`目录下：

```CLI
> git init
> git add .
> git commit -m "..."
> git remote add origin http://github.com/###/###.git	添加远程
> git push origin gh-pages	推送到远程的gh-pages分支（会在远程自动创建gh-pages分支）
```

占坑，其余的逐渐补上:smile: