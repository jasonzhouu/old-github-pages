---
layout: post
title: "网站的国际化（支持多语言）"
---

## 互联网世界的语言
全世界有很多语言，在互联网上仅使用人数超过一亿的语言就有9种，以下是使用人数最多的10种语言：

![]({{site.url}}/images/languages2016.png)

 - 使用英语和中文的互联网用户数量大大领先于其他语言，两者加起来有17亿
 - 使用另外8种语言的互联网用户加起来一共11亿
 - 使用所有其他语言的互联网用户加起来一共8亿
 
## 国际化

虽然中国人口众多，很多网站仅面向国内就能生存，但在21世纪我们要有国际化视野。正如吴军老师说的：

>中国人还有两门课要学：**国际化** 和 **利用资本的力量**

在中国以外的地方还有更广阔的天地。

![](https://i0.wp.com/geonet.oii.ox.ac.uk/wp-content/uploads/sites/46/2015/07/OII-Internet_population_cartogram.png)

而且很多国家的网速比我们更快，人均GDP比我们高

![]({{site.url}}/images/ourworldindata_average-download-speeds.jpg)

## 中国互联网用户占全世界的1/5
在[internet live stats](http://www.internetlivestats.com/)可以看到全世界有35亿多的互联网用户，中国互联网用户数量全世界第一，有7亿，但也只占世界的五分之一，我们不应该固守于国内，而应该奋发进取，争取外面更广阔的市场。比中国经济更发达的国家的互联网用户数加起来超过10亿，他们支付能力更强，付费习惯更好，市场潜力很大，但他们使用各种不同的语言。

![]({{site.url}}/images/Snip20170102_9.png)

**所以，必须实现多语言化。**

## 技术上的方法
在github上搜索"internationlization"，能找到很多javascript语言编写的实现多语言化的工具。

最受欢迎的有：

### 1. 基于rails环境的[i18n](http://guides.rubyonrails.org/i18n.html)
Angular制作了相应的库[angular-translater](https://angular-translate.github.io/)，在github上有4000多星。vue也有对应的[vue-i18n](https://kazupon.github.io/vue-i18n/)

 ![]({{site.url}}/images/Snip20170102_6.png)
 
 i18n是Internationalization and localization的缩写，wikipedia讲解[Internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization)时提到：

 >The terms are frequently abbreviated to the numeronyms i18n (where 18 stands for the number of letters between the first i and the last n in the word internationalization, a usage coined at DEC in the 1970s or 80s) and L10n for localization, due to the length of the words.
 
### 2. yahoo出品的[format.js](http://formatjs.io/)
支持React, Ember框架，react对应的[react-intl](https://github.com/yahoo/react-intl)有3700多星。

 ![]({{site.url}}/images/Snip20170102_3.png)
 
### 3. 支持几乎所有主流框架的[i18next](http://i18next.com/)
有1800多星。

 ![]({{site.url}}/images/Snip20170102_5.png)
