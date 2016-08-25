---
title: js知识点拾遗
date: 2014-08-17 21:08:14
categories:
- 编程
tags:
- js
---
1. 使用 JSON.parse(str)  字符串里的key必须用双引号括起来（不能用单引号）
2. 为dom添加相同属性相同，值不同的class时，好的习惯是先清除在添加。
 class加载的顺序是按照样式表里从上到下的顺序。下面的将覆盖上面的。而不是按照添加class的先后顺序。 
3. onscroll
事件在ios滚动过程中，只在滚动结束时触发一次。（ucweb也是这样）
兼容的连续触发事件只有touchmove事件 

4. form表单action属性为空时，提交表单操作向当前页面链接提交请求
可以用于登陆页面

5. 模拟触发事件
被委托的事件，在安卓中可以模拟触发该事件。 在ios中不可以。其他平台没有设置，所以把不要模拟触发委托的事件。

6. 连续执行href
window.location.href = "http://www.baidu.com";
window.location.href = "http://www.sina.com";
上面两行代码同时出现，大家都知道第二行肯定执行不了。
但是href的值为非跳转性的连接呢，如 meilishuo://setTitle.meilishuo ，这个连接是app协议，告诉app设置一个标题，并不会转向。
此时如果是下面俩行内容
window.location.href = "meilishuo://setTitle.meilishuo";
window.location.href = "meilishuo://openUrl.meilishuo";
则第二行代码不会被执行，应该下面这样写：
window.location.href = "meilishuo://setTitle.meilishuo";
setTimeout(function(){window.location.href = "meilishuo://openUrl.meilishuo"},300);
注意一下href的原理。

7. 当遇到标签兼容行问题时（某些手机好使，某些不好使），首先要想到是不是标签内的某些属性导致的问题
比如：a标签的target属性，当target的值为_blank时，某些app（美丽说）会直接让a标签失效


