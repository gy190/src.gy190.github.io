---
title: js那点事系列:原型、原型链、继承
date: 2014-05-03 08:33:20
categories:
- 编程
tags:
- js
---
本文将详细的分析js继承原理  
## 一些结论
- 构造函数、用new创建的对象、对象字面量都是实例
- 实例上默认存在__proto__属性,该属性指向生成它的构造函数上的prototype对象。
- 有且仅有构造函数有prototype属性,该属性是一个对象字面量
- prototype只跟其构造函数生成的实例有关系。prototype里的__proto__默认指向Object.prototype。
- 因为prototype是一个实例,所以它本身必然有一个__proto__属性。并且默认指向Object.prototype
- Object.prototype.__proto__ 为null,是链子的顶端。
- 实例上的属性查找机制:先搜索实例上是否有访问的属性,如果没查到,则继续从实例属性__proto__里进行查找,如果__proto__里没有,则继续进入到__proto__里的__proto__进行查找,
直到查到请求的数据,或已经查到最高层Object.prototype.__proto__ 直接返回null。
- 根据属性查询机制和prototype、__proto__特性可以实现原型式继承。
- Function和Object是两个特殊的根构造函数——**Function和Object构成一个封闭的环**;Object是Function的实例,Object.__proto__指向Function.prototype,Fucntion是Function(自己是自己的)的实例。Function.__proto__指向自己的
Function.prototype,Function.prototype.__proto__指向Object.prototype。


## js实现继承的要素
- 构造函数(方法/类)
1. 使用function构建的代码块都是构造函数
2. Function是根构造函数,所有其他的构造函数都是该函数的实例。如Object, Array,Math,自定义函数等
```
console.log(Object instanceof Function); //true
console.log(Object.__proto__ == Function.prototype)
console.log(Array instanceof Function); //true
function A() {}
console.log(A instanceof Function); //true
```
3. Function也是实例,但它是它自己的实例
```
console.log(Function.__proto__ == Function.prototype) //true 默认只有Function具有这一特性
```
4. 其它实例的__proto__都指向该实例的构造函数上的prototype对象
```
console.log(Array.__proto__ == Function.prototype) //true 原生构造函数是Function实例

function A() {}
console.log(A.__proto__ == Function.prototype) //ture 自定义构造函数是Function实例

var a = new A(); 
console.log(a.__proto__ == A.prototype) //true
```
5. 方法是一个特殊的实例,是Function函数的实例
```
function A() {}
console.log(A instanceof Function) //true
```
6. 方法上默认会有一个prototype属性,该属性里的属性/方法被该方法的所有实例共享
```
function A() {}
A.prototype.o = {m : 10}
var a1 = new A();
var a2 = new A();
console.log(a1.__proto__ == a2.__proto__) //true
console.log(a2.__proto__ == A.prototype) //true
console.log(a2.o.m) // 10
a1.o.m = 13
console.log(a2.o.m) // 13
```

- 实例
1. 通过new一个函数返回的值就叫做这个函数的实例;如:
```
function A(){}
var a = new A(); //a是实例
```
2. 对象字面量也是一个实例。如:
```
var a = {} //a是实例
```
3. 实例默认包含一个__proto__属性

- __proto__属性
实例上默认会有一个__proto__属性,该属性是一个引用数据类型。实例的__proto__默认指向函数的prototype属性

- prototype
1. 方法(函数/类)上的默认属性,当使用new创建方法的实例时,实例上会自动包含一个__proto__属性指向方法上的该属性。
```
function A() {}
var a = new A();
console.log(a.__proto__ == A.prototype) //true
```
2. 该属性为引用数据类型,也指向一个实例。默认指向一个对象字面量```{}```。 例: 
```
function A() {}
console.log(typeof A.prototype) //object
```
- 对象字面量({})
1. 上文说过,对象字面量也是实例,所以对象字面量也有__proto__属性  
2. 对象字面量的__proto__默认指向Object.prototype,即定义在Object.prototype上的属性/方法都能被对象字面量访问到  

```
Object.prototype.sayHello = function(){
    console.log('hello')
}
var a = {};
a.sayHello();
```

## js如何通过上面的要素实现继承的
主流的继承方式就是通过依赖prototype、__proto__的特性而实现。这种链子的特性又被叫做原型链。prototype是原型的意思

```
 var a = {};
 console.log(a.__proto__ == Object.prototype); //true
 console.log(Object.prototype.__proto__ == null); //true
```

### 继承实现方式
- 不依赖原型的继承

```
function Grandparent() {
    this.x = 1;
}
Grandparent.prototype.px = 11;
function Parent() {
    Grandparent.call(this)
    this.y = 2;
}
function Child() {
    this.z = 3;
    Parent.call(this)
}
var c = new Child(); //c具有x,y,z属性。但是没有px属性
```

- 赖原型继承

```
function Grandparent() {
    this.x = 1;
}
Grandparent.prototype.px = 11;
function Parent() {
    Grandparent.call(this)
    this.y = 2;
}
Parent.prototype = Grandparent.prototype;
Parent.prototype.py = 12;
function Child() {
    this.z = 3;
    Parent.call(this)
}
Child.prototype = Parent.prototype
var c = new Child(); //c具有x,y,z,px,py属性
```

## 为什么需要原型式继承  
原型(prototype)对象里属性是被所有实例共享的,而构造函数里的语句是每次创建一次就会执行一次,所以构造函数里的属性是每个实例里独享的。
所以根据需要以及性能选用不同的继承方式