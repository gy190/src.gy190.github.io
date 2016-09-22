---
title: js那点事系列:跨域
date: 2014-03-18 13:20:19
categories:
- 编程
tags:
- js
---

## 已知的请求资源的方法
- ajax
- form
- iframe/frameset(忽略)
- img
- script
- link

## 存在跨域限制的方法
- ajax
 > 完全限制:不同域名的资源不能访问
- iframe
 > 部分限制:可以请求不同域资源,但是其父页面不能访问到子页面窗口对象。

## 问题本质
 1、跨域限制是由于浏览器基于安全考虑而产生的策略,所以只能通过hack的方式去解决。
 2、跨域问题不能单方面解决。需要两端配合。

## 无刷新请求异域接口数据的跨域问题解决方案
- CROS
    - 优点:简单快捷
    - 缺点:安全性问题;ie8、9兼容不好
- 代理服务器
    - 优点:直接避免了跨域的问题
    - 缺点:复杂;多了一层服务,需要额外的维护成本和安全成本。
- jsonp
    - 优点:简单快捷
    - 缺点:只能get方式;需要修改后端接口实现
- form + iframe
    - 优点: 可以post方式请求
    - 缺点: 相对复杂
    
### 使用form + iframe跨域的实现步骤  
- **方式一:通过querystring获取异域接口响应的数据**
    1. 接口(异域)请求页面中,js动态创建form表单,异域接口通过form表单提交进行请求(form提交没有跨域限制)。同时form表单的target属性为页面里一个隐藏的用于接收接口数据的iframe标签。
    2. 本域服务器上创建一个cross.html页面,用于给异域接口返回数据用。
    3. 异域接口接收到请求后,使用302重定向到与接口请求页面同域的cross.html页面,并将响应的数据作为querystring放在url后面。
    4. 由于cross.html和当前接口请求页面是同域的,所以js可以直接获取iframe的window对象,通过location.search获取上步骤中接口写在url后面的querystring数据。
- **方式二:通过window.name获得异域接口响应的数据**
    1. 接口(异域)请求页面中,js动态创建form表单,异域接口通过form表单提交进行请求(form提交没有跨域限制)。同时form表单的target属性为页面里一个隐藏的用于接收接口数据的iframe标签。
    2. 异域接口所在服务器上创建cross.html页面,异域接口接收到请求后,使用302重定向到与接口同域的cross.html页面,页面里使用模板,响应的数据通过模板脚本填充,最终赋给window.name。
    3. 由于cross.html和请求页面存在跨域,请求页面服务器上需要创建proxy.html页面,请求页面中js动态的将步骤1中的iframe的src属性值改成同域的proxy.html
    4. window.name的特性————相同窗口容器中(iframe就是一个窗口容器),通过js脚本跳转切换的页面,仅有一个全局的window.name属性,也就是说无论窗口中页面如何跳转,window.name都会被共享。
    5. 基于window.name的特性,当iframe的src被只想同域名下的页面时,iframe和父页面就可以进行通讯了。伪代码是:var data = frameObject.contentWindow.name;  
- ** 两种方式区别**
    由于querystring有固定长度限制,而window.name长度基于内存。当接口响应数据量大时,用方案二。但是方案二也增加了复杂度,需要两个域都创建额外的hack页面进行数据通信。
    
## iframe跨域,父子页面通信解决方案
 - window.name
 - postMessage:存在兼容问题,移动端优先考虑使用。
 - document.domain:据说可以在不同子域下实现跨域,但本人没有实现成功。
 
 
> *说明: 由于form+iframe的实现方式比较难理解,本文特别解释一下。其他的跨域方案的实现细节请自行搜索 。*