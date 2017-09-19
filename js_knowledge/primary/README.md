<!--[TOC]-->

# js初级知识点
排序不分难易,答案仅供参考

## 简述js基本数据类型(值类型)和引用数据类型，以及存储在内存哪里？
### 基本数据类型
- Undefined、Null、Boolean、Number和String
- 基本型数据存在栈中  
- 特点：由于每个变量都需要自己的内存空间，所以占用的空间比较大
### 引用数据类型
- Object、Array和Function
- 引用型数据引用地址存在栈中，而实体对象存在堆中
- 特点：共用相同的内存空间

## 什么是NaN和Null,Undefined，它的类型是什么？怎么测试一个值是否等于 NaN?
### NaN
NaN 是 Not a Number 的缩写，JavaScript 的一种特殊数值，其类型是 Number，可以通过 isNaN(param) 来判断一个值是否是 NaN：
```bash
console.log(isNaN(NaN)); //true
console.log(isNaN(23)); //false
console.log(isNaN('ds')); //true
console.log(isNaN('32131sdasd')); //true
console.log(NaN === NaN); //false
console.log(NaN === undefined); //false
console.log(undefined === undefined); //false
console.log(typeof NaN); //number
```
### Null
null表示没有定义过
### Undefined
undefined表示已定义但是未赋值。
## 强制类型转换发生的情况有哪些？
- 字符串拼接
```bash
var a = 100 + '10' //10010
```
- ==运算符
```bash
100 == '100'  //true
null == undefined  //true,注意这里，一般==有且仅当这种情况才是用
```
- if语句
```bash
var a = 100
if (a) {
    
}
```
- 逻辑运算
## ==和===有什么不同？何时使用===，何时使用==？
- == 先强制类型转换同一种数值，然后比较数据  
- === 先比较数据类型，再比较数据
- 一般除了下面示例是==，其他的全部用===
```bash
//jquery框架中的推荐写法
if (obj.a == null) {
 // 这里相当于obj.a === null || obj.a === undefined 的简写形式
}
```

## 请指出document.onload和document.ready两个事件的区别。
页面加载完成有两种事件：
- ready，表示文档结构已经加载完成（不包含图片等非文字媒体文件）
- onload，指示页面包含图片等文件在内的所有元素都加载完成。

## JS中有哪些内置函数,以及每个内置函数对应的方法
### JS基础知识(ECMA262标准)
- Array
    - push
    - pop
    - unshift
    - shift
    - reverse
    - sort
    - slice
    - splice
    - toSource
    - valueOf
    - concat
    - toString
    - toLocalString
    - join

- String
    - charAt
    - charCodeAt
    - indexOf
    - lastIndexOf
    - match
    - repalce
    - search
    - toLowerCase
    - toUpperCase
    - toLocaleLowerCase
    - toLocaleUpperCase
    - slice
    - substring
    - toSource
    - valueOf
    - toString
    - split
    
- Math
    - ceil(x)
    - floor(x)
    - round(x)
    - max(x,y)
    - min(x,y)
    - random()
    - toSource
    - valueOf
- Date
    - Date
    - getTime
    - getFullYear
    - getMonth
    - getDate
    - getDay
    - getHours
    - getMinutes
    - getSeconds
    - getMilliseconds
    - 
    - setTime
    - setFullYear
    - setMonth
    - setDate
    - setDay
    - setHours
    - setMinutes
    - setSeconds
    - setMilliseconds
    - 
    - toString
    - toSource
    - valueOf
- RegExp
    - test
    - exec
    - search
    - split
    - replace
    - match
- Number
- Boolean
- Object
- Error
- Function
### JS-Web-API(W3C标准)
浏览器中全局函数
- window
- document
- navigator

## 如何理解JSON
- JSON是一个简单的JS对象
- 有两个api
    - JSON.stringify({a: 10, b:20})
    - JSON.parse('{"a": 10, "b", 20}')

## JS中使用typeof能得到哪些类型？
- 可能的字符串有："number"、"string"、"boolean"、"object"、"function" 和 "undefined"。  
- 需要注意typeof null的返回值是object
- 特点：只能区分值类型，区分不了引用类型，因为引用类型返回的都是object，这个时候需要用instanceof
- 实例：  
<table width="600">
  <tbody>
    <tr>
      <td align="center" valign="middle">表达式</td>
      <td align="center" valign="middle">返回值</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof undefined</td>
      <td align="center" valign="middle">'undefined'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof null</td>
      <td align="center" valign="middle">'object'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof true</td>
      <td align="center" valign="middle">'boolean'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof 123</td>
      <td align="center" valign="middle">'number'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof &quot;abc&quot;</td>
      <td align="center" valign="middle">'string'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof function() {}</td>
      <td align="center" valign="middle">'function'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof {}</td>
      <td align="center" valign="middle">'object'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof []</td>
      <td align="center" valign="middle">'object'</td>
    </tr>
    <tr>
      <td align="center" valign="middle">typeof unknownVariable</td>
      <td align="center" valign="middle">'undefined'</td>
    </tr>
  </tbody>
