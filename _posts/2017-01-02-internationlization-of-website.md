---
layout: post
title: "网站的国际化（支持多语言）"
---

## 支持多语言的重要性
全世界有很多语言，在互联网上使用人数超过一亿的语言有7种。

![]({{site.url}}/images/most_used_languages_on_the_internet_2015.png)

虽然中国人口数量很大，很多网站仅仅面向国内就能保证自己的生存，但是在21世纪我们必须要国际化视野。正如吴军老师说的：

>中国人现在有两门课要学：国际化 和 资本

在中国以外的地方还有更加广阔的天地。

![]({{site.url}}/images/the_world_online.png)

要让网站面向全世界，就必须实现网站的多语言化。

## 技术上的方法
在github上搜索internationlization，能找到很多用javascript语言编写的用语实现多语言的库。

最为广泛使用的有：

### 基于rails环境的[i18n](http://guides.rubyonrails.org/i18n.html)
Angular制作了相应的库[angular-translater](https://angular-translate.github.io/)，在github上有4000多星。vue也有对应的[vue-i18n](https://kazupon.github.io/vue-i18n/)

 ![]({{site.url}}/images/Snip20170102_6.png)
 
 i18n是Internationalization and localization的缩写，wikipedia讲解[Internationalization and localization](https://en.wikipedia.org/wiki/Internationalization_and_localization)时提到：

 >The terms are frequently abbreviated to the numeronyms i18n (where 18 stands for the number of letters between the first i and the last n in the word internationalization, a usage coined at DEC in the 1970s or 80s) and L10n for localization, due to the length of the words.
 
### yahoo出品的[format.js](http://formatjs.io/)
支持React, Ember框架，react对应的[react-intl](https://github.com/yahoo/react-intl)有3700多星。

 ![]({{site.url}}/images/Snip20170102_3.png)
 
### 支持几乎所有主流框架的[i18next](http://i18next.com/)
有1800多星。

 ![]({{site.url}}/images/Snip20170102_5.png)
