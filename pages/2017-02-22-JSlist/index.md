---
title: 前端一些重点list
date: "2017-02-18T22:12:03.284Z"
path: "/interviewRecord/"
---

##gulp.js 构建 pipe()
done
##阿里飞猪 主要是移动页面展示，所以css 也要准备 
##BFC IFC
done
## pub/v ftl
都是在同一个服务器里面，只不过静态资源走的是静态域名
## 项目中的模板语法
regular nej
## 如何优化作用域链的查找
形成作用域的
函数 作用域
with
全局作用域
函数嵌套 会产生作用域链
减少作用域上的查找次数
闭包
IIFC 立即执行函数
如果我们作出一些很简单的修改，在逻辑代码外包装一层函数，这样效果就大不同了。当UI渲染完成之后，代码
对data的引用也就随之解除，而在最外层函数执行完毕时，JAVASCRIPT引擎就开始对其中的对象进行检查，data也就可以随之被回收。
## regular 为什么要脏检查
//TODO
脏检查 优点  兼容性比较好 

编译的时候的过程：
parsing和 compile
parse：html 模板 解析为 AST
compile：结合特定的数据模型(在regularjs中，是一个裸数据)， 模板引擎层级游历AST并递归生成Dom节点
归功于 watch函数 一旦表达式发生改变，文本节点也会随之改变，这一切其实与angularjs并无两样(事实上regularjs同样也是基于脏检查)
$watch: 添加一个数据监听器(watcher对象)

如何判断 数组发生改变？
digest 将会进行数据检查，它的处理流程如下:

