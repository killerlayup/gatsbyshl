---
title: 中国大学MOOC前端CSS（scss）规范
date: "2017-02-24T22:12:03.284Z"
path: "/cssCodeGuide/"
---


中M前端CSS规范主要参考了[NEC](http://nec.netease.com/standard/css-sort.html)的方案，加上行业流行的css标准规范(主要参照[google](https://google.github.io/styleguide/htmlcssguide.xml))，旨在提高代码质量和协作效率。本规范主要由CSS风格规范，CSS格式规范，组件池css规范和scss规范4个方面组成。



##CSS风格规范

###文件引用和顺序
在页面中我们一般引用两个css文件，先引用通用的style.css,再引用对应页面的css, 如：

````html
<link type="text/css" rel="stylesheet" href="/src/css/web/style.css"/>
<link type="text/css" rel="stylesheet" href="/src/css/web/page/university.css"/> 
````

###"-"连字符
在中M样式规范里，"-"不代表连字符，只表示前缀分隔符或者扩展，见下面规范。

###css内部分类及其顺序
.p- 页面自有的大类，控制本页面样式；注意此大类不会写到公用样式文件里；
.g- 布局大类，定义布局样式，如.g-bd{} ；
.m- 模块大类，定义模块样式，如.m-nav{} ；
.u- 元件大类，定义元件样式，如.u-okbtn{} ；
.f- 功能大类，设置常用样式，如.f-fl{float:left;} ；
.s- 皮肤大类，设置常用的颜色相关的样式，如： .s-fc{color:#333} ；
.z- 状态大类，设置在某种状态下的样式，如： .u-btn.z-dis{} 按钮不可用的状态；经常借助js操作此状态类来实现效果的切换。
.j- 交互大类，空类，只作为给js获取节点的选择器，如$('.j-okbtn')，不做为样式使用。


###分类命名方法
采用NEC的规范，使用单个字母+"-"为前缀，如布局（grid）（.g-）；模块（module）（.m-）；元件（unit）（.u-）；功能（function）（.f-）；皮肤（skin）（.s-）；状态（.z-）。
注意尽量在你样式中的选择器总是要以上面前五类开头，然后在里面使用后代选择器(见下面后代选择器)。
如果这五类不能满足你的需求，你可以另外定义一个或多个大类，但必须符合单个字母+"-"为前缀的命名规则，即 .x- 的格式。
比较特殊的是.j-将被专用于JS获取节点，请勿使用.j-定义样式。

###后代选择器命名
约定在模块或者元件选择器中的生效的，不以单个字母+"-"为前缀的类选择器作为后代选择器。
命名应该简约而不实语义：

````css
 /* bad */
.m-abc .green2 {}
/* good */
.m-list .wrap2 {}
````

###模块和元件的扩展类的命名方法
当A、B、C、...它们类型相同且外形相似区别不大，那么就以它们中出现率最高的做成基类，其他做成基类的扩展。
比如：+“-”+数字或字母（如：.m-list的扩展类为.m-list-1、.m-list-2等）。
基类自身可以独立使用（如：class="m-list"即可），扩展类必须基于基类使用（如：class="m-list m-list-2"）。


###模块和元件的后代选择器的扩展类
有时候模块内会有些类似的东西，如果你没有把它们做成元件和扩展，那么也可以使用后代选择器和扩展。
后代选择器：.m-login .btn{}。
后代选择器扩展：.m-login .btn-1{}，.m-login .btn-dis{}。

###禁止单个字母的类选择器
不允许单个字母的类选择器出现；单字母本身语义上就不清晰，而且在进行扩展的时候，会跟大类的命名方式冲突；

###使用类选择器
尽量使用类选择器，而不要使用ID选择器和标签选择器。
由于ID选择器的唯一性，使用了ID选择器就无法重用样式；
标签选择器会容易引起代码的样式污染，因此需要慎用标签选择器，采用类选择器代替。若一定需要使用标签选择器，则尽量使用
有语义化的标签，如li等。

###限制简写形式的属性声明

在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

- padding
- margin
- font
- background
- border
- border-radius

大部分情况下，我们不需要为简写形式的属性声明指定所有值。过度使用简写形式的属性声明会导致代码混乱，
并且会对属性值带来不必要的覆盖从而引起意外的副作用。

###css Hack
很多不兼容问题可以通过改变方法和思路来解决，并非一定需要Hack，根据经验你完全可以绕过某些兼容问题。
一种合理的结构和合理的样式，是极少会碰到兼容问题的。
由于浏览器自身缺陷，我们无法避开的时候，可以允许使用适当的Hack。

统一使用“*”和“_”分别对IE7和6进行Hack。

````css
/* IE7会显示灰色#888，IE6会显示白色#fff，其他浏览器显示黑色#000 */
.m-list {
    color:#000;
    *color:#888;
    _color:#fff;
}
````
##CSS格式规范

###编码格式
编码统一为utf-8;

###都使用小写
在xhtml标准中规定了所有标签、属性和值都小写，CSS也是如此，切记不要使用驼峰：

````css
/* bad */
.m-list .tipWrap {} {
  display: block;
  height: 100px;
}

/* good */
.m-list .tipwrap {} {
  display: block;
  height: 100px;
}
````

###声明结束
 每行 CSS 都应以分号结尾。

````css
/* good */
.test {
  display: block;
  height: 100px;
}
````

###声明样式块的分隔
在选择器和 {} 之间用空格隔开。

````css
/* good */
.m-box {
  margin-top: 1em;
}
````
###省略值为0时的单位
为节省不必要的字节同时也使阅读方便，我们将0px、0em、0%等值缩写为0。

````css
/* good */
.m-box {
    margin:0 10px;
    background-position:50% 0;
}
````

###引号
省略url引用中的引号，其他需要引号的地方使用单引号。

````css
.m-box {
    background:url(bg.png);
}

.m-box:after {
    content:'.';
}
````

###声明顺序

相关的属性声明应当归为一组，并按照下面的顺序排列：

- Positioning（定位）
- Box model（盒模型）
- Visual（视觉）

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。
其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

如果属性间存在关联性，则不要隔开写。

````css
.m-box {
    position:relative;
    height:20px;
    line-height:20px;
    padding:5px;
    color:#000;
}
````

###规则分隔

````css
.m-box {
    background:url(bg.png);
}

.m-box:after {
    content:'.';
}
````
###注释
注释格式用单行注释

````css
/* 注释文字 */
.xxxx{}
````

##组件池css规范

###样式前缀
组件样式前缀 ux- , 模块样式前缀 mx- , 子系统样式前缀 px-

###嵌套
减少嵌套，嵌套不超过5层，后代选择器不需要完整表现结构树层级，尽量能短则短

###命名规则
借鉴 BEM 规则中B与E连接的规则， 格式如： [Block]_[Element]

#### Block - 功能块简称
#### Element - 元素标签

````html
<form class="ux-form ux-form-primary">
    <input class="ux-form_input" type="text" />
    <input
    class="ux-form_submit"
    type="submit" />
</form>
````
对应的css：

 ````css
.ux-form { }
.ux-form_input { }
.ux-form_submit { }
````

对应的scss：

````css
.ux-form{
    &_input{}
    &_submit{}
    &_submit{
    }	
}
````

##scss规范

中M主要用scss来作为css的预编译，因此在编写scss时除了注意上述基础的css语法外，还需要注意scss的一些规范。

###文件规范

中M主要根据平台将scss分为mobile,org,admin和web四个目录，另外还有公用的common目录，放置一些公用的基础样式。
在对应目录下分别有page,module,ui目录，分别放置对应页面，模块和组件的样式。

###块级内容缩进
为了反映层级关系和提高可读性，块级内容都应缩进。

````css
.m-class {
  display: block;

   .article {
    background-color: #eee;
 
    .title {
      font-size: 1.2em;
    }

} 
````
###嵌套

scss支持嵌套，但是要避免嵌套没有任何内容的选择器。

###嵌套中引入空行

嵌套选择器和CSS属性之间空一行。

````css
.m-class {
  display: block;

   .article {
    background-color: #eee;
 
    .title {
      font-size: 1.2em;
    }
 
    .footnote {
      font-size: 0.8em;
    }
  }
} 
````
###嵌套顺序

嵌套时需要有一个明确的嵌套顺序，可以让代码更加直观简洁

- 当前选择器的样式属性
- 父级选择器的伪类选择器 (:first-letter, :hover, :active etc)
- 伪类元素 (:before and :after)
- 父级选择器的声明样式 (.selected, .active, .enlarged etc.)
- 用Sass的上下文媒体查询
- 子选择器作为最后的部分

````css
.m-class {
  /* 1. 当前选择器的样式属性 */
  display: inline-block;
  padding: 1rem;
  background-color: whitesmoke;
  color: grey;
 
  /* 2. 父级选择器的伪类选择器 */
  &:hover {
    color: black;
  }
 
  /* 3. 父级选择器的伪类选择器 */
  &:before {
    content: "";
    display: block;
    border-top: 1px solid grey;
  }
 
  &:after {
    content: "";
    display: block;
    border-top: 1px solid grey;
  }
 
  /* 4. 父级选择器的声明样式 */
  &.active {
    background-color: pink;
    color: red;
 
    /* 4.2. 父级选择器的声明样式的伪类选择器 */
    &:hover {
      color: darkred;
    }
  }
 
  /* 5. 用Sass的上下文媒体查询 */
  @media screen and (max-width: 640px) {
    display: block;
    font-size: 2em;
  }
 
  /* 6. 子类选择器 */
  .content  .title {
    font-size: 1.2em;
 
    /* 6.5 子类选择器的上下文媒体查询 */
    @media screen and (max-width: 640px) {
      letter-spacing: 0.2em;
      text-transform: uppercase;
    }
  }
} 
````


