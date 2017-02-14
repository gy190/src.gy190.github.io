---
title: label标签触发两次事件原因及解决方案
date: 2014-10-21 14:10:12
categories:
- 编程
tags:
- js
---

实现复选的时候遇到一个lable问题——当点击label的时候，click事件被执行了两次,导致复选框不能被选上,但是直接点击复选框功能正常。  

demo代码如下：
```html
 　　<div id="wrap">
     　　<input type="checkbox" name="sel" id="sel"/>
     　　<label for="sel">我是labe1l</label>
  　　</div>
  　　<script type="text/javascript">
     　　document.getElementById("wrap").onclick = function(e) {
         　　console.log(e.target);
     　　}
 　　</script>
 ```
### 现象 
在控制台可以发现事件被触发了两次,触发的事件源分别是input和label；  

### 问题产生的必要条件  
1. 监听的是label和input的上层元素click事件  
2. label和input关联（for或者input在label下）  

### 问题产生原因
当点击label标签时，label上click事件触发并冒泡一次，同时因为label**关联**input标签(浏览器内部过程处理),浏览器会触发input的click事件，导致事件再次冒泡

### 解决方案
- 方案1:不使用label标签

- 方案2:只认input，判断事件源为input，具体代码如下：
``` js
    document.getElementById("wrap").onclick = function(e) {
         var ele = e.target;
         if (ele.tagName === 'LABEL') { return; }
         // do something;
    }
```
> 为什么不只认label:因为label是单向关联到input标签上的。即点击label会label和input都会触发。点击在input上,只会触发input

- 方案3:利用两次事件触发间隔的超短的时间差。
```
 var prevTime = 0;
 document.getElementById("wrap").onclick = function(e) {
     var now = +new Date();
     if (now - prevTime < 100) {
         //do something
     } else {
        prevTime = now;
     }
 }
```