标记dirty = false
遍历所有通过component.$watch绑定的数据观察者watcher，对比当前值watcher.get(component)与老值watcher.last
如果值发生改变，运行绑定的监听器 - watcher.fn(newvalue, oldvalue)，并导致__dirty__=true。设置watcher.last=newvalue`
进入下一个watcher的检查
遍历检查一轮后，如果dirty===true，我们重新进入步骤1. 否则进入步骤4.
完成脏检查

为什么要使用脏检查：
1.脏检查完全不关心你改变数据的方式，而常规的set, get的方式则会强加许多限制
脏检查完全不关心你改变数据的方式，而常规的set, get的方式则会强加许多限制
2.脏检查可以实现批处理完数据之后，再去统一更新view.
3.脏检查其实比 GET/SET 更容易实现。脏检查是个单向的检查流程(请不要和双向绑定发生混淆)，可以实现_任意复杂度的表达式支持。
而get/set的方式则需要处理复杂依赖链，基本上表达式支持都是阉割的(使用时就像踩雷).


缺点 性能问题  
脏检查 低效 它的效率基本上取决于你绑定的观察者数量，在Regular中，你可以通过@(Expression)元素来控制你的观察者数量。
Regular实际上在解析时，已经提取了表达式的依赖关系，在未来Observe到来时，可以调整为脏检查 + 依赖计算的方式
由于脏检查机制的性能极大的依赖于监听器的数量，为了精确控制监听器的数量，regularjs引入了一个新的表达式语法元素@()提供了bind-once的表达式的支持.
 这个被监听的表达式在检查到一次值变化就会被解除监听。
由于脏了一次就被被抛弃, 如果值后续继续变化，会导致ui与data的不同步，所以请小心使用

请尽量使用一次绑定


<nest-component r-model={} > </nest-component>
使用list的track by功能

使用isolate 单向绑定 

使用if else代替 display:none

使用throttle或until(tid = setTimeout)的方式来避免频繁更新


## bower 管理组件 与npm的区别

与NPM最大的区别在于，NPM主要运用于Node.js项目的内部依赖包管理，安装的模块位于项目根目录下的node_modules
文件夹内。而Bower大部分情况下用于前端开发，对于CSS/JS/模板等内容进行依赖管理，依赖的下载目录结构可以自定义。

因为npm设计之初就采用了的是嵌套的依赖关系树，这种方式显然对前端不友好；而Bower则采用扁平的依赖关系管理方式，
使用上更符合前端开发的使用习惯。
使用NPM作用于后端 bower 作用于前端的组合使用模式。
让前后端公用开发语言的同时，不同端的开发工程师能够更好地利用手上的工具提升开发效率。

关键在于npm的依赖管理是奇特的倒向树结构（不同于linux越底层依赖越小）。一个普通的前端包的依赖树非常冗长，
甚至可能触及windows下256字符的路径长度限制。同时和其它安装包不能共享依赖代码。导致文件非常多，不适合前端代码部署。
而bower让模块开发者定义了简洁的输出文件。

npm 可以算做node的第三方工具包管理，bower是前端库管理的工具，管理一些js类库

npm 可以结合Browserify 项目用 CommonJS 写，不需要任何配置，给一个入口文件就行！还有一个官方工具 watchify，一行命令跑起，
保存文件自动构建，连 grunt gulp 都不需要。
这个方案唯一的缺点，就是 npm 的树状依赖结构可能导致重复的模块和代码量的臃肿，需要跑一次 `npm dedupe` 来尽量压平依赖树。
当然，实际情况中前端模块出现依赖同一模块的不兼容版本还是很少见的。


## pwa

那就是PWA（渐进式增强WEB应用）。
PWA有以下几种特性：

Installablity（可安装性）
App Shell
Offline（离线能力）
Re-engageable（推送通知能力）
所有这些特性都是“优雅降级、渐进增强的”，给支持的设备更好的体验，不支持的设备也不会更差。
这就和微信小程序这种二流设计的根本不同之处。

实现思路就是，利用service worker，另起一个线程，用来监听所有网络请求，讲已经请求过的数据放入cache，在断网的情况下，
直接取用cache里面的资源。为请求过的页面和图片，展示一个默认值。当有网络的时候，再重新从服务器更新。

PWA主要一个Manifest.son来配置一些功能，像浏览器样式、添加到屏幕的图标等等。
利用Service Worker来实现离线存储


## ie6 兼容 avalon 
使用的是 VBScript
## AMD CMD amd按顺序加载依赖不太好，所以才有了cmd吧 为什么要有CMD
 
## node为什么要用commonjs 因为node是服务器端运行，资源在本地，读取速度快 不需要异步

CommonJS 是同步的，

CMD(sea.js) 异步加载 同步执行 ES6 的模块体系最后选择的是异步加载和同步执行。也就是 Sea.js 的行为是最接近 ES6 模块的。
不过 Sea.js 这样做是需要付出代价的——需要扫描代码提取依赖，所以它不像 CommonJS/AMD 是纯运行时的模块系统。

AMD 异步执行异步加载 RequireJS基于AMD 规范的
对于依赖的模块，AMD是提前执行，CMD是延迟执行。CMD推崇依赖就近，AMD推崇依赖前置。

Browserify 是目前最常用的 CommonJS 格式转换的工具。
http://www.ruanyifeng.com/blog/2015/05/commonjs-in-browser.html 


## 脏检查 regular 为什么要用脏检查 性能上 该怎么做？
## 节流 闭包 
以下场景往往由于事件频繁被触发，因而频繁执行DOM操作、资源加载等重行为，导致UI停顿甚至浏览器崩溃。
 以下场景往往由于事件频繁被触发，因而频繁执行DOM操作、资源加载等重行为，导致UI停顿甚至浏览器崩溃。

  1. window对象的resize、scroll事件

  2. 拖拽时的mousemove事件

  3. 射击游戏中的mousedown、keydown事件

  4. 文字输入、自动完成的keyup事件


http://www.cnblogs.com/dolphinX/p/3403821.html
function throttle(method,context){
            clearTimeout(method.tId);
            method.tId=setTimeout(function(){
                method.call(context);
            },500);
        }

## 跨域 jsonP 如何abort jsonP
abort jsonP的话 设置一个flag 来终止 callback
jsonp 不支持循环条用的解决：

http://www.cnblogs.com/mominger/p/4459712.html
## CORS 
http://www.ruanyifeng.com/blog/2016/04/cors.html
AJAX 只能同源使用
浏览器讲CORS请求分为两种，简单强求和非简单强求，
###请求方法是以下三种方法之一：
HEAD
GET
POST
###HTTP的头信息不超出以下几种字段：
Accept
Accept-Language
Content-Language
Last-Event-ID
Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/plain

不满足以上两个条件的就是非简单请求

###简单请求基本流程

对于简单请求，浏览器直接发出CORS请求。具体来说，就是在头信息之中，增加一个Origin字段。

响应的头部信息字段
### Access-Control-Allow-Origin
### Access-Control-Allow-Credentials
### Access-Control-Expose-Headers

### 非简单请求
非简单请求是那种对服务器有特殊要求的请求，比如请求方法是PUT或DELETE，或者Content-Type字段的类型是application/json。

非简单请求的CORS请求，会在正式通信之前，增加一次HTTP查询请求，称为"预检"请求（preflight）。
浏览器先询问服务器，当前网页所在的域名是否在服务器的许可名单之中，以及可以使用哪些HTTP动词和头信息字段。只有得到肯定答复，
浏览器才会发出正式的XMLHttpRequest请求，否则就报错。

预检请求头部的字段有origin，还有Access-Control-Request-Method，Access-Control-Request-Headers

预检请求的响应的头部字段有：
Access-Control-Allow-Origin
Access-Control-Allow-Methods: GET, POST, PUT
Access-Control-Allow-Headers: X-Custom-Header
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 1728000

CORS 与jsonP做对比，JSONP只支持GET请求，CORS支持所有类型的HTTP请求。JSONP的优势在于支持老式浏览器，
以及可以向不支持CORS的网站请求数据。

## 同源策略 http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html

三种行为受限

（1） Cookie、LocalStorage 和 IndexDB 无法读取。
（2） DOM 无法获得。
（3） AJAX 请求不能发送。

## HTTP2

1.HTTP2是一个彻底的二进制协议
2.多工 客户端和浏览器都可以同时发送多个请求或回应，而且不用按照顺序一一对应，这样就避免了"队头堵塞"。
3.数据流 
4.头信息压缩 引入了头信息压缩机智
5.服务器推送 常见场景是客户端请求一个网页，这个网页里面包含很多静态资源。正常情况下，客户端必须收到网页后，解析HTML源码，
发现有静态资源，再发出静态资源请求。
其实，服务器可以预期到客户端请求网页后，很可能会再请求静态资源，所以就主动把这些静态资源随着网页一起发给客户端了。

使用HTTP2 前必须先启动HTTPS，学名TLS

升级HTTPS步骤：
1.获取证书
2.安装证书
3.修改链接
4.301重定向 将HTTP 协议的访问导向 HTTPS 协议的 



## 首页白屏

## Content Security Policy CSP 

使用CSP来让浏览器禁止外部注入恶意脚本 XSS

## 数组 字符串方法

map
reduce


###数组

###字符串方法

##网页性能
http://www.ruanyifeng.com/blog/2015/09/web-page-performance-in-depth.html

提高网页性能，就是要降低"重排"和"重绘"的频率和成本，尽量少触发重新渲染。
性能角度考虑，尽量不要把读操作和写操作，放在一个语句里面。
样式表越简单，重排和重绘就越快。
重排和重绘的DOM元素层级越高，成本就越高。
table元素的重排和重绘成本，要高于div元素
优化的9条规则：

第一条是上一节说到的，DOM 的多个读操作（或多个写操作），应该放在一起。不要两个读操作之间，加入一个写操作。
第二条，如果某个样式是通过重排得到的，那么最好缓存结果。避免下一次用到的时候，浏览器又要重排。
第三条，不要一条条地改变样式，而要通过改变class，或者csstext属性，一次性地改变样式。
// bad
var left = 10;
var top = 10;
el.style.left = left + "px";
el.style.top  = top  + "px";
// good 
el.className += " theclassname";
// good
el.style.cssText += "; left: " + left + "px; top: " + top + "px;";
第四条，尽量使用离线DOM，而不是真实的网面DOM，来改变元素样式。比如，操作Document Fragment对象，完成后再把这个对象加入DOM。再比如，使用 cloneNode() 方法，在克隆的节点上进行操作，然后再用克隆的节点替换原始节点。
第五条，先将元素设为display: none（需要1次重排和重绘），然后对这个节点进行100次操作，最后再恢复显示（需要1次重排和重绘）。这样一来，你就用两次重新渲染，取代了可能高达100次的重新渲染。
第六条，position属性为absolute或fixed的元素，重排的开销会比较小，因为不用考虑它对其他元素的影响。
第七条，只在必要的时候，才将元素的display属性为可见，因为不可见的元素不影响重排和重绘。另外，visibility : hidden的元素只对重绘有影响，不影响重排。
第八条，使用虚拟DOM的脚本库，比如React等。
第九条，使用 window.requestAnimationFrame()、window.requestIdleCallback() 这两个方法调节重新渲染（详见后文）。

###刷新率

一秒之间能够完成多少次重新渲染，这个指标就被称为"刷新率"，英文为FPS（frame per second）。60次重新渲染，就是60FPS。
如果想达到60帧的刷新率，就意味着JavaScript线程每个任务的耗时，必须少于16毫秒。一个解决办法是使用Web Worker，主线程只用于UI渲染，然后跟UI渲染不相干的任务，都放在Worker线程。

###window.requestAnimationFrame()
window.requestAnimationFrame()，让读操作和写操作分离，把所有的写操作放到下一次重新渲染。
减少渲染的次数
### window.requestIdleCallback()
也可以用来调节重新渲染。
它指定只有当一帧的末尾有空闲时间，才会执行回调函数。 requestIdleCallback(fn);

## JS 封装 多态
多态的基本概念：一个引用类型（变量）在不同情况下的多种状态。
js本身是无态的，天生就支持多态。

封装性：抽象出来的数据和对数据的操作封装在一起，数据被保护在内部，程序的其它部分只有通过被授权的操作(成员方法)，才能对数据进行操作
继承性：继承可以解决代码复用，让编程更加靠近人类思维。当多个类存在相同的属性(变量)和方法时，可以从这些类中抽象出父类，在父类中定义这些相同的属性和方法，
所有的子类不需要重新定义这些属性和方法，只需要通过继承父类中的属性和方法。
多态性：一个引用(类型)在不同情况下的多种状态。也可以理解成：多态是指通过指向父类的引用，来调用在不同子类中实现的方法。
<script type="text/javascript"> 
  // Master类 
  function Master(name){ 
    this.nam=name; 
    //方法[给动物喂食物] 
  } 
  //原型法添加成员函数 
  Master.prototype.feed=function (animal,food){ 
    window.alert("给"+animal.name+" 喂"+ food.name); 
  } 
  function Food(name){ 
    this.name=name; 
  } 
  //鱼类 
  function Fish(name){ 
    this.food=Food; 
    this.food(name); 
  } 
  //骨头 
  function Bone(name){ 
    this.food=Food; 
    this.food(name); 
  } 
  function Peach(name){ 
    this.food=Food; 
    this.food(name); 
  } 
  //动物类 
  function Animal(name){ 
    this.name=name; 
  } 
  //猫猫 
  function Cat(name){ 
    this.animal=Animal; 
    this.animal(name); 
  } 
  //狗狗 
  function Dog(name){ 
    this.animal=Animal; 
    this.animal(name); 
  } 
  //猴子 
  function Monkey(name){ 
    this.animal=Animal; 
    this.animal(name); 
  } 
  var cat=new Cat("猫"); 
  var fish=new Fish("鱼"); 
  
  var dog=new Dog("狗"); 
  var bone=new Bone("骨头"); 
  
  var monkey=new Monkey("猴"); 
  var peach=new Peach("桃"); 
  
  //创建一个主人 
  var master=new Master("zs"); 
  master.feed(dog,bone); 
  master.feed(cat,fish); 
  master.feed(monkey,peach); 
</script> 
多态利于代码的维护和扩展，当我们需要使用同一类树上的对象时，只需要传入不同的参数就行了，而不需要再new 一个对象。

## react 渲染 生命周期 

组件的生命周期：
Mounting：已插入真实 DOM
Updating：正在被重新渲染
Unmounting：已移出真实 DOM

React 为每个状态都提供了两种处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用，三种状态共计五种处理函数。
componentWillMount()
componentDidMount()
componentWillUpdate(object nextProps, object nextState)
componentDidUpdate(object prevProps, object prevState)
componentWillUnmount()

此外，React 还提供两种特殊状态的处理函数。
componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用

## ES6 的模块的循环加载

ES6模块的运行机制与CommonJS不一样，它遇到模块加载命令import时，不会去执行模块，而是只生成一个引用。等到真的需要用到时，
再到模块里面去取值。
因此，ES6模块是动态引用，不存在缓存值的问题，而且模块里面的变量，绑定其所在的模块
这导致ES6处理"循环加载"与CommonJS有本质的不同。ES6根本不会关心是否发生了"循环加载"，只是生成一个指向被加载模块的引用，
需要开发者自己保证，真正取值的时候能够取到值。

## Object.create

<script>
　if (!Object.create) {
　　　　Object.create = function (o) {
　　　　　　 function F() {}
　　　　　　F.prototype = o;
　　　　　　return new F();
　　　　};
　　}
</script>

## 异步编程

1.回调函数
2.事件监听
3.发布/订阅
4.Promises对象

<script>
var promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
</script>

5.generator async

## 模块化 

IIFE
var module1 = (function(){
　　　　var _count = 0;
　　　　var m1 = function(){
　　　　　　//...
　　　　};
　　　　var m2 = function(){
　　　　　　//...
　　　　};
　　　　return {
　　　　　　m1 : m1,
　　　　　　m2 : m2
　　　　};
　　})();

输入全局变量模式

var module1 = (function ($, YAHOO) {
　　　　//...
　　})(jQuery, YAHOO);

对服务器端不是一个问题，因为所有的模块都存放在本地硬盘，可以同步加载完成，等待时间就是硬盘的读取时间。但是，
对于浏览器，这却是一个大问题，因为模块都放在服务器端，等待时间取决于网速的快慢，可能要等很长时间，浏览器处于"假死"状态。

浏览器端的模块，不能采用"同步加载"（synchronous），只能采用"异步加载"（asynchronous）。这就是AMD规范诞生的背景。

因此导出AMD 异步模块定义

require([module], callback);

require(['math'], function (math) {
　　　　math.add(2, 3);
　　});

require.js

（1）实现js文件的异步加载，避免网页失去响应；
（2）管理模块之间的依赖性，便于代码的编写和维护。

<script src="js/require.js" defer async="true" ></script>
async属性表明这个文件需要异步加载，避免网页失去响应。IE不支持这个属性，只支持defer，所以把defer也写上。

## redux

（1）Web 应用是一个状态机，视图与状态是一一对应的。
（2）所有的状态，保存在一个对象里面。

## IntersectionObserver
var io = new IntersectionObserver(callback, option);
IntersectionObserverEntry对象提供目标元素的信息，一共有六个属性。

{
  time: 3893.92,
  rootBounds: ClientRect {
    bottom: 920,
    height: 1024,
    left: 0,
    right: 1024,
    top: 0,
    width: 920
  },
  boundingClientRect: ClientRect {
     // ...
  },
  intersectionRect: ClientRect {
    // ...
  },
  intersectionRatio: 0.54,
  target: element
}




