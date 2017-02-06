---
layout: post
title: 'React Server Render'
---

如果不Server Render好，发给浏览器的html文件的DOM是空的，virtual DOM都在bundle.js里，需要浏览器运行bundle.js才能render出真实的DOM。

这样有两个坏处：

- 不利于SEO，搜索引擎只能搜索到DOM，而不能搜索js文件
- 稍有影响网站访问性能，相比静态页面多了本地render的时间，但这影响不大，因为用server render也需要在浏览器发出请求后，在服务器端render一遍然后发给浏览器，除非页面不是实时render

如果不server render，当页面需要数据时，一般是先给react组件的state设置为一个空数据，然后在componentDidMount里，通过ajax请求获取到数据，并用回调函数讲state设置为获取的数据，react监测到state改变，会进行重新render。之所以先设置空数据，是为了避免ajax请求阻碍页面的渲染。

但是在server render中仍然用这种方法，会造成一些浪费。因为服务器在服务器端render好后将完整的html文件和bundle.js发给浏览器，但是react会将上面的过程又过一遍。这是不需要的，因为已经有完整的页面了。这造成两个浪费，一是多了一次不必要的ajax请求，而是浏览器多了两次不必要的render。

解决办法是，除去给react组件传空数据的环节，直接进行ajax请求，然后进行渲染。这样可以减少一次组件数据为空的一次渲染。但是仍然有不必要的ajax请求。

去除多余的ajax请求的办法是，server给broswer不仅传递渲染后的DOM，而且还传递要用到的数据，数据放在window.initialData对象里。React组件直接调用window.initialData对象里的数据，而不是通过发起ajax请求获得，然后发现virtual DOM和页面真实的DOM一样，就不会进行重新渲染了。这样减少了不必要的ajax请求和一次渲染。

综上，Server Render有利于SEO和提高网站访问性能。