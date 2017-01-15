---
layout: post
title: "小程序开发框架的应用"
---

## 小程序开发框架

开发小程序需要用也只能用“小程序开发框架”，框架提供了自己的视图层描述语言 WXML 和 WXSS，以及基于 JavaScript 的逻辑层框架，并在视图层与逻辑层间提供了数据传输和事件系统。语法和html, css, js基本一致，用到了响应式的数据绑定，和Vue类似，当做数据修改的时候，只需要在逻辑层修改数据，视图层就会做相应的更新，总体来说开发很方便。

另外，框架提供了一些微信风格的组件和微信原生的API。

框架设定好了一些规则（比如设置导航栏的颜色和文字），我们按照这些规则进行编写可以实现对应的效果，而不需要理解背后的实现方法，从而降低编写的难度。

## 目录结构

编写过程中主要需要关注的文件包括/pages目录和	app.js, app.json, app.wxss文件。所有页面的文件都放在/pages目录下，每个页面包括完整的`.wxml`, `.wxss`, `.js`, `.json`文件。

`.js`后缀的是脚本文件，`.json`后缀的文件是配置文件，`.wxss`后缀的是样式表文件。

#### [app.js](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/app-service/app.html?t=2017112)

> app.js是小程序的脚本代码，用于注册一个小程序。我们可以在这个文件中监听并处理小程序的生命周期函数、声明全局变量。

大概意思就是打开一个小程序，并将相关的代码载入。整个文件的代码写在`App()`函数内，而且`App()` 必须在 `app.js` 中注册，且不能注册多个。

```javascript
//app.js
App({
  onLaunch: function () {
    //调用API从本地缓存中获取数据
    var logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)
  },
  getUserInfo:function(cb){
    var that = this;
    if(this.globalData.userInfo){
      typeof cb == "function" && cb(this.globalData.userInfo)
    }else{
      //调用登录接口
      wx.login({
        success: function () {
          wx.getUserInfo({
            success: function (res) {
              that.globalData.userInfo = res.userInfo;
              typeof cb == "function" && cb(that.globalData.userInfo)
            }
          })
        }
      });
    }
  },
  globalData:{
    userInfo:null
  }
})
```

onLaunch是生命周期函数中的一种，小程序一打开就会调用对应的定义的函数。

| 属性       | 类型       | 描述               | 触发时机                                     |
| -------- | -------- | ---------------- | ---------------------------------------- |
| onLaunch | Function | 生命周期函数--监听小程序初始化 | 当小程序初始化完成时，会触发 onLaunch（全局只触发一次）         |
| onShow   | Function | 生命周期函数--监听小程序显示  | 当小程序启动，或从后台进入前台显示，会触发 onShow             |
| onHide   | Function | 生命周期函数--监听小程序隐藏  | 当小程序从前台进入后台，会触发 onHide                   |
| onError  | Function | 错误监听函数           | 当小程序发生脚本错误，或者 api 调用失败时，会触发 onError 并带上错误信息 |
| 其他       | Any      |                  | 开发者可以添加任意的函数或数据到 Object 参数中，用 `this` 可以访问 |

#### [Page.js](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/app-service/page.html)

每个页面也需要注册，使用`Page()` 函数用来注册一个页面。接受一个 object 参数，用来指定页面的初始数据、生命周期函数、事件处理函数等。

**object 参数说明：**

