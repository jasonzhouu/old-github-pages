---
layout: post
title: "前端开发工作流"
---

以下内容根据”猿生态十城沙龙|杭州“上网易云信负责人张迎亚的演讲”漫谈前端开发工作流“整理而成。

## 从工作坊到流水线
前端开发从最开始可以一个人手工用HTML, CSS, Javascript制作网站已经转变成了如今需要团队协作才能完成，一些大型的网站一个人已经是很难完成了，团队里每个人只负责整个项目中的一部分。就像汽车生产的流水线一样，没有人能独立制造一辆汽车，汽车生产的每个员工都只负责整个流水线上的一个细小流程。

团队协作需要降低沟通成本，通过制定规范、让代码更加可维护、使代码复用，从而提高团队协作的效率。

## JS

### 格式校验工具
Jslint, JSHint, ESLint, Flow

其中Flow是Facebook出的静态类型检查工具，可以提前找出错误。错误越早检查出来，修改的成本就越小。

### 模块化
AMD（异步模块定义）, CommonJS, UMD, ES2015 Module

这么多种模块化的规范，有可能会给团队合作带来障碍，模块化还有一种终极解决方案：

	Webpack + Babel + ES2015

Webpack可以将JS, CSS, 图片文件进行打包，从而减少网络请求次数，提高网页访问速度。

## CSS

### 功能缺失

* import：将CSS按功能分成一个个文件，用import命令综合，以便于维护
* nest：用嵌套写出更优雅的代码
* Autoprefixer：自动加前缀，以适配各浏览器
* mixin/extend
* variable：变量，便于常用变量的复用
* if/for/while

但是通过工具可以弥补上面的功能缺失：Less, Sass, Stylus, PostCSS

### 校验工具
Stylelint

## 包管理工具
生产过程中会用到很多工具，比如：处理cookie的工具……所以需要一个包管理工具进行综合：Bower, component, jspm, npm, yarn

推荐使用npm，但是基于npm现在又推出了yarn.

yarn的下载来源和npm相同，但是具有以下优点：

* 支持离线下载，只要下载过一次，下次用到的时候可以直接调用，不用重新下载
* lock文件：可以认定某个包的特定版本，使用包的特定功能时，不用担心包在更新版本的时候这个功能缺失了
* 网络性能优化，支持并行下载
* 自动重试

工具在工程化中非常重要

## 常规任务
* 打包JS, CSS
* 混淆压缩JS：可压缩至原来文件的1/5
* 混淆压缩CSS
* JS source map：根据混淆压缩文件对应至源码，便于修改代码时定位
* CSS source map
* 打包图片资源：精灵图，雪碧图。网站开发中会用到很多小图标，以提高用户体验，但也会增加网络请求，所以将这些小图标打包成一张图片。
* 开发环境与生产环境的差异
* mock（模拟）数据：后端需要给前端数据，前端负责将数据展现出来，但是开发过程中后端还没有提供数据时，前端可以模拟数据进行渲染。
* 自动监听变更：文件改变时浏览器自动刷新页面

## 任务调度器 Task runner
Grunt, Gulp, Broccoli, Brunch, npm scripts

推荐npm scripts

## 举例

### 做Web IM SDK（聊天SDK）
任务：

* 生成各个环境相关的SDK文件
* 生成测试工程
* 生成API文档，拷贝、压缩、上传
* 生成开发文档，拷贝
* 打包发布SDK、API文档、开发文档

### Node
有句话叫：人生苦短，请用Python。而Node就是前端的Python。因为JS用起来比较熟悉，可以用ES2015最新的语言规范。
ES2015的最新语法：

* const/let
* default function parameter
* spread (....) operator
* ovject literal extensions
* template literals
* destructuring
* arrow function
* class/super/module
* promise/generator/asunc await

而Webpadck + Babel让我们可以提前使用最新的语法，然后转成browser能理解的形式。

## 规范之后——复用
* DRY (Don't repeat yourself)
* 抽取公共的部分，提交到npm。包括各种配置文件，webpack, ESlint, stylelint etc.

## 升级之路
马上动手做一个项目，在项目中会遇到各种坑，将各个问题一个个解决。

## 学习工程化
找一个开源项目，照着它的工程化方式进行。看他的README, Lisence。

## 组件化
一项工程由这些组成：组件，模块，公共方法
使用组件从而实现功能的复用，组件是由完整的HTML, CSS, JS构成的。