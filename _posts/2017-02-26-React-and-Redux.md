---
layout: post
title: 'React & Redux'
---



> We built React to solve one problem: **building large applications with data that changes over time**.——[Why React ?](http://reactjs.cn/react/docs/why-react.html)

React用于制作web单页应用，界面由React渲染出来，并且实现组件化，组件具有Declarative特点。

但是，

> 随着 JavaScript 单页应用开发日趋复杂，**JavaScript 需要管理比任何时候都要多的 state （状态）**。 
>
> 管理不断变化的 state 非常困难。如果一个 model 的变化会引起另一个 model 变化，那么当 view 变化时，就可能引起对应 model 以及另一个 model 的变化，依次地，可能会引起另一个 view 的变化。直至你搞不清楚到底发生了什么。——[动机](http://cn.redux.js.org/docs/introduction/Motivation.html)

Redux就是用于解决state管理的问题。将所有数据都存在store中，view和store一一对应，view由store和mapStateToProps()决定。store存有所有的数据，mapStateToProps()决定如何显示这些数据。

> **惟一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象。**

action对应的store的更改方式由reducer决定，store由reducer和initialDate生成。

就像之前看别人解释的：

store就像一个银行，不仅存着钱，还有服务人员根据你的需求对金额进行更改。我们不能直接对金额进行操作。

通过mapDispatchToProps()向presentational components传递dispatch(action)，使用户的操作能够对store进行更改。

综上，实现严格的单向数据流。

目前我对于单一数据源的好处我能理解，但关于对store的更改统一的作用还不是很能理解。

最近发现用React的网站还挺多的，豆瓣和知乎都用了。