---
title: js实用面试题
date: 2016-5-10 13:12:10
categories:
- 编程
tags:
- js
---
自认为比较经典比较接地气的js面试题。
## 基础题(初中级别)
### 综合
```
function fun() {
	print = function() {console.log(1)}
	return this;
}

fun.print = function(){console.log(2)}

fun.prototype.print = function(){console.log(3)}

var print = function(){console.log(4)}

function print(){console.log(5)};

//写出以下输出的值。并说明原因。
fun.print(); //构造函数成员和对象成员
print(); //变量声明提升。只提升声明，不提升赋值。所以在赋值时函数被覆盖
fun().print(); //全局作用域变量被覆盖
new fun.print(); //运算符优先级
new fun().print() //原型，运算符优先级
```

### 构造一个具有40个元素的数组,数组的元素为50-100之内的随机数。之后对数组进行去重和排序;(算法)
```
var arr = [];

function getRandom(min, max) {
   return min + Math.random()*(max-min)
}

for (var i = 0; i < 100; i++) {
  arr.push(parseInt(getRandom(0,100)))
}


var len = arr.length;
for (var i = 0; i < len - 1; i++) {
  for (var m = 0; m < len - 1 - i; m++) {
    if (arr[m] > arr[m+1]) {
      var tmp = arr[m];
      arr[m] = arr[m + 1];
      arr[m + 1] = tmp;
    }
  }
}

var obj = {};
for (var i =0; i < arr.length; i++) {
	if (obj[arr[i]]) {
		arr.splice(i, 1);
		i--;
	} else {
		obj[arr[i]] = true;
	}
}
console.log(arr)
```

### 事件委托解决了什么问题?

## 经验题(中高级别)
### zepto中,tap事件的作用,为什么不用click?tap存在什么问题,如何解决?

### 用过哪些跨域技术,jsonp有什么短板?

### 用过哪些方法实现过异步编程?
回调、事件监听、发布订阅、promise、yiled、async/wait

### promise解决了回调函数式编程的哪些问题?
return、throw error、callback hell

### 说说对前端工程化的理解?

### 说说组件化的理解?实现过哪些组件?(问个一个组件实际实现的思路,比如图片懒加载)

## 高级题(高级别)
### 如何实现一个前后端分离开发架构