</table>

## 说一下对变量提升的理解
### 执行上下文
- 范围：<script>内（即全局范围）或者一个函数内（局部范围）
- 全局范围：变量定义、函数声明会自动提前
- 函数范围：变量定义、函数声明、this声明、arguments定义也会自动提前
```bash
console.log(b) //直接报错，因为找不到b

console.log(a)  //undefined,这里需要注意：首先执行下面的代码var a但是不给赋值，这时才是undefined
var a = 100

fn('zhangsan')   //函数是自动提升变量
function fn (name) {
    console.log(this)
    console.log(arguments)

    age = 20      //这里是先执行var age ，然后再执行age = 20
    console.log(name, age)
    var age
}
```
### 函数声明和函数表达式
```bash
//函数声明
fn()   //正常执行
function fn () {
    
}

//函数表达式，实际上也就是var a = 100形式
fn1()   //此时报错，因为这是先执行var fn1,但是不给赋值，这时fn1是undefined，所以无法识别为函数
var fn1 = function () {
    
}
```

## 说明this几种不同的使用场景
### this原则: this要在执行时才能确认，定义时无法确认
```bash
var a = {
    name: 'A',
    fn: function () {
        console.log(this)
    }
}
a.fn()   //this === a

a.fn.call({name: 'B'})   //this === {name: 'B'}

var fn1 = a.fn
fn1()   //this === window
```
出现上面的原因主要是js是解释型语言，不是编译型语言，只有真正执行的时候this才起作用 
### this作为构造函数执行
```bash
function Foo (name) {
    this.name = name
    return this //可省略
}

var f = new Foo('test')
```
### 作为对象的属性执行
```bash
var obj = {
    name: 'A',
    fn: function () {
        console.log(this.name)
    }
}
```
### 作为普通函数执行
```bash
function fn () {
    console.log(this)   //指向window
}
fn()
```
### call apply bind
```bash
function fn (name, age) {
    console.log(this)   //指向{x: 100}
}
fn.call({x: 100}, 'zhangdan', 100)
```
我博客里面已经总结好，详情请看<a href="https://manlili.github.io/2017/08/10/call-apply-bind/">传送门</a>


## 如何理解作用域
### ES5里面没有块级作用域，只有函数作用域
```bash
//全局作用域定义
var b = 100

//没有块级作用域，下面的name相当于正在全局作用域里面定义的
if (true) {
    var name = 'zhangan'
}
console.log(name)  //zhangan

//函数作用域
function fn() {
    var c = 20
    console.log('fn', c) // c=20
}
fn()
console.log('全局里面查找C', c)  //报错，c is not defined
```
### 自由变量
定义：当前作用域没有定义的变量
```bash
var a = 100
function fn () {
    var b = 200
    
    console.log(a)   //a = 100,当前作用域没有定义的变量，即"自由变量"
    console.log(b)   //100
}
fn()
```

### 作用域链
定义：一个自由变量不断的往父级作用域寻找值的过程,注意这里的父级作用域是变量定义时候的作用域，不是变量执行时候的作用域
```bash
var a = 100
function fn () {
    var b = 200
    
    console.log(a)   //a = 100,当前作用域没有定义的变量，即"自由变量",这时候需要去父级作用域找a,a的父级作用域是全局作用域
    console.log(b)   //100
}
fn()

//再举一个例子
var a = 100
function F1() {
    var b = 200
    function F2 () {
        var c = 300
        console.log(a)   //100
        console.log(b)   //200
        console.log(c)   //300
    }
    F2()
}
F1()

//不断的演变
var a = 100
function F1() {
    var a = 400
    var b = 200
    function F2 () {
        var c = 300
        console.log(a)   //400
        console.log(b)   //200
        console.log(c)   //300
    }
    F2()
}
F1()
```
### 闭包使用的场景也要说，具体见下面

