---
title: 前端工作总结
date: 
categories:
- 编程
tags:
- js
---

- web是由javascript、css和html构成的
 js负责页面逻辑  html负责页面结构 css负责页面样式

 - 那这三种web语言是如何关联到一起的？
 - 通过html，在html中调用js和css文件。
 - 进一步能够知道浏览器访问页面时，是以html文件为入口访问的，即先请求html文件，对其解析，然后请求
 html文件里调用的js和css文件
 - 清楚浏览器加载的流程，就能知道不能对html文件设置缓存。因为它乃入口。
 
 
## 工程化

## 模块化

基本功能：

很多朋友觉得学习框架成本很高，其实只要掌握要点，也没有多难，那如何学习一个新js框架呢：
以具体的业务功能为线索去学习新框架。
基础：
dom操作：
绑定事件：
事件委托
数据
进阶：如何实现组件、应用组件。 组件的嵌套。 组件的通信（同级通信、嵌套通信）

如何操纵dom、如何绑定事件、如何实现组件、组件间如何通信


面临的实际问题：
promise该什么时候用，该怎么用
轮播图插件
日历插件
图片懒加载
瀑布流
布局