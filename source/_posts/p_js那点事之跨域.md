---
title: js那点事系列:跨域
date: 2014-03-18 13:20:19
categories:
- 编程
tags:
- js
---










### 可以的请求资源的方法
- ajax
- form
- iframe/frameset(忽略)
- img
- script
- link

### 存在跨域限制的方法
- ajax
 > 完全限制:不同域名的资源不能访问
- iframe
 > 部分限制:可以请求不同域资源,但是其父页面不能访问到子页面窗口对象。