## 什么是闭包
### 闭包的定义
关于这个我有一篇博客，详情请看<a href="https://manlili.github.io/2016/04/10/%E9%97%AD%E5%8C%85/">传送门</a>
### 闭包使用的场景
- 函数作为返回值
```bash
function F1 () {
    var a = 100
    
    //返回一个函数（函数作为返回值）
    return function () {
        console.log(a)  //"自由变量",这时候需要去父级作用域找a,a的父级作用域是F1
    }
}

//f1得到一个函数
var f1 = F1()
var a =200
f1()  //a=100，a的值是在定义的作用域里面（这里是指F1）找，而不是执行的作用域（这里是指全局）找
```
- 函数作为参数传递
```bash
function F1 () {
    var a = 100
    
    //返回一个函数（函数作为返回值）
    return function () {
        console.log(a)  //"自由变量",这时候需要去父级作用域找a,a的父级作用域是F1
    }
}

//f1得到一个函数
var f1 = F1()

function F2 (fn) {
    var a = 200
    fn()
}

F2(f1)
```

## 实际开发中闭包的应用
- 闭包实际应用中主要用于封装变量，收敛权限
```bash
function isFirstLoad () {
    var _list = []  //封装数据源，除了这个函数内部，外面的一律拿不到也改不了_list
    console.log(arguments)
    return function (id) {
        if(_list.indexOf(id) >= 0) {
            return false
        }else {
            _list.push(id)
            return true
        }
    }
}

var firstLoad = isFirstLoad ()

//注意firstLoad是isFirstLoad()返回的函数
firstLoad(10)  //true
firstLoad(10)  //false
firstLoad(20)  //true
firstLoad(20)  //false
```

## 创建10个<a>标签，点击的时候弹出对应的序号
考点：函数作用域的使用
```bash
//下面是错误的写法，是因为创建完不是立马点击，等后面点击的时候i早都到10了并且会一直保持10
var i , a
for (i = 0; i < 10; i++) {
    a = document.createElement('a')
    a.innerHTML = i + '<br>'
    a.addEventListener('click', function (e) {
        e.preventDefault()
        alert(i)  //自由变量，向父作用域里面找i
    })
    document.body.appendChild(a)
}

//正确的写法
var i
for (i = 0; i < 10; i++) {
    (function(i) {  //新的函数，有自己独立的函数作用域
        var a = document.createElement('a')
        a.innerHTML = i + '<br>'
        a.addEventListener('click', function (e) {
            e.preventDefault()
            alert(i) //自由变量，向父作用域里面找i
        })
        document.body.appendChild(a)
    })(i)  //自执行函数
}
```

## 同步和异步的区别？分别举一个同步和异步的例子
### 异步
```bash
console.log(100)
setTimeout(function () {
    console.log(200)
}, 1000)
console.log(300)  //效果是100 300 200
```
### 同步
```bash
console.log(100)
console.log(200)
console.log(300)
```
### 异步和同步的区别
在于有没有阻塞程序的进程，同步阻塞，异步不阻塞
```bash
console.log(100)
alert(200)  //什么时候确认，什么时候执行下面的代码
console.log(300)
```
### 何时需要异步
- 有可能发生等待的情况
- 等待过程中不能像alert一样阻塞程序的运行


## 前端使用异步的场景有哪些？
- 定时任务：setTimeout，setInverval
- 网络请求：ajax请求， 动态<img>加载
- 事件绑定：比如监听点击事件
```bash
//ajax请求示例
console.log('start')
$.get('./data.json', function (data) {
    console.log(data)
})
console.log('end') //先打印start  end  data

//img加载示例
console.log('start')
var img = document.createElement('img')
img.onload = function () {
    console.log('loaded')
}
img.src = '/***.png'
console.log('end')  //先打印start end loaded

//事件绑定示例
console.log('start')
document.getElementById('btn1').addEventListener('click', function() {
    alert('clicked')
})
console.log('end')  //先打印start end clicked
```
## 什么是单线程？单线程和异步的关系？
### 单线程
js是单线程，一次只能做一件事情，一般都是配合异步使用
```bash
console.log(100)
setTimeout(function () {
    console.log(200)
})  //注意这里没有1000毫秒延时，但是setTimout是异步的标志，遇见这个标签就会自动挂起，等后面代码执行完再执行这里
console.log(300)  //效果是100 300 200
```
上面的过程是：
- 执行第一行，打印100
- 执行setTimeout后，传入setTimout的函数会被暂存起来，不会立即执行（单线程的特点，不能同时干两件事情）
- 执行最后一行，打印300
- 待所有的程序都执行完，处于空闲状态时，会立马看有没有暂存起来的要执行
- 发现暂存起来要执行的setTimout中函数无需等待时间，就立即过来执行

