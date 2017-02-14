---
title: 基于前后端分离的开发流程
date: 2014-05-03 08:33:20
categories:
- 编程
tags:
- js
---
本文将讲解前后端分离开发架构与后端渲染的
### 开发流程对比
#### 旧流程:
1、ue:  
**责任**：实现静态页面和样式。  
**调试**：a、不涉及js核心库(g.js)时,本地实时访问调试。b、涉及js核心库,需要上传到测试环境，因为核心库需要php接口返回。c、如果需要使用less等预编译工具,也需要先进行build。  

2、phper:  
**责任**：将ue实现的静态页面改成嵌入php脚本的动态页面、加入js逻辑、实现接口  
**调试**：先build,然后再通过php server看实际修改效果。  

#### 新流程:  
1、ue:  
**责任**：实现静态页面和样式。  
**调试**：无需复杂配置,一条命令启动本地mock-server。所有改动直接通过该mock-server进行查看。在最终开发完成前,无需分发到远程环境预览效果。当然ue如果不用less、ejs,也可以无需使用mock-server。  
2、jser:  
**责任**：将ue实现的静态页加入js逻辑。  
**调试**：无需复杂配置,一条命令启动本地mock-server。所有改动直接通过该mock-server实时查看。  
3、phper:  
**责任**：实现接口  
**调试**：无需关注前端页面  

### mock-server  
**功能**：  
1、根据实际请求实时build资源。无需实时watch本地资源改动,降低能耗。  
2、解决本地环境ajax请求接口跨域的问题。 无需频繁提交、切换环境。  
3、模拟登录,解决本地环境无权限访问需要认证的接口的问题。 无需频繁提交、切换环境。  

**搭建&运行**:  
1、git检出mock-server项目  
2、解压node-module压缩包到项目根目录  
3、修改doumi-config.js里的路径配置,路径指向实际业务项目根目录  
4、运行:node server.js  
5、访问:http://localhost:port/view/xx/xxx.html  //view是实际业务项目里的视图根目录  


### 新旧builder工具对比:  
#### 旧builder:  
1、构建工具:使用grunt。 （慢、配置繁琐）  
2、模块化构建:无。（在实时访问阶段,模块化依赖需要通过js框架完成。）  
3、版本控制:无。 （在实际访问阶段,依赖请求php接口,返回全部资源时间戳作为版本号。）  

#### 新builder  
1、构建工具:gulp。 （快、配置简洁。）  
2、模块化构建:webpack  
3、版本控制:分析资源引用,在文件内插入所引用资源的md5摘要作为版本号。  

> 说明：其他的优化比如压缩混淆合并就不说了，这些是前端构建的必须流程  

### 新开发流程下的前端项目划分及目录结构  
#### 项目划分  
**通用项目**:  
PC版站点通用项目(common_pc)  
WAP版站点通用项目(common_m)  

**业务项目**:  
C端PC版主站项目(c_pc_doumi)  
C端WAP版主站项目(c_m_doumi)  
B端PC版主站项目(vip_pc_doumi)  
B端WAP版主站项目(vip_m_doumi)  


#### 目录结构  
**通用项目目录结构**  
.  
├── com             前端组件目录  
└── lib             js库、框架目录  

**业务项目目录结构**  
.  
├── common(**submodule**)  指向到通用项目  
├── proto_view        ue开发的静态页面存放目录  
├── static  
│   ├── img            ue存放图片的目录  
│   ├── css            ue存放css的目录  
│   ├── less           ue存放less文件的目录  
│   └── js              jser存放业务js文件的目录  
├── view                jser对proto_view里的视图文件修改后的最终html文件存放目录  

>说明:实际开发中,ue只需关注前端业务项目。jser关注通用项目和业务项目。phper无需关注前端项目。  

### seo问题  
建立爬虫服务器spider-server。建立搜索引擎爬虫白名单。在白名单中的爬虫的请求都通过nginx转发到spider-server上。  
spider-sever基本构成:http server + PhantomJS。  
  
对于访问相同的页面：  
- 爬虫请求访问ajax页面返回的html内容截图  
![Alt text](http://git.corp.doumi.com/doumi_browser/doc/raw/master/img/爬虫访问.png)  

- 正常请求访问ajax页面返回的html内容截图  
![Alt text](http://git.corp.doumi.com/doumi_browser/doc/raw/master/img/正常访问.png)  

> 说明：爬虫服务器可以做的事情有很多，比如制定缓存策略，提前把ajax页面渲染出来，提高响应速度。  

### 前端js框架  
pc端：使用avalon + jquery  
wap端：使用vuejs + zepto + fastclik

> 说明：目前主流框架如angular、react、vue等都不支持IE9以下版本浏览器了。所以pc端使用avalon2作为前端组件框架。如果有时间可以对使用的组件框架进行封装，为业务层提供统一的调用方式。  



### 新架构路由走向图  
![Alt text](http://git.corp.doumi.com/doumi_browser/doc/raw/master/img/新架构路由.png)  

> 一段时期内，新旧开发流程会并存。橙色线是旧开发框架对应的线上请求的路由走向。  

### 新开发流程用例图  
![Alt text](http://git.corp.doumi.com/doumi_browser/doc/raw/master/img/新架构用例图.png)  

> 前端开发者只需将完成的源码提交到git。无需关注builder工具。  

### 总结  
新开发架构主要解决了以下问题：  
- 前端本地开发调试不便捷(核心)
- 前端项目结构混乱 
- 前后端分离不能seo
> seo策略因客观原因暂时搁置  
- phper不熟悉js  
- 版本控制不完善  
- 构建阶段不能合并同步依赖的模块为一个文件。