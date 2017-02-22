---
layout: post
title: 'React Server Render'
---

### 为什么要Server Render

一个完全用React制作的网站，如果不Server Render，发给浏览器的html文件的DOM将是空的，virtual DOM都在bundle.js里，需要浏览器运行bundle.js才能渲染出完整的DOM。

不server render有两个坏处：

- 不利于SEO，搜索引擎只能检索html文件，而不能检索js文件
- 影响网站访问性能，相比静态页面多了本地render的时间，和发起ajax请求的时间。当然，用server render也需要在浏览器发出请求后，在服务器端render一遍然后发给浏览器，仍然会造成一定延迟，除非页面不是实时render。

如果不server render，当页面需要数据时，一般是先给react组件的state设置为一个空数据，然后在componentDidMount里，通过ajax请求获取到数据，并用回调函数将state设置为获取的数据，react监测到state改变，会进行重新render。之所以先设置空数据，是为了避免ajax请求阻碍页面第一次的渲染。

### Server Render的两种改进方案

但是在server render中仍然用这种方法，会造成一些浪费。因为服务器在服务器端render好后将完整的html文件和bundle.js发给浏览器，但是react会接管整个页面，并将整个页面重新render一遍。这是不需要的，因为已经有完整的页面了。这造成了两个浪费，一是多了一次不必要的ajax请求，二是浏览器多了两次不必要的render。对用户体验带来的影响就是页面“空白”了一会儿。

解决办法是

1. **先解决空白的问题。**除去给react组件传空数据的环节，直接进行ajax请求，然后进行渲染。因为已经有完整的页面了，不需要担心ajax请求阻碍页面的第一次渲染的问题。这样可以减少一次数据为空的渲染，不会造成页面空白的结果，整个ajax请求的过程在后台进行，对页面不会造成任何影响。而且用ajax请求获得的数据得到的virtual DOM和当前页面的DOM一样，React并不会重新渲染，因为React只会渲染改变的部分。但还是有一次不必要的ajax请求。
2. **要避免这次ajax请求**，server可以不仅给broswer发送渲染后的完整html，还发送要用到的数据，数据放在window.initialData对象里。React组件直接调用window.initialData对象里的数据，从而避免发起ajax请求。和上面的方法一样，React会发现virtual DOM和真实的DOM一样，从而不会进行重新渲染。这样就避免了这不必要的ajax请求。

但是，React调用数据产生virtual DOM和server render产生的DOM进行Diff运算，这个环节是无法避免的。因为React要保证有一个virtual DOM在内存中。

### BTW

提升网站访问性能可以从三方面入手：

- 服务器架构
- 浏览器带宽
- 代码的设计

这里是从最后一个方面入手。