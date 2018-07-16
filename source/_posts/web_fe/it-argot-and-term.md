---
title: 黑话和术语
date: 2017-3-17 10:46:12
categories:
- 编程
tags:
- 综合
---

# WEB前端行话，了解一下！
这是一篇轻松的普适性文章，本文通过对一些出现频率较高或误解较多的前端行话进行解释与总结，希望能够加深大家对前端的认知。

### vanilla JS  
这其实是一个玩笑，历史背景是有个人号称开发出了一个世上最轻量功能最全面的js库叫 vanilla js。当你使用这个库的时候，你发现里面什么也没有。后来vanilla JS就被大家用来代指原生js。
所以把vailla看成是pure或者plain的意思都是可以的。


### 前端工程化  
基于构建平台（webpack/gulp等）和编译器/预处理器（babel、less、post-css等），来建立一套统一高效的开发约束，保证开发流程、技术、工具的规范化、标准化。从而提高开发维护效率。 
 > 注意前端工程化，跟es6和react等语言版本和语言框架没有必然关系。使用原生js、html、css技术，同样可以搭建工程化开发框架。
 
### MVVM （Model-View-ViewModel） 
视图和业务分离，基于数据驱动的前端开发框架。 代表框架有 react 、vue、 angularjs。
和MVC的区别在于 Controller 和 ViewModel。 Controller就是Model和View桥梁及解耦的作用。ViewModel除了有C的作用外，还具有数据驱动（双向绑定）的功能。
 > 其实前端很多新名词都有新瓶装旧酒意味。很多设计思想都是从已有的其他技术上学来的。换个名字多了一层营销的概念，更有利于推广。

### native语言  
系统原生开发语言。多出现在移动端hybird app中，app里的页面既可用native实现也可以用web技术实现。
所在调试app上的bug的时候，要确认是native导致的还是web导致的。如果是native导致的就要
找ios或android开发人员解决，如果web导致的，就要反馈给web开发人员。

### hybird  
混合开发，常见于移动端app开发。指app程序是由native语言和web语言混合实现的。

### H5
html5，狭义指的就是html技术的一个版本。广义来讲，指的是包括HTML(5)、CSS（3）和JavaScript（es6）在内的一套技术组合。
由于h5在2014年才完成标准制定，因此pc端上的早期低版本浏览器对其支持不好，而移动端浏览器出现较晚，对h5支持较好，所以h5技术初期主要在移动端广泛使用。所以也有一部分人会把h5代指为移动端的web页面。

### ES6
全称 ECMAScript6，表示ecma-262标准的第六次变更的意思。官方标准叫法是ECMAScript 2015。  
javascript语言是ecma-262标准的实现。  

### DOM & BOM
DOM是操控html的api。如Document、Event 等  
BOM可理解为控制浏览器的api。  如Navigator、XMLHttpRequest、open、alert等
DOM、BOM是依据的是W3C的标准和浏览器厂商内部标准实现的。    
DOM、DOM和js语言的关系可以简单类比成c++和MFC的关系。就是基于js实现的两个api库。    

### CSS RESET  
由于不同浏览器都会自带的或者共有一些默认样式，这会给开发者造成布局上的困扰。所以需要在样式开头写一些重置样式，来覆盖浏览器的默认样式。
从而达到统一布局的目的。

### polyfill / shim  
指代兼容库，用于实现低版本浏览器并不支持的原生API的代码。
因为web技术标准的更新，总是超前于浏览器实现的。如果要使用新的技术api，就需要引入polyfill来兼容浏览器。

### headless browser  
无头浏览器，即没有GUI的浏览器，可以类比桌面操作系统和命令行操作系统来理解。
headless browser的出现可以帮助实现很多有价值的场景，如web页面的自动ui测试、爬虫、单页应用的seo、截图处理等。

### SPA(Single Page Application）
单页应用，相对于多页应用（MPA）。顾名思义，整个应用只有一个html页面，所有内容的变更都是使用类ajax技术进行替换的。
一般来说，SPA实现的应用会比MAP有更好的用户体验。但会丧失MPA的一些先天优势，如seo、前进后退的处理等。且实现复杂度相对较高。

### PWA(Progressive Web App)
是一种前端开发理念，通过运用一些先进的技术，增强应用程序的功能，如缓存能力、推送能力，提升用户的使用体验。

### callback hell  
回调地狱，指的是异步编程导致代码层层嵌套，不利于维护。解决方案有Promise、generator、async/await。

### shadow DOM  
影子DOM。既指代一种组件封装思想也是指该思想的具体实现。原生html标签里的video和input都是shadow dom，可以通过打开chrome的devtool -> setting -> perferences -> show user agent shadow DOM 查看shadow dom的内部结构。
shadow DOM 对应的一系列api浏览器支持不好。

### mixin  
混入,通俗的讲就是把一个对象的方法和属性拷贝到另一个对象上。 
被mixin的对象存在属性或方法冲突时会根据实际语言特性有不同的解决方案,如覆盖或放到数组里顺序执行。

### Throttle（节流阀）& Debouncing（防抖动）  
都是防止用户频繁的与浏览器交互而导致函数被高频调用。其作用是限制函数的执行周期。  
Throttle 是限定函数一个时间周期内只能被执行一次。  
Debouncing 限定函数两次调用的间隔时间大于某个时间后才会被真正执行。  
常见的应用场景：搜索框的检索请求、文本框的输入校验、添加购物车等。  

### Conf  
除了是配置单词(configuration)的简写。还可以用作会议(conference)的简写。如 CSS Conf。  

### awesome  
指github上的一类仓库。仓库里搜集整理某个技术领域的资料库。囊括了大量的技术方方案（编程语言、平台、框架、库、插件、工具、教程、ide等）。
> [awesome主库](https://github.com/sindresorhus/awesome)




