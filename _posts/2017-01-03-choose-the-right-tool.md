---
layout: post
title: "用正确的工具"
---

## 网站的类型
互联网在不断发展，由最初的静态页面，不断发展到现在的单页应用(SPA, single page application).

 1. 最初我们用原生的html, cass, javascript代码写出一个完整的页面，放在服务器上，浏览器访问后下载完整的页面呈现出来。

 2. 但是内容变多以后，网站的管理就困难起来，而且每个页面都要重复很多代码，为了代码的复用原则，出现类似jekyll这种模式，服务器能够自动生成html页面。我们只要将markdown文件放在指定的文件夹。
 3. 然后又出现了wordpress, drupal, joomla!这些内容管理系统(CMS, content management system)，提供一个管理员界面，我们可以直接在管理员界面管理内容，发布、删除、更改。
 4. 上面这些模式都有个共同点，只有网站的维护人员能够影响网站的内容，用户则不能。用户使用网站的需求逐渐增强，他们需要控制自己的个人主页，发表状态。总之，他们要向服务器发送更多的数据，而不仅仅是服务器向他们发送数据。这时便诞生了新的技术，即单页应用(SPA)。类似react, vue, angular这些技术都能帮我们实现这个目标，它们使得浏览器上的状态、服务器上的数据、用户的操作这三者的互动能够以更加简便、易读、可扩展的代码实现。

上面4种制作网站的方式现在应该都有人用，因为它们都有各自适用的场景。最关键的永远是思考自己要制作的网站的特点，以及它最适合的制作方式。

## 我的使用经历
我在学习 html&css 4天后制作的第一个网站就是用第一种方式制作的，它只有两三个页面，并没有太大问题，而且可以帮助我练习这两种语言。

我现在用的博客就是用第二种方式制作的，它让我快速的制作出了自己的博客，而不需要了解太多里面的技术，因为整个网站自动生成页面的过程jekyll已经帮我实现了，也有大量别人做的现成的主题，我只要明白使用规则，按照规则使用就行。这样勉强可以用，但是体验并不好。虽然它让我对网站的主题拥有了更大的控制权，但相比“简书”这种博客网站，使用体验还是稍微差一点。在“简书”上我直接在网站上写作，直接按发表，文章就发出了，但是jekyll则需要我生成markdown文件，并上传到服务器指定的文件夹里，而且每一次修改我都需要重新上传。

## Drupal
今天在宁皓网里看到王皓因为参加drupal camp线下聚会而写的一篇文章，总结了制作这个网站的历程。宁皓网是用drupal制作的，而且自从2006年诞生以来几乎没有改动过。他认为drupal让他这种不懂技术的人，也大概能实现自己的想法。引用原文：

>当时做宁皓网的时候，我其实基本从零开始自学的。我不懂 PHP，不会 JavaScript ，其实我现在也不怎么懂：）也不了解 Linux 服务器，只会一点 CSS 跟 HTML，能做个静态网页。
>
>我现在想想，当时得亏有 Drupal，不然想我这样的，永远也不可能做出来。因为我当时就只有一个想法，就是录一些视频放网上，大家付了费就可以看了，不付费不能看，会员资格过一段时间就会自动取消，用户可以再续费。所有的功能 Drupal 其实都给我提供了，我也没写几行代码，其实主要就是做了一个模板，然后把一些现成的功能模块拼到一块儿。
>
>我觉得 Drupal 最厉害的地方就是能让我们这些不懂技术的人，也大概可以实现自己的想法。

这让我突然发现drupal的强大之处，它降低了制作网站的门槛，提供大量的功能，让我们直接使用就行。

## 用正确的工具
但是我大概是想起之前尤雨溪在演讲里说的：

>要选择合适的工具。

虽然他讲这个的背景是指需求的内在复杂度和工具的复杂度要匹配。大概意思就是不要用宰牛刀杀鸡，也不要用小刀宰牛，根据不同的场景用最适合的工具。

任何工具都不是万能的，它都有自己擅长的方面、不擅长的方面，所以我们永远都应该要选择合适的工具，而不是看到一个工具强大的方面就不顾一切地去用。

