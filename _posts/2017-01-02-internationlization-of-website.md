---
layout: post
title: "网站的国际化（支持多语言）"
---

## 支持多语言的重要性
全世界有很多语言，在互联网上仅使用人数超过一亿的语言就有7种。

![]({{site.url}}/images/most_used_languages_on_the_internet_2015.png)

虽然中国人口数量很大，很多网站仅仅面向国内就能生存，但在21世纪我们必须要有国际化视野。正如吴军老师说的：

>中国人还有两门课要学：**国际化** 和 **资本**

在中国以外的地方还有更加广阔的天地。

![]({{site.url}}/images/the_world_online.png)

很多国家的网速比我们快

![](http://ourworldindata.org/wp-content/uploads/2015/07/ourworldindata_average-download-speeds.jpg)

在[internet live stats](http://www.internetlivestats.com/)可以看到全世界有35亿多的互联网用户，中国互联网用户数量全世界第一，有7亿，但也只占五分之一而已。将一些比中国经济更发达的国家的互联网用户数加起来超过10亿，但是这些国家使用的语言却非常之多，有英语、葡萄牙语、日语、俄语、德语、法语、韩语。

![]({{site.url}}/images/Snip20170102_9.png)

要让网站面向全世界，就必须实现多语言化。

## 技术上的方法
在github上搜索internationlization，能找到很多javascript语言编写的实现多语言化的工具。

最受欢迎的有：

### 1.基于rails环境的[i18n](http://guides.rubyonrails.org/i18n.html)
Angular制作了相应的库[angular-translater](https://angular-translate.github.io/)，在github上有4000多星。vue也有对应的[vue-i18n](https://kazupon.github.io/vue-i18n/)

 ![]({{site.url}}/images/Snip20170102_6.png)
 
 i18n是Internationalization and localization的缩写，wikipedia讲解[Internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization)时提到：

 >The terms are frequently abbreviated to the numeronyms i18n (where 18 stands for the number of letters between the first i and the last n in the word internationalization, a usage coined at DEC in the 1970s or 80s) and L10n for localization, due to the length of the words.
 
### 2.yahoo出品的[format.js](http://formatjs.io/)
支持React, Ember框架，react对应的[react-intl](https://github.com/yahoo/react-intl)有3700多星。

 ![]({{site.url}}/images/Snip20170102_3.png)
 
### 3.支持几乎所有主流框架的[i18next](http://i18next.com/)
有1800多星。

 ![]({{site.url}}/images/Snip20170102_5.png)