```bash
console.log(100)
setTimeout(function () {
    console.log(200)
}, 1000)  
console.log(300)  //效果是100 300 200
```
上面的过程是：
- 执行第一行，打印100
- 执行setTimeout后，传入setTimout的函数会被暂存起来，不会立即执行（单线程的特点，不能同时干两件事情），但是需要1秒后才能解封
- 执行最后一行，打印300
- 待所有的程序都执行完，处于空闲状态时，会立马看有没有暂存起来的要执行
- 发现暂存起来要执行的setTimout中函数需要等待1秒后解封，就等它解封后再执行

再举个例子
```bash
//ajax请求示例
console.log('start')
$.get('./data.json', function (data) {
    console.log(data)
})
console.log('end') //先打印start  end  data
```
上面的过程是：
- 执行第一行，打印start
- 执行ajax请求后，将请求后返回的结果暂存，继续执行下面的
- 执行最后一行，打印end
- 待所有的程序都执行完，处于空闲状态时，会立马看有没有暂存起来的要执行
- 这时候需要看服务器那边有没有返回数据，如果返回，则直接执行，没有返回就继续等待结果返回

```bash
//事件绑定示例
console.log('start')
document.getElementById('btn1').addEventListener('click', function() {
    alert('clicked')
})
console.log('end')  //先打印start end clicked
```
上面的过程是：
- 执行第一行，打印start
- 等待点击，暂存起来这个事件
- 执行最后一行，打印end
- 待所有的程序都执行完，处于空闲状态时，会立马看有没有暂存起来的要执行
- 这时候需要看用户有没有点击，没有点击继续等待，点击后接着执行，当然用户可能会点击很多次

## 一个关于setTimeout的笔试题
```bash
console.log(1)
setTimeout(function() {
    console.log(2)
}, 0)
console.log(3)
setTimeout(function() {
    console.log(4)
}, 1000)
console.log(5)
//打印的结果是 1 3 5 2 4
```

## 单线程和异步的关系
就是是单线程，但是我想一次做多个事情，这个时候就需要暂存起来，就需要异步

## 获取2017-06-10格式的日期
知识点是Date对象的方法
```bash
function formatDate(dt) {
    if (!dt) {
        dt = new Date()
    }
    var year = dt.getFullYear()
    var month = dt.getMonth() + 1
    var date = dt.getDate()
    
    if (month < 10) {
        month = '0' + month
    }
    
    if (date < 10) {
        date = '0' + date
    }
    
    return year + '-' + month + '-' + date
}

var dt = new Date()
formatDate(dt)
```

## 获取一个随机数，要求是长度一致的字符串格式
```bash
var random = Math.random()   //0~1之间的数 0.556822335566
random = random + '0000000000'   //加10个零
random = random.slice(1, 10)
```

## 写一个能遍历对象和数组的通用forEach函数
```bash
function likeForEach(obj, fn) {
    var key
    if (obj instanceof Array) { //或者Array.isArray(obj)
        obj.forEach(function (item, index) {  //注意这里必须是先item index
            fn(index, item)
        })
    }else {
        for (key in obj) {
            if (obj.hasOwnProperty(key)) {
                fn(key, obj[key])
            }
        }
    }
}

var arr = [21, 22, 23]
likeForEach (arr, function (index, item) {
    console.log(index, item)
})

var obj = {x: 100, y: 200}
likeForEach (obj, function (key, value) {
    console.log(key, value)
})
```
## DOM是哪种基本的数据结构？
### DOM的本质
全称：document obj model
```bash
//xml结构,可以随意自定义标签
<?xml>
 <node></node>
 <other></other>
</xml>

//html只能用固定的结构
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link href="/test/asset/src/h5/style/global.css" rel="stylesheet" type="text/css">
  </head>
  <body>

  </body>
</html>
```
是由字符串组成的浏览器可识别的树

## DOM操作常用的API有哪些？
### DOM节点的操作
- 获取DOM节点
```bash
var dom = document.getElementById("div1")  //单体模式
var list1 = document.getElementsByTagName('p')  //集合模式
var list2 = document.getElementsByClassName('.ta') //集合模式

var list3 = document.querySelectorAll(css选择器) //集合模式,是上面三种模式的总体书写模式，参数可为#div1, p, .ta
```
- 获取Property
```bash
var list3 = document.querySelectorAll('p') //集合模式
var p = list3[0]

//获取样式
console.log(p.style.width)
p.style.width = '100px' 

//获取class
console.log(p.className)
p.className = "p1"

//获取nodeName
console.log(p.nodeName)  //p

//获取nodeType
console.log(p.nodeType)  //1
```
### DOM结构操作
- 新增节点
```bash
var p1 = document.createElement('p')
p1.innerHtml = 'test'

var div1 = document.getElementById('div1')
div1.appendChild(p1)  //添加在div1里面的最后面，不顶替里面的节点
```
- 删除节点
```bash
var div1 = document.getElementById('div1')
var child = div1.childNodes   //集合模式
div1.removeChild(child)
```
- 获取父元素
```bash
var div1 = document.getElementById('div1')
var parent = div1.parentElement
```
- 获取子元素
```bash
var div1 = document.getElementById('div1')
var child = div1.childNodes
div1.removeChild(child)
```

