# js中级知识点
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
- 通常来讲，使用 instanceof 就是判断引用类型（数组、对象、函数）属于哪个构造函数的方法
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
- 所有的函数（不包括数组，对象）都有一个prototype显式原型属性，它也是一个普通的对象
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
        console.log("对象本身的属性"+ item)  //name printName
    }else {
        console.log("对象继承的属性"+ item)  //alertName
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
下面来看上面代码实现的原理图  
![图](https://github.com/manlili/web_interview_question/blob/master/img/prototype.jpg)

## 写一个原型链继承的例子
- 很Low的写法
```bash
function Animal () {
    this.eat = function () {
        console.log('animal eat')
    }
}
function Dog () {
    this.bark = function () {
        console.log('dog bark')
    }
}
Dog.prototype = new Animal ()  //注意这里是new
var hashiqi = new Dog ()
```
- 贴合实际的写法
写一个封装DOM查询的例子
```bash
function Elem(id) {
    this.elem = document.getElementById(id)
}
Elem.prototype.html = function (val) {
    var elem = this.elem
    if (val) {
        elem.innerHTML = val
        return this   //链式操作
    }else {
        return elem.innerHTML
    }
}
elem.prototype.on = function (type, fn) {
    var elem = this.elem
    elem.addEventListener(type, fn)
    return this
}

//一般使用
var div1 = new Elem("test")
div1.html('<p>123</p>')
div1.on(click, function () {
    alert('clicked')
})

//由于返回了this,所以可以链式操作
div1.html('<p>123</p>')
.on(click, function () {
    alert('clicked')
})
.html()
```

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
1. 首先new一个对象，可传可不传参数,this指向这个空对象
2. 接着走到构造函数里面，将参数赋值给this
3. 最后将this返回出去，这一步构造函数是默认返回的，可省略，但是面试是要说的

## zepto(或者其他框架)源码中如何使用原型链
这个我已经有专门的博客写好了,具体细节请看<a href="https://manlili.github.io/categories/%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB%E7%B3%BB%E5%88%97-zepto/">传送门</a>  
整个zepto的源码大概架构就是
```bash
var Zepto = (function(){
  var $,
      zepto = {}  //内部定义的zepto，非外部的Zepto
  
  // ...省略N行代码...

  function Z(dom, selector) {
      var i, len = dom ? dom.length : 0
      for (i = 0; i < len; i++) this[i] = dom[i]
      this.length = len
      this.selector = selector || ''
  }
  
  zepto.init = function(selector, context) {
      return zepto.Z(dom, selector)
  }
  
  $ = function(selector, context){
      return zepto.init(selector, context)
  }

  $.fn = {
      // ...很多属性...
  }
  zepto.Z.prototype = Z.prototype = $.fn

  // ...省略N行代码...
  
  return $
})()

window.Zepto = Zepto
window.$ === undefined && (window.$ = Zepto)
```
## 模块化
### 不使用模块化
- 假设有三个文件
  - util.js 最基础的外部框架，里面有个getFormatDate()
  - a-util.js 相当于业务框架里面又对util底层框架封装了一次 是将util.getFormatDate()封装成aGetFormatDate()
  - a.js 也就是业务里面使用的具体js，里面使用的是a-util.js封装好的aGetFormatDate()
```bash
//util.js里面的内容
function getFormatDate(date, type) {
    //type === 1 返回2017-06-05
    //type === 2 返回2017年6月15日
    // ...
}

//a-util.js
function aGetFormatDate(date) {
    //要求返回2017年6月15日这种格式
    return getFormatDate(date, 2)
}

//a.js
var dt = new Date()
console.log(aGetformatDate(dt))


//html中使用
<script src = 'util.js'> </script>
<script src = 'a-util.js'> </script>
<script src = 'a.js'> </script>
```
上面代码在html使用的时候注意事项
- 三个js使用的顺序，必须先util.js， 中间调a-util.js， 最后a.js
- 这三个文件中的函数必须是全局变量，才能暴露给使用方，这样会产生全局变量的污染
- a.js依赖于a-util.js,但是它不知道还需要依赖于util.js,因为业务开发者和框架人员不一定是同一个人，这时候就需要出现模块化

### 使用模块化
- 假设有三个文件
  - util.js 最基础的外部框架，里面有个getFormatDate()
  - a-util.js 相当于业务框架里面又对util底层框架封装了一次 是将util.getFormatDate()封装成aGetFormatDate()
  - a.js 也就是业务里面使用的具体js，里面使用的是a-util.js封装好的aGetFormatDate()
下面来说一下实现的原理，注意是伪代码书写的
```bash
//util.js里面的内容
export {
    getFormatDate: function(date, type) {
        //type === 1 返回2017-06-05
        //type === 2 返回2017年6月15日
        // ...
    }
}

//a-util.js
var getFormatDate = require('util.js')
export {
    aGetFormatDate: function (date) { 
        //要求返回2017年6月15日这种格式
        return getFormatDate(date, 2)
    }
}

//a.js
var aGetFormatDate = require('aGetFormatDate')
var dt = new Date()
console.log(aGetformatDate(dt))

//html中使用
<script src = 'util.js'> </script>
<script src = 'a-util.js'> </script>
<script src = 'a.js'> </script>
```
上面代码在html使用的时候注意事项
- 三个js使用的顺序，必须先util.js， 中间调a-util.js， 最后a.js
- 这三个文件中的函数不是全局函数，只需要用export暴露出需要的函数
- 从上面可以很清楚的看到a.js依赖于a-util.js,a-util.js依赖于util.js

关于AMD具体编程使用的是require.js实现的，具体代码可见[传送门](https://github.com/manlili/AMD-CMD)

## 简述AMD、CMD和UMD区别
Commonjs 在Nodejs服务端上运行，无法在浏览器端运行。为了满足浏览器端模块化的要求，才有了AMD和CMD。
### AMD
AMD (Asynchronous Module Definition)是 RequireJS 在推广过程中对模块定义的规范化产出。特点是异步加载。AMD 推崇依赖前置，把依赖参数以数组形式保存在前半部分。使用规则如下：
```bash
define(id?, dependencies?, factory);
```

关于AMD典型实例编程使用的是require.js实现的
- 使用场景是: 异步加载JS
- 具体代码可见[传送门](https://github.com/manlili/AMD-CMD)
### CMD
CMD (Common Module Definition)是seaJs在推广过程中对模块定义的规范化产出。它不会异步加载js，而是同步一次性加载出来，使用规则如下：
```bash
define(function(require, exports, module) {
  // 模块代码
});
```

关于CMD典型实例编程使用的是commonJs
- 它是nodeJs模块化的规范，现在被大量的前端使用
- 使用场景是：使用了npm之后建议使用commonJs
### UMD
UMD (Universal Module Definition)，AMD，CommonJS规范是两种不一致的规范，虽然他们应用的场景也不太一致，但是人们仍然是期望有一种统一的规范来支持这两种规范，对两种情况进行判断，UMD兼容两个规范。
```bash
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], factory);
    } else if (typeof exports === 'object') {
        // Node, CommonJS-like
        module.exports = factory(require('jquery'));
    } else {
        // Browser globals (root is window)
        root.returnExports = factory(root.jQuery);
    }
}(this, function ($) {
    //    methods
    function myFunc(){};

    //    exposed public method
    return myFunc;
}));
```