| 属性                                       | 类型       | 描述                                       |
| ---------------------------------------- | -------- | ---------------------------------------- |
| [data](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/app-service/page.html#初始化数据) | Object   | 页面的初始数据                                  |
| onLoad                                   | Function | 生命周期函数--监听页面加载                           |
| onReady                                  | Function | 生命周期函数--监听页面初次渲染完成                       |
| onShow                                   | Function | 生命周期函数--监听页面显示                           |
| onHide                                   | Function | 生命周期函数--监听页面隐藏                           |
| onUnload                                 | Function | 生命周期函数--监听页面卸载                           |
| onPullDownRefresh                        | Function | 页面相关事件处理函数--监听用户下拉动作                     |
| onReachBottom                            | Function | 页面上拉触底事件的处理函数                            |
| onShareAppMessage                        | Function | 用户点击右上角分享                                |
| 其他                                       | Any      | 开发者可以添加任意的函数或数据到 object 参数中，在页面的函数中用 `this` 可以访问 |

```javascript
//index.js
Page({
  data: {
    text: "This is page data."
  },
  onLoad: function(options) {
    // Do some initialize when page load.
  },
  onReady: function() {
    // Do something when page ready.
  },
  onShow: function() {
    // Do something when page show.
  },
  onHide: function() {
    // Do something when page hide.
  },
  onUnload: function() {
    // Do something when page close.
  },
  onPullDownRefresh: function() {
    // Do something when pull down.
  },
  onReachBottom: function() {
    // Do something when page reach bottom.
  },
  onShareAppMessage: function () {
   // return custom share data when user share.
  },
  // Event handler.
  viewTap: function() {
    this.setData({
      text: 'Set some data for updating view.'
    })
  },
  customData: {
    hi: 'MINA'
  }
})
```

#### app.json

> app.json 是对整个小程序的全局配置。我们可以在这个文件中配置小程序是由哪些页面组成，配置小程序的窗口背景色，配置导航条样式，配置默认标题。注意该文件不可添加任何注释。

```json
{
  "pages": [
    "pages/index/index",
    "pages/logs/index"
  ],
  "window": {
    "navigationBarTitleText": "Demo"
  },
  "tabBar": {
    "list": [{
      "pagePath": "pages/index/index",
      "text": "首页"
    }, {
      "pagePath": "pages/logs/logs",
      "text": "日志"
    }]
  },
  "networkTimeout": {
    "request": 10000,
    "downloadFile": 10000
  },
  "debug": true
}
```

app.json 配置项列表：

| 属性                                       | 类型           | 必填   | 描述              |
| ---------------------------------------- | ------------ | ---- | --------------- |
| [pages](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html#pages) | String Array | 是    | 设置页面路径          |
| [window](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html#window) | Object       | 否    | 设置默认页面的窗口表现     |
| [tabBar](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html#tabbar) | Object       | 否    | 设置底部 tab 的表现    |
| [networkTimeout](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html#networktimeout) | Object       | 否    | 设置网络超时时间        |
| [debug](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html#debug) | Boolean      | 否    | 设置是否开启 debug 模式 |

#### page.json

页面的配置比`app.json`全局配置简单得多，只是设置 app.json 中的 window 配置项的内容，页面中配置项会覆盖 app.json 的 window 中相同的配置项。页面的`.json`只能设置 `window` 相关的配置项，以决定本页面的窗口表现，所以无需写 `window` 这个键，如：

| 属性                           | 类型       | 默认值     | 描述                                       |
| ---------------------------- | -------- | ------- | ---------------------------------------- |
| navigationBarBackgroundColor | HexColor | #000000 | 导航栏背景颜色，如"#000000"                       |
| navigationBarTextStyle       | String   | white   | 导航栏标题颜色，仅支持 black/white                  |
| navigationBarTitleText       | String   |         | 导航栏标题文字内容                                |
| backgroundColor              | HexColor | #ffffff | 窗口的背景色                                   |
| backgroundTextStyle          | String   | dark    | 下拉背景字体、loading 图的样式，仅支持 dark/light       |
| enablePullDownRefresh        | Boolean  | false   | 是否开启下拉刷新，详见[页面相关事件处理函数](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/app-service/page.html?t=2017112#页面相关事件处理函数)。 |
| disableScroll                | Boolean  | false   | 设置为 true 则页面整体不能上下滚动；只在 page.json 中有效，无法在 app.json 中设置该项 |

## [事件](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxml/event.html)

- 事件是视图层到逻辑层的通讯方式。
- 事件可以将用户的行为反馈到逻辑层进行处理。
- 事件可以绑定在组件上，当达到触发事件，就会执行逻辑层中对应的事件处理函数。
- 事件对象可以携带额外信息，如 id, dataset, touches。

#### 事件类型

| 类型          | 触发条件               |
| ----------- | ------------------ |
| touchstart  | 手指触摸动作开始           |
| touchmove   | 手指触摸后移动            |
| touchcancel | 手指触摸动作被打断，如来电提醒，弹窗 |
| touchend    | 手指触摸动作结束           |
| tap         | 手指触摸后马上离开          |
| longtap     | 手指触摸后，超过350ms再离开   |

#### 事件绑定

事件绑定的写法同组件的属性，以 key、value 的形式。

- key 以`bind`或`catch`开头，然后跟上事件的类型，如`bindtap`, `catchtouchstart`
- value 是一个字符串，需要在对应的 Page 中定义同名的函数。不然当触发事件的时候会报错。

`bind`事件绑定不会阻止冒泡事件向上冒泡，`catch`事件绑定可以阻止冒泡事件向上冒泡。

#### 使用事件的方式

- 在组件中绑定一个事件处理函数。

如`bindtap`，当用户点击该组件的时候会在该页面对应的Page中找到相应的事件处理函数。

```html
<view id="tapTest" data-hi="WeChat" bindtap="tapName"> Click me! </view>
```

- 在相应的Page定义中写上相应的事件处理函数，参数是event。

```javascript
Page({
  tapName: function(event) {
    console.log(event)
  }
})
```