## DOM节点的property和Attribute有何区别
- property  
js对象的基本属性的获取和修改
```bash
var obj = {x: 100, u: 300}
console.log(obj.x)  //100

var p = document.getElementsByName('p')[0]
console.log(p.nodeName)   //P
```
- Attribute  
html标签里面的属性
```bash
var p = document.getElementsByName('p')[0]
p.getAttribute('data-name')
p,getAttributr('style')
```

## Bom操作
- navigator
```bash
var ua = navigator.userAgent
var isChrome = ua.indexOf('Chrome')
var isIos = ua.indexOf('ios')
```
- screen  
屏幕的特性
```bash
screen.width
screen.height
```
- location
```bash
location.href
location.protocol
location.pathname
location.search
location.hash
```
- history
```bash
history.back()
history.forward()
history.go(2)  //或者-2
```

## 如何检测浏览器类型
```bash
var ua = navigator.userAgent // "Mozilla/5.0 (iPhone; CPU iPhone OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13B143 Safari/601.1"
var isChrome = ua.indexOf('Chrome')
var isOs = ua.indexOf('OS')
```

## 解析url的各部分api有哪些
```bash
location.href   //   http://192.168.0.233:3000/webapp/index?query=345#123
location.protocol  //   http:
location.pathname //  /webapp/index
location.search  //    ?query=345
location.hash   // #123
```
## 你如何从浏览器的URL中获取查询字符串参数。
```bash
function parseQueryString ( name ){
  name = name.replace(/[\[]/,"\\\[");
  var regexS = "[\\?&]"+name+"=([^&#]*)";
  var regex = new RegExp( regexS );
  var results = regex.exec( window.location.href );

  if(results == null) {
      return "";
  } else {
   return results[1];
  }
}
```

## 描述事件冒泡流程，哪些事件是冒泡的应用？
### 树形结构
DOM是树形结构，所以冒泡是从下往上
### 事件冒泡的使用
```bash
//html
<body>
    <div id="div1">
        <p id="p1">激活</p>
        <p id="p2">激活</p>
        <p id="p3">激活</p>
        <p id="p4">激活</p>
    </div>
    <div id="div2">
        <p id="p5">激活</p>
        <p id="p6">激活</p>
        <p id="p7">激活</p>
        <p id="p8">激活</p>
    </div>
</body>

//js
var p1 = document.getElementById('p1')
var body = document.body

function bindEvent(elem, type, fn) {
    elem.addEventListener(type, fn) //IE低版本使用的是attachEvent 
}
bindEvent(p1, 'click', function (e) {
    // e.stopPropatation() 阻止冒泡，这个必须要会和面试时候要说
    alert('激活')
})
bindEvent(body, 'click', function (e) {
    alert('取消')
})

//最后是先弹出激活，后弹出取消
```
### 冒泡的应用-事件代理
```bash
//html
<div id="div1">
    <a href="#"></a>
    <a href="#"></a>
    <a href="#"></a>
    <a href="#"></a>
    <a href="#"></a>
    <!--随时添加更多的a-->
</div>

//js
//由于a标签不断的增加，事件不能绑定在a标签里面，但是又想获取a标签的内容，这个时候要考虑冒泡到父节点,z在父节点监听
var div1 = document.getElementById('div1')
div1.addEventListener('click', function(e) {
    var target = e.target
    if(target.nodeName === 'A') {
        alert(target.innerHTML)
    }
})
```
## 事件代理的好处
- 代码简洁
- 减少浏览器的内存的占用

## 对于一个无限下拉加载图片的页面，如何给每个图片绑定事件
使用代理