## Drupal适合的场景和不适合的场景
本着这种想法，我上谷歌搜索"drupal good at"，想了解drupal擅长什么，不擅长什么。两个网页解决了我的疑问, 第一个是[Drupal. Good or bad? : PHP - Reddit](https://www.reddit.com/r/PHP/comments/2v2cnu/drupal_good_or_bad/).

>The problem is that Drupal and WordPress are not custom application frameworks: they're CMSes, and they are designed to handle specific use cases that fall within that domain: Drupal is more geared towards enterprise-esque monolithic content management while WordPress is geared towards blogs and mom-and-pop brochureware sites.

正如里面说的Drupal, WordPress本质上还是【内容】管理系统，Drupal适合企业管理大量的内容，WordPress适合个人博客和夫妻店这种小的网站，但它们都不适合制作web app。

另外一篇，[When is Drupal not the right choice? - Yuriy Babenko](http://yuriybabenko.com/blog/when-drupal-not-right-choice)，作者用drupal做过非常多的项目，遇到过很多需求场景。

>**What is Drupal?**
>
>Drupal is primarily a framework, one that can be used to build a CMS, but out of the box it is nothing more than a toolset with some basic functionality - a codebase and some interface forms. Drupal is not a blogging platform, not an ecommerce store, not a forum, and not a social network, but it can be used to build all of these (and then some).
>
>An experienced Drupal developer can dissect the system, turn it sideways, and make it do things it was never even remotely intended for (while still following the best practices), but the tricky part is looking at every project objectively and deciding not whether you can, but whether you should.
>
>**The strengths**
>
>Drupal's tools are fantastic at structuring and managing content. The Entity, Field and Form APIs make managing content a pleasure, while modules like Taxonomy and Menu give us efficient ways of structuring, organizing, and filtering the content. Even on the presentation side of things we've got the flexible theme layer and tools like Display Suite to give us more options than anyone is likely to need. If your project's primary uses cases centre around creating, managing and viewing content, all this will combine for a great developer experience.
>
>
>**A large content base does not a content-driven site make**
>
>On the other hand, if the project requires a complex content review flow, integration with a dozen third-party APIs, tricky UI elements, tons of user-driven events and tens of thousands of lines of custom modules to achieve your end goal, there's a good chance you're building an application and not a content-driven site. Take Twitter for example: massive amounts of content, but not content-driven; it's all about user interactions, not the tweets themselves.
>
>**The weaknesses**
>
>**Performance**. Drupal has never been a fast performer; the philosophy of tailoring to everyone's needs resulted in large codebase, an overly normalized database and other selectively-unnecessary bloat to provide the desired flexibility. Any given project will often only take advantage of 30 - 40% (gut feeling estimate) of what Drupal is capable of out of the box. The remaining functionality does nothing but slow things down, and the architecture decisions made to achieve that functionality will also have impacted the performance of the parts you are using.
>
>Now you have to optimize a large codebase of contributed modules that you're likely not familiar with, and ones which were probably not tested in conjunction with the other modules you're using. 
>
>**Development**. Drupal development can be tricky. The programming itself is rarely anything "hard," but it takes a lot of effort & experience to understand the concepts, flow, and the implications of the changes you're making. 
>
>If you are a start up, building a proof of concept, or otherwise an application that is not 100% defined and may change at any moment (ie. a real agile project), Drupal is the last thing you want to be using. 
>
>**xtl;dr;**
>
>At the end of the day, it's in your (and your client's) best interest to scope out the projects properly, and pick the best tool for the job, which may not be the one you're most experienced with.

Drupal是一个大而全的工具库，这些工具很适合用于架构和管理内容，它的好处是给我们带来了很大方便，我们只要使用使用它30 - 40%的功能就足以制作一个内容网站。

但是这带来的一些问题：

 - 运行性能的下降，如果想要对它的性能进行优化，面对一大堆的代码，难度会非常之大。
 - 如果要添加一些库、模块，并不能保证和Drupal兼容。
 - 如果要在Drupal基础上做一些开发，了解Drupal内部的原理会很耗时间。非常不适合目标还不明确，需要经常改动的初创项目。

## 情况明了

Drupal方便快速开发一个内容网站，这个网站最好做好之后就不需要改动，没有用户驱动的内容，不需要太多第三方的库，而且不讲究性能。

如果项目经常要改动，有很多用户驱动的内容，需要很多模块、第三方的库，用户量大，对性能有要求，那就不适合用Drupal。

## 项目开始前要评估
在开始项目前一定要对项目进行评估，然后选择合适的工具，即使这个工具并不是你最擅长的。