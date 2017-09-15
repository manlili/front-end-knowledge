# js面试的中级知识点
排序不分难易,答案仅供参考

## 如何准确判断一个变量是引用类型
### 常用的语法糖
```bash
var a = {} //其实是var a = new Object()的语法糖
var b = []  //其实是var a = new Array()的语法糖
function Foo () {   //其实是 var Foo = new Function (参数)
    
}
```
上面如果直接表明很容易看出来变量的类型，但是不能每次都用眼看，这个时候我们可以用instanceof
### instanceof
- 通常来讲，使用 instanceof 就是判断一个实例是否属于某种类型
- 与 typeof 方法不同的是，instanceof 方法要求开发者明确地确认对象为某特定类型
 ```bash
// 判断 foo 是否是 Foo 类的实例
function Foo(){} 
var foo = new Foo(); 
console.log(foo instanceof Foo)//true
console.log(foo instanceof Object)//true
```
- 更重的一点是 instanceof 可以在继承关系中用来判断一个实例是否属于它的父类型
```bash
// 判断 foo 是否是 Foo 类的实例 , 并且是否是其父类型的实例
function Aoo(){} 
function Foo(){} 
Foo.prototype = new Aoo();//JavaScript 原型继承
 
var foo = new Foo(); 
console.log(foo instanceof Foo)//true 
console.log(foo instanceof Aoo)//true
```
### instanceof实现的源码
```bash
function instance_of(L, R) {//L 表示左表达式，R 表示右表达式
 var O = R.prototype;// 取 R 的显式原型
 L = L.__proto__;// 取 L 的隐式原型
 while (true) { 
   if (L === null) 
     return false; 
   if (O === L)// 这里重点：当 O 严格等于 L 时，返回 true 
     return true; 
   L = L.__proto__; 
 } 
}
```
## 什么是原型
### 原型的规则
- 所有的引用类型（数组、对象、函数）都有对象的特性，即可自由扩展属性（null除外）
```bash
var obj = {} 
obj.a =100

var arr = []
arr.a = 100

function fn () { }
fn.a = 100
```
- 所有的引用类型（数组、对象、函数）都有一个``__proto__``隐式原型属性，它是一个普通的对象
```bash
var obj = {}
obj.__proto__

var arr = []
arr.__proto__

function fn () { }
fn.__proto__
```
- 所有的函数（不包括数组，对象）都有一个prototype显示原型属性，它也是一个普通的对象
```bash
function fn () { }
fn.prototype
```
- 所有的引用类型（数组、对象、函数），``__proto__``属性值指向**它的构造函数**的prototype属性值
```bash
var obj = {}
obj.__proto__ === Object.prototype  //true, 注意是===
```
- 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的``__proto__``即它的构造函数的prototype中去找，由原则4衍生而来
```bash
function Foo (name, age) {
    this.name = name
}
Foo.prototype.alertName = function () {
    alert(this.name)
}

var f = new Foo('zhangsan')
f.printName = function () {
    console.log (this.name)
}

f.printName()
f.alertName()
```

## 如何区分方法是属于这个对象还是它继承的？
- 使用hasOwnProperty属性
```bash
function Foo (name, age) {
    this.name = name
}
Foo.prototype.alertName = function () {
    alert(this.name)
}

var f = new Foo('zhangsan')
f.printName = function () {
    console.log (this.name)
}

for (item in f) {
    //do something
    if (f.hasOwnProperty(item)) {
        console.log("对象本身的属性"+ item)
    }else {
        console.log("对象继承的属性"+ item)
    }
}
```

## 什么是原型链
下来看一段代码
```bash
function Foo (name, age) {
    this.name = name
}
Foo.prototype.alertName = function () {
    alert(this.name)
}

var f = new Foo('zhangsan')
f.printName = function () {
    console.log (this.name)
}

f.printName()
f.alertName()
f.toString()   //注意：要去f.__proto__.__proto__里面找
```
注意上面多了一个toString(),在f的``__proto__``中没有，那么它就去构造函数Foo.prototype中去找，还是没有，这时就要顺着Foo的``__proto__``找它的构造函数Object.prototype中去找
下面来看一张图
![图](https://github.com/manlili/web_interview_question/blob/master/img/prototype.jpg)

## 写一个原型链继承的例子

## 描述new一个对象的过程
先来看一段代码
```bash
function Foo(name, age) {
    this.name = name
    this.age = age
    this.class = 'class-l'
    //return this   //默认有这一行，一般都是省略
}

var f = new Foo ('zhangsan', 20)
var f2 = new Foo ('lisi', 25)   //创建多个对象
```
下面来总结一下发生的具体过程
1. 首先先new一个对象，可传可不传参数
2. 接着走到构造函数里面，这时候this是空对象，接着将参数赋值给this
3. 最后将this返回出去，这一步构造函数是默认返回的，可省略，但是面试是要说的

## zepto(或者其他框架)源码中如何使用原型链