## 编写一个通用的事件监听函数
```bash
//不考虑代理情况下
function bindEvent(elem, type, fn) {
    elem.addEventListener(type, fn) //IE低版本使用的是attachEvent 
}
var a = document.getElementById('link1')
bindEvent(a, 'click', function(e) {
    e.preventDefault()//阻止默认行为
    alert('clicked')
})

//通用的事件监听,包含代理和非代理
function bindEvent(elem, type, selector, fn) {  //selector 被代理的物
    if (fn == null) {
        fn = selector
        selector = null
    }
    
    elem.addEventListener(type, function(e) {
        var target 
        if (selector) {
            target = e.target
            if (target === 'selector') {
                fn.call(target, e)
            }
        }else {
            fn(e)
        }
    })
}

//使用代理
var div1 = document.getElementById('div1')
bindEvent(div1, 'click', function (e) {
    console.log(this.innerHTML)   //注意这里的this指的是a标签，不是div1，所以用fn.call(target, e)
})

//不使用代理
var a = document.getElementById('a1')
bindEvent(a, 'click', function (e) {
    console.log(this.innerHTML)
})
```
## 请描述下事件冒泡和事件捕获机制。
- 冒泡型事件：事件按照从最特定的事件目标到最不特定的事件目标(document对象)的顺序触发。
- 捕获型事件：事件从最不精确的对象(document对象)开始触发，然后到最精确(也可以在窗口级别捕获事件，不过必须由开发人员特别指定)。

## ajax的状态码有哪些?
### readyState状态码
- 0 （未初始化）还没有调用send()方法 
- 1 （载入）已调用send()方法，正在发送请求 
- 2 （载入完成）send()方法执行完成，已经接收到全部响应内容 
- 3 （交互）正在解析响应内容 
- 4 （完成）响应内容解析完成，可以在客户端调用了 
### status状态码
- 2xx 表示成功处理请求 如200，请求成功
- 3xx 需要重定向，浏览器直接跳转  如305使用代理，被请求的资源必须通过指定的代理才能被访问
- 4xx 客户端错误 如404 找不到对象。请求失败，资源不存在
- 5xx 服务器端错误

## 手动写一个ajax，不依赖第三方库
```bash
var xhr = new XMLHttpRequest()
xhr.open('GET', '/API', false)
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
        if (xhr.status === 200) {
            alert(xhr.responseText)
        }
    }
}
xhr.send(null)
```
## 什么是跨域
- 定义
浏览器有同源的策略，不容许ajax访问其他域接口
- 跨域的条件  
协议  
域名   
端口  
- 举例  
你的网站：http://www.yourname.com:80/page1.html  
你要访问的网站: https://www.source.com:443/gateway/home/getHomeData  
上面例子的协议  比如https， http  
上面例子的域名  比如www.yourname.com 和 www.source.com  
上面例子的端口  比如80 和443

## 跨域的几种实现方式
### 三个标签允许跨域加载资源
- <img src=***>
- <link href=***>
- <script src=***>
### 三个标签的使用场景
- img标签用于打点统计，统计网站可能是其他域
- link，script可以使用CDN,CDN的也是其他域
- script可以用于JSONP
### 服务器端设置http header
另外一个解决跨域的简洁方法，需要服务器端来，前端需要了解
```bash
//第二个参数是允许跨域的域名城，*代表全部都允许跨域
response.setHeader('Access-Control-Allow-Origin', 'https://a.com', 'http://a.com')
response.setHeader('Access-Control-Allow-Origin', *)

//接受跨域的cookie
response.setHeader('Access-Control-Allow-Credentials', 'true')
```
### 跨域注意事项
- 所有的跨域请求都必须经过信息提供方的允许
- 如果未经允许即可获取信息，那么就是浏览器的同源策略出了问题

## 什么是JSONP
### JSOP实现跨域的前提
- 加载http://www.baidu.com:80/page1.html 
- 服务器端不一定有page1.html，可能是服务器端根据你的请求动态拼接起来的
- 同理，如果我请求的是http://www.baidu.com:80/api.js，这个js也不一定存在，也可能是服务器动态拼接的
- 那么我们就可以使用<script src="http://www.baidu.com:80/api.js">,拿到api.js里面的内容进行处理
### JSOP实现的原理
- 假设A网站用script标签src向B网站发送了请求，B只需要将A所需要的数据放在api.js，数据格式为A,B协商的格式，比如{a: 10, b: 20},A拿到数据后直接处理就可以了
- 实现的源码
```bash
<script src = "http://www.baidu.com:80/api.js"></script>
<script>
   window.callback = function (data) {
        //这是我们跨域得到的信息
        console.log(data)  //{a: 10, b: 20}
   }
</script>
```


## 关于HTTP请求GET和POST的区别
1.GET提交，请求的数据会附在URL之后（就是把数据放置在HTTP协议头＜request-line＞中），以?分割URL和传输数据，多个参数用&连接;例如：login.action?name=hyddd&password=idontknow&verify=%E4%BD%A0 %E5%A5%BD。如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，则直接把字符串用BASE64加密，得出如： %E4%BD%A0%E5%A5%BD，其中％XX中的XX为该符号以16进制表示的ASCII。

