## js实现继承的要素
- 方法(函数/类)
1.方法是一个特殊的实例
```
function A() {}
console.log(A instanceof Function) //true
```
2. 方法上默认会有一个prototype属性,该属性里的属性/方法被该方法的所有实例共享
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

- 对象字面量```{}```
1. 上文说过,对象字面量也是实例,所以对象字面量也有__proto__属性
2. 对象字面量的__proto__默认指向Object.prototype,即定义在Object.prototype上的属性/方法都能被对象字面量访问到
```
Object.prototype.sayHello = function(){
    console.log('hello')
}
var a = {};
a.sayHello();
```

- 实例上的属性查找机制
先搜索实例上是否有访问的属性,如果没查到,则继续从实例属性__proto__里进行查找,如果__proto__里没有,则继续进入到__proto__里的__proto__进行查找,
直到查到请求的数据,或已经查到最高层Object.prototype.__proto__ 直接返回null。


## js如何通过上面的要素实现继承的
主流的继承方式就是通过依赖prototype、__proto__的特性而实现。这种链子的特性又被叫做原型链。prototype是原型的意思

```
 var a = {};
 console.log(a.__proto__ == Object.prototype); //true
 console.log(Object.prototype.__proto__ == null); //true
```
> 实例的
### 原型
原型就是在函数上多了一个叫做prototype属性,该属性是一个对象。
- 作用: