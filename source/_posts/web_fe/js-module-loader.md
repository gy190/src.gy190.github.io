---
title: 轻量js模块加载器实现及思路分析
date: 
categories:
- 编程
tags:
- js
---

实现轻量的模块加载器。构成：
```
//没有id。 前置依赖模块解析。 回调函数。
define([], function(require, export) {
    // something
})
```

分析：
- 引用加载模块：递归分析
- 导出模块：
- 定义模块：define，用于形成封闭的作用于空间，防止变量冲突。 用于前置加载依赖。
- 路径分析：获取当前执行文件的路径、依赖模块的路径分析、绝对/相对路径的转换
- 模块唯一识别id：使用绝对路径作为id
- 模块缓存

```
window.Loader = {};
Loader.Require = function(contentModulePath) {
    var require = function() { //require都在模块体内被调用
     //路径处理
     //从缓存中获取模块
    }
    return require;
}

//define在模块文件加载完成后立即调用
Loader.define = function(deps, callback) {
    //分析依赖，处理依赖路径
    //从缓存中获取依赖，如果缓存没有则加载依赖
    //将新加载的依赖放入缓存
    //所有依赖加载完成后，执行callback
}
Loader.loadScript = function() {}
Loader.path = {

}

```


参考：http://www.jianshu.com/p/09ffac7a3b2c