POST提交：把提交的数据放置在是HTTP包的包体＜request-body＞中。上文示例中红色字体标明的就是实际的传输数据
因此，GET提交的数据会在地址栏中显示出来，而POST提交，地址栏不会改变

2.传输数据的大小：
首先声明，HTTP协议没有对传输的数据大小进行限制，HTTP协议规范也没有对URL长度进行限制。 而在实际开发中存在的限制主要有：
GET:特定浏览器和服务器对URL长度有限制，例如IE对URL长度的限制是2083字节(2K+35)。对于其他浏览器，如Netscape、FireFox等，理论上没有长度限制，其限制取决于操作系统的支持。
因此对于GET提交时，传输数据就会受到URL长度的限制。
POST:由于不是通过URL传值，理论上数据不受限。但实际各个WEB服务器会规定对post提交数据大小进行限制，Apache、IIS6都有各自的配置。

3.安全性：
POST的安全性要比GET的安全性高。注意：这里所说的安全性和上面GET提到的“安全”不是同个概念。上面“安全”的含义仅仅是不作数据修改，而这里安全的含义是真正的Security的含义，比如：通过GET提交数据，用户名和密码将明文出现在URL上，因为(1)登录页面有可能被浏览器缓存， (2)其他人查看浏览器的历史纪录，那么别人就可以拿到你的账号和密码了。


##  js深度复制的方式
1、使用jq的$.extend(true, target, obj)   
2、newobj = Object.create(sourceObj)，// 但是这个是有个问题就是 newobj的更改不会影响到 sourceobj但是 sourceobj的更改会影响到newObj   
3、newobj = JSON.parse(JSON.stringify(sourceObj))     


## 请解释变量声明提升。
在JS里定义的变量，存在于作用域链里，而在函数执行时会先把变量的声明进行提升，仅仅是把声明进行了提升，而其值的定义还在原来位置。示例如下：
```bash
 var test = function() {
     console.log(name); // 输出：undefined
     var name = "jeri";
     console.log(name); // 输出：jeri
 }
 
 test();
```
上述代码与下述代码等价。
```bash
 var test = function() {
     var name;
     console.log(name); // 输出：undefined
     name = "jeri";
     console.log(name); // 输出：jeri
 }
 
 test();
```
由以上代码可知，在函数执行时，把变量的声明提升到了函数顶部，而其值定义依然在原来位置。

## 简述AMD、CMD和UMD区别
Commonjs 在Nodejs服务端上运行，无法在浏览器端运行。为了满足浏览器端模块化的要求，才有了AMD和CMD。
### AMD
AMD (Asynchronous Module Definition)是 RequireJS 在推广过程中对模块定义的规范化产出。对于依赖的模块，AMD 是提前执行。AMD 推崇依赖前置，把依赖参数以数组形式保存在前半部分。使用规则如下：
```bash
define(id?, dependencies?, factory);
```
### CMD
CMD (Common Module Definition)是 Seajs 在推广过程中对模块定义的规范化产出。 CMD 是延迟执行，CMD 推崇依赖就近，使用规则如下：
```bash
define(function(require, exports, module) {
  // 模块代码
});
```
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
### Require.js 和Sea.js区别
Require.js 和Sea.js都是模块加载器，两者的主要区别如下：

- 定位有差异。RequireJS 想成为浏览器端的模块加载器，同时也想成为 Rhino / Node 等环境的模块加载器。Sea.js 则专注于 Web 浏览器端，同时通过 Node 扩展的方式可以很方便跑在 Node 环境中。
- 遵循的规范不同。RequireJS 遵循 AMD（异步模块定义）规范，Sea.js 遵循 CMD （通用模块定义）规范。规范的不同，导致了两者 API 不同。Sea.js 更贴近 CommonJS Modules/1.1 和 Node Modules 规范。
- 推广理念有差异。RequireJS 在尝试让第三方类库修改自身来支持 RequireJS，目前只有少数社区采纳。Sea.js 不强推，采用自主封装的方式来“海纳百川”，目前已有较成熟的封装策略。
- 对开发调试的支持有差异。Sea.js 非常关注代码的开发调试，有 nocache、debug 等用于调试的插件。RequireJS 无这方面的明显支持。
- 插件机制不同。RequireJS 采取的是在源码中预留接口的形式，插件类型比较单一。Sea.js 采取的是通用事件机制，插件类型更丰富。

