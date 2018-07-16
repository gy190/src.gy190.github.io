---
title: PostMan实用技巧
date: 2017-04-23 19:20:29
keywords: postman使用技巧
categories:
- 编程
tags:
- httpclient
---

本文仅列出实用但是容易被忽略的使用方法。不涉及基本用法、Built-in Tools用法（mock, debug, test、monitor,etc.）和收费功能。

### Collections
- 说明：文件夹功能
- 场景：将不同的接口分类。

### Environment  
- 说明：环境变量
- 场景：动态ip；接口有多种测试环境，不同环境ip不同；全局参数。
    
### Presets
- 说明：请求头（headers）预设值，类似环境变量功能
    
### 导出（免费功能只能导出Collections）  
- export：导出json文件
- get Link  
        生成一个连接，其他人通过该链接可以直接导入你的文件夹。

### 导入
- import File  
    将上文导出的json文件导入

- import From Link  
    导入上文生成的连接
    
- Paste Raw Text （非常实用）
	- 说明：导入curl请求文本
	- 场景：可方便将浏览器里的请求导入到postman。（打开浏览器network，在请求上点击右键->copy->copy as curl）
        
### Bulk Edit  
  批量编辑，基本上所有配置都有此功能。

### code  
  集成了多种语言发送http请求的基本代码实现。

### interceptor  
    拦截浏览器请求。需要安装chorome 扩展和chrome app版postman。 （桌面版postman貌似没有此功能，直接使用Paste Raw Text就可以了。）

### 注册postman账户并登录  
  有的功能需要登录才能使用，如登陆后，可以同步文件夹和环境变量。
  
## 图示
 
