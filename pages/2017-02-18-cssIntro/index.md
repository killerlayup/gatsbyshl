---
title: CSS 高级特性盘点
date: "2016-12-14T22:12:03.284Z"
layout: post
readNext: "/cssIntro/"
path: "/netlify/"
---



现在随着部分网站逐渐不支持IE8及以下浏览器，如天猫，知乎等，IE8及以下版本的浏览器已经慢慢退出历史舞台，我们在写前端样式css时，可以考虑使用那些旧浏览器不能支持的CSS特性。另外，在移动适配页上，由于没有IE这个历史包袱，浏览器支持一些高级的CSS特性（安卓低版本的浏览器除外），没有必要还使用原来那一套web端老式的CSS特性，我们需要与时俱进。
由于教育产品部目前还需要支持IE8，所以基本上都是在移动适配页上使用一些新的CSS特性

##1. CSS结构和布局
以往传统的CSS 布局，主要依赖display+position+float来布局，该方式浏览器兼容性高，但是对于一些特殊需求的布局，往往很费劲。现在来试试一些高级的布局技巧

###（1）使用flex布局
这个布局方式在前端微专业上魏老师着重讲过，它是一种自适应的布局方式，基本上在高版本浏览器上都会支持。虽然它属性很多，但是只需要记住常用的一些，就很轻松方便的写出以前css比较纠结的布局，比如自适应多列布局和盒元素垂直居中的问题：

####demo
http://codepen.io/killerlayup/pen/rWbWYm

flex有很多相关的属性，具体可以参阅w3c文档或者前端微专业或者[阮老师的博客](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

###（2）calc布局
calc是从字面上看就是calculate的缩写，可以理解为css3的一个类似calculate函数的功能，它可以动态指定元素的长度。所谓动态，是其可以使用百分比来计算长度，比如````width: calc(100% - (20px ) * 2)````，这样在一些流式布局或者自适应不等宽多列布局上非常方便。

####demo
http://codepen.io/killerlayup/pen/ObGbze

###（3）使用vm和vh还是rem

现在在工作中，基本使用田翔分享的[移动适配方案](http://ks.netease.com/blog?id=5298)基于viewport与rem的适配，其实vw和vh也可以达到相应的效果。vw和vh是CSS3中的单位，1vw和1vh分别代表viewport的宽度和高度的1%，如果设定了viewport的长度就是设备的长度````<meta name="viewport" content="width=device-width, height=device-height">````，那么就可以让元素自适应于设备的长度，因此可以在布局适配的时候可以起到很好的效果，比如实现全屏滚动的效果：

####demo
http://codepen.io/killerlayup/pen/aBxBPY

vw和vh在布局上方便很多，但是为什么一般还是使用rem而不使用vw呢？rem和vw的主要区别在于兼容性，vw的兼容性很不好，我们可以用http://caniuse.com/#search=vw来比较vw和rem的兼容性效果，如图：


可以看到vw的浏览器兼容性非常差，很多重要的浏览器都不支持，这大概也是为什么我们都使用rem而没有使用vw吧。

###（4）使用CSS3选择器来布局
巧用CSS3选择器也可以在一些布局上起到神效，比如这些伪类选择器：

````:nth-child(),:nth-last-child(), nth-of-type, nth-last-of-type(), :last-child, :first-of-type, :last-of-type, :only-child, :only-of-type, :empty````

都可以使用起来，比如nth-child()可以匹配其父元素的第N个子元素，:empty可以匹配空元素等。另外，像这类选择器强大的地方在于是它可以支持an+b的表达式，比如nth-child(2n)，可以选择偶数个子元素，因此在使用上可以非常多样化，实现以前需要js支持的功能。

##2.一些css3样式技巧
（1）chrome浏览器不支持12px以下字体的解决方案
可能大家都知道，新版的chrome浏览器不支持小于12px字体显示，当font-size设置小于12px时，在chrome里显示都是12px大小，这在一些英文字体显示上，就有可能会影响视觉效果。而chrome又是占有率最大的浏览器，有必要解决。这时我们可以使用-webkit-transform : scale()来解决。比如我们需要显示10px的字体，那么可以这样解决:
````css
font-size:10px;
-webkit-transform:scale(0.84);
````
这里需要注意的问题是，transform:scale会对整个元素都进行放大缩小，因此会把背景（如果有的话）也同时缩放，需要避免，因此一般会在需要缩放的字体上加入span标签，并且设置display为block或者inline-block, 因为transform:scale只对可以定义宽高的元素有效，具体看demo：

http://codepen.io/killerlayup/pen/bBJBJE

###（2）弹性滚动（滑动）
在一些子元素高度超出父元素高度的情况下，有时候我们需要子元素在父元素里滑动来显示，这个时候如果想要做到跟native一样的流畅弹性滑动，需要设置以下属性:
````css
overflow: auto;
-webkit-overflow-scrolling: touch;
````
其中overflow-scrolling是CSS3针对ios版本的新属性，可以激活ios平滑滚动

###（3）显示多行文本溢出
我们知道单行显示溢出处理通常使用以下css代码：
````css
overflow: hidden;
text-overflow: ellipsis;/* 当字符串超过规定长度，显示省略符*/ 
white-space: nowrap;
````
但是对于如下图需求，课程名称需要两行显示，多余两行的用省略号表示，则比较少见。



我们可以添加一个-webkit-line-clamp属性来解决。该属性仅在webkit的浏览器上有效，而一般移动端都是webkit内核的，因此可以很好的兼容：

####demo

http://codepen.io/killerlayup/pen/vyMgBw

###（4）尽量使用CSS3动画

我们知道，在用js操作DOM来实现动画效果时，会有很大的性能损耗，主要是由于它会引起浏览器的重绘和重排。而使用CSS3的一些属性，则可以避免重排。如何来判别CSS属性是否会触发重绘和重重排，可以使用https://csstriggers.com/这个网站来查看。比如利用transform来实现动画，它只会触发重绘，不会触发重排，因此实现的动画性能就比js操作DOM要好。





###（5）提高CSS3动画性能



为了增加动画性能，一般可以开启3D硬件加速：

````css
-webkit-transform: translate3d(0, 0, 0);

-moz-transform: translate3d(0, 0, 0);

-ms-transform: translate3d(0, 0, 0);
transform: translate3d(0, 0, 0);

还有如果在动画中出现闪烁现象，可以设置
-webkit-backface-visibility:hidden;
backface-visibility:hidden;
-webkit-perspective: 1000;
perspective: 1000;

````

它可以设置动画元素只渲染面向用户的一面，减少性能损耗。

参考资料：

- 阮老师博客：http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html
- 田翔分享:http://ks.netease.com/blog?id=5298
- caniuse:http://caniuse.com
csstriggers:https://csstriggers.com/
- 更平滑的动画：https://www.w3ctrain.com/2015/12/15/smoother-animation/