## 下面两个函数的返回值是一样的吗？为什么？
```bash
function foo1()
{
  return {
      bar: "hello"
  };
}
 
function foo2()
{
  return
  {
      bar: "hello"
  };
}
```
在编程语言中，基本都是使用分号（;）将语句分隔开，这可以增加代码的可读性和整洁性。而在JS中，如若语句各占独立一行，通常可以省略语句间的分号（;），JS 解析器会根据能否正常编译来决定是否自动填充分号：
```bash
var test = 1 + 2;
console.log(test);  //3
```
在上述情况下，为了正确解析代码，就不会自动填充分号了，但是对于 return 、break、continue 等语句，如果后面紧跟换行，解析器一定会自动在后面填充分号(;)，所以上面的第二个函数就变成了这样：
```bash
function foo2()
{
  return;
  {
      bar: "hello"
  };
}
```
所以第二个函数是返回 undefined。

## 使用 typeof bar === “object” 判断 bar 是不是一个对象有什么潜在的弊端？如何避免这种弊端？
使用 typeof 的弊端是显而易见的(这种弊端同使用 instanceof)：
```bash
let obj = {};
let arr = [];
 
console.log(typeof obj === 'object');  //true
console.log(typeof arr === 'object');  //true
console.log(typeof null === 'object');  //true
```
从上面的输出结果可知，typeof bar === “object” 并不能准确判断 bar 就是一个 Object。可以通过 Object.prototype.toString.call(bar) === “[object Object]” 来避免这种弊端：
```bash
let obj = {};
let arr = [];
 
console.log(Object.prototype.toString.call(obj));  //[object Object]
console.log(Object.prototype.toString.call(arr));  //[object Array]
console.log(Object.prototype.toString.call(null));  //[object Null]
```
另外，为了珍爱生命，请远离 ==： 
珍爱生命
而 [] === false 是返回 false 的。

## 下面的代码会在 console 输出什么？为什么？
```bash
(function(){
  var a = b = 3;
})();
 
console.log("a defined? " + (typeof a !== 'undefined'));   
console.log("b defined? " + (typeof b !== 'undefined'));
```
这跟变量作用域有关，输出换成下面的：
```bash
console.log(b); //3
console,log(typeof a); //undefined
```
拆解一下自执行函数中的变量赋值：
```bash
b = 3;
var a = b;
```
所以 b 成了全局变量，而 a 是自执行函数的一个局部变量。

## 下面的代码会在 console 输出什么？为什么？
```bash
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log("outer func:  this.foo = " + this.foo);
        console.log("outer func:  self.foo = " + self.foo);
        (function() {
            console.log("inner func:  this.foo = " + this.foo);
            console.log("inner func:  self.foo = " + self.foo);
        }());
    }
};
myObject.func();
```
第一个和第二个的输出不难判断，在 ES6 之前，JavaScript 只有函数作用域，所以 func 中的 IIFE 有自己的独立作用域，并且它能访问到外部作用域中的 self，所以第三个输出会报错，因为 this 在可访问到的作用域内是 undefined，第四个输出是 bar。如果你知道闭包，也很容易解决的：
```bash
(function(test) {
  console.log("inner func:  this.foo = " + test.foo);  //'bar'
  console.log("inner func:  self.foo = " + self.foo);
}(self));
```

## 将 JavaScript 代码包含在一个函数块中有什么意思呢？为什么要这么做？
换句话说，为什么要用立即执行函数表达式（Immediately-Invoked Function Expression）。
IIFE 有两个比较经典的使用场景，一是类似于在循环中定时输出数据项，二是类似于 JQuery/Node 的插件和模块开发。
```bash
for(var i = 0; i < 5; i++) {
  setTimeout(function() {
      console.log(i);  
  }, 1000);
}
```
上面的输出并不是你以为的0，1，2，3，4，而输出的全部是5，这时 IIFE 就能有用了：
```bash
for(var i = 0; i < 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);  
    }, 1000);
  })(i)
}
```
而在 JQuery/Node 的插件和模块开发中，为避免变量污染，也是一个大大的 IIFE
```bash
(function($) { 
        //代码
 } )(jQuery);
```

## 简述常见js设计模式
总体来说设计模式分为三大类：
- 创建型模式，共五种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。
- 结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。
- 行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模

## 简述JS深浅拷贝的原理及项目应用
[答案我已总结出来，点击查看参考地址](https://manlili.github.io/2017/04/17/JS%E7%9A%84%E6%B5%85%E6%8B%B7%E8%B4%9D%E4%B8%8E%E6%B7%B1%E6%8B%B7%E8%B4%9D%E7%A0%94%E7%A9%B6/)

## 写出下面的输出结果
```bash
var p = new Promise((resolve, reject)=> {reject()}).then(()=>{console.info('resolve1')}, ()=>{console.info('reject1')})
p.then(()=>{console.info('resolve2')}, ()=>{console.info('reject2')})
```
输出结果reject1, resolve2