---
layout: post
title: "WebSocket在小程序中的应用"
---

## 为什么要使用WebSocket？

在对实时性要求比较高的场景，传统的HTTP轮询和长连接无法满足需求。

> 使用传统的 HTTP 轮询或者长连接的方式也可以实现类似服务器推送的效果，但是这类方式都存在资源消耗过大或推送延迟等问题。而 WebSocket 直接使用 TCP 连接保持全双工的传输，可以有效地减少连接的建立，实现真正的服务器通信，对于有低延迟有要求的应用是一个很好的选择。
>
> (source:http://www.henkuai.com/thread-15152-1-1.html)

另外，传统的办法服务器只能响应客户端的数据请求。

> Most web applications currently operate by simply responding to user interaction. You click a button, called “Next”, and this causes the browser to fetch the next data set, and then render that to the page. This is great, but it’s still a very limiting model.
>
> (source:https://lostechies.com/chrismissal/2013/08/06/browser-wars-websockets-vs-ajax/)

而WebSocket实现了持久连接，服务器不再只能等待客户端发起请求，而是可以主动推送信息给客户端。

> Because the connection is persistent, the *server* can now *initiate communication with the browser*. 
>
> (source:https://lostechies.com/chrismissal/2013/08/06/browser-wars-websockets-vs-ajax/)

总之，WebSockets就是为了在浏览器和服务器之间创建低延迟的、双向的、全双工的、持久的连接。

> The purpose of WebSockets is to provide a low-latency, bi-directional, full-duplex and long-running connection between a browser and server. 
>
> (source:http://stackoverflow.com/questions/10377384/why-use-ajax-when-websockets-is-available)

其他的都好理解，那全双工(full-duplex)是什么呢？就是可以两个方向同时传输数据。

> Refers to the transmission of data in two directions simultaneously.
>
> (source:www.webopedia.com/TERM/F/full_duplex.html)

## WebSocket的定义

> WebSocket protocol 是HTML5一种新的协议。它实现了浏览器与服务器全双工通信(full-duplex)。一开始的握手需要借助HTTP请求完成。
>
> (source:http://baike.baidu.com/item/WebSocket)

> **WebSocket** is a computer [communications protocol](https://en.m.wikipedia.org/wiki/Communications_protocol), providing [full-duplex](https://en.m.wikipedia.org/wiki/Full-duplex) communication channels over a single [TCP](https://en.m.wikipedia.org/wiki/Transmission_Control_Protocol) connection. The WebSocket protocol was standardized by the [IETF](https://en.m.wikipedia.org/wiki/Internet_Engineering_Task_Force) as [RFC](https://en.m.wikipedia.org/wiki/Request_for_Comments) 6455 in 2011, and the WebSocket [API](https://en.m.wikipedia.org/wiki/Application_programming_interface) in [Web IDL](https://en.m.wikipedia.org/wiki/Web_IDL) is being standardized by the [W3C](https://en.m.wikipedia.org/wiki/World_Wide_Web_Consortium).
>
> (source:https://en.m.wikipedia.org/wiki/WebSocket)

## WebRTC vs. WebSocket

与WebSocket协议类似的还有Google开发的Web RTC协议，主要区别在于：Web RTC主要是浏览器和浏览器之间通信，而WebSocket在浏览器中间必须要服务器参与。

当然WebRTC还是需要服务器将服务器连接起来的：

> WebRTC使用RTCPeerConnection来在浏览器之间传递流数据，这个流数据通道是点对点的，不需要经过服务器进行中转。但是这并不意味着我们能抛弃服务器，我们仍然需要它来为我们传递信令（signaling）来建立这个信道。WebRTC没有定义用于建立信道的信令的协议：信令并不是RTCPeerConnection API的一部分
>
> (source:https://segmentfault.com/a/1190000000436544)

两者的区别主要就是服务器的参与度：

> **WebRTC**
>
> WebRTC is designed for high-performance, high quality communication of video, audio and arbitrary data. In other words, for apps exactly like what you describe.
>
> WebRTC apps need a service via which they can exchange network and media metadata, a process known as signaling. However, once signaling has taken place, video/audio/data is streamed directly between clients, avoiding the performance cost of streaming via an intermediary server.
>
> **WebSocket**
>
> WebSocket on the other hand is designed for bi-directional communication between client and server. It is possible to stream audio and video over WebSocket (see [here](http://stackoverflow.com/questions/4241992/video-streaming-over-websockets-using-javascript) for example), but the technology and APIs are not inherently designed for efficient, robust streaming in the way that WebRTC is.
>
> (source:http://stackoverflow.com/questions/18799364/webrtc-vs-websockets-if-webrtc-can-do-video-audio-and-data-why-do-i-need-web)

WebSocket相比WebRTC性能要差一些，**但小程序只支持WebSocket。**

## 框架

基于WebSocket协议有著名的Socket.io, Tornado框架。

|              | Socket.io         | Tornado                    |
| ------------ | ----------------- | -------------------------- |
| 语言           | Node.js           | Python                     |
| Github stars | 30k               | 13k                        |
| 官网           | http://socket.io/ | http://www.tornadoweb.org/ |

Socket.io需要包括分别运行在服务器和浏览器的两部分：

> **Socket.IO** 
>
> is a [JavaScript](https://en.m.wikipedia.org/wiki/JavaScript) library for realtime [web applications](https://en.m.wikipedia.org/wiki/Web_application). It enables realtime, bi-directional communication between web clients and servers. It has two parts: a [client-side](https://en.m.wikipedia.org/wiki/Client-side) library that runs in the [browser](https://en.m.wikipedia.org/wiki/Web_browser), and a [server-side](https://en.m.wikipedia.org/wiki/Server-side) library for [Node.js](https://en.m.wikipedia.org/wiki/Node.js). Both components have a nearly identical [API](https://en.m.wikipedia.org/wiki/Application_programming_interface). Like Node.js, it is [event-driven](https://en.m.wikipedia.org/wiki/Event-driven_architecture).
>
> (source:https://en.m.wikipedia.org/wiki/Socket.IO)

> **Tornado** 
>
> is a Python web framework and asynchronous networking library, originally developed at [FriendFeed](http://friendfeed.com/). By using non-blocking network I/O, Tornado can scale to tens of thousands of open connections, making it ideal for [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_Polling), [WebSockets](http://en.wikipedia.org/wiki/WebSocket), and other applications that require a long-lived connection to each user.
>
> (source:https://github.com/tornadoweb/tornado)