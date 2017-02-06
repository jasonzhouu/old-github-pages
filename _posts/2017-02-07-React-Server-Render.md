---
layout: post
title: 'React Server Render'
---

如果不Server Render，发给浏览器的html文件的DOM将是空的，virtual DOM都在bundle.js里，需要浏览器运行bundle.js才能渲染出完整的DOM。

不server render有两个坏处：

- 不利于SEO，搜索引擎只能检索html文件，而不能检索js文件
- 影响网站访问性能，相比静态页面多了本地render的时间，和发起ajax请求的时间。当然，用server render也需要在浏览器发出请求后，在服务器端render一遍然后发给浏览器，除非页面不是实时render。

如果不server render，当页面需要数据时，一般是先给react组件的state设置为一个空数据，然后在componentDidMount里，通过ajax请求获取到数据，并用回调函数讲state设置为获取的数据，react监测到state改变，会进行重新render。之所以先设置空数据，是为了避免ajax请求阻碍页面的渲染。

但是在server render中仍然用这种方法，会造成一些浪费。因为服务器在服务器端render好后将完整的html文件和bundle.js发给浏览器，但是react会将上面的过程又过一遍。这是不需要的，因为已经有完整的页面了。这造成了两个浪费，一是多了一次不必要的ajax请求，二是浏览器多了两次不必要的render。

解决办法是，除去给react组件传空数据的环节，而直接进行ajax请求，然后进行渲染。这样可以减少一次组件数据为空的一次渲染。但是仍然有不必要的ajax请求。因为已经有完整的页面了，不需要担心ajax请求阻碍页面渲染的问题，整个ajax请求的过程都是在后台进行。

而去除多余的ajax请求的办法是，server给broswer不仅传递渲染后的完整html，还传递要用到的数据，数据放在window.initialData对象里。React组件直接调用window.initialData对象，避免发起ajax请求。React会发现virtual DOM和页面真实的DOM一样，就不会进行重新渲染了。这样减少了不必要的ajax请求和一次渲染。

综上，Server Render有利于SEO和提高网站访问性能。