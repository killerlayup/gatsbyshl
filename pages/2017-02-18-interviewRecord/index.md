---
title: 微店和爱客仕的面试
date: "2017-02-18T22:12:03.284Z"
path: "/interviewRecord/"
---

最近找工作，记录下在微店和爱客仕的面试过程。

##爱客仕

两个面试官，应该是一个主管一个技术吧，都是技术提问的，基本上是聊天的性质，内容主要是围绕着简历上的点，
由于是聊天的性质，很多内容也记得不是很清楚。
首先是聊着简历上对应的项目经验，工作内容，项目部署，打包，模块加载和组件的一些问题。
说到组件化，问了regularJS的渲染原理，VUE组件的渲染步骤，vuex的工作原理和思想。网易这边主要的开发框架是NEJ，
组件是使用了regular来写。
接下去主要聊了前后端分离，还有ajax保存url信息(用pushState)等，还有跨域啊啥的，反正也都是点到为止。
最后就介绍了他们工程的一些内容。

个人感觉在面试过程中，面试官的提问都是根据简历上的点进行逐一提问，广度是到了，但是问的也不是特别深。

##微店 

微店前后有三个技术来面我，第三个是前端的leader，还有最后的HR面试。整体感觉还是比较放松的，但是相比较爱客仕来说，
他们虽然也问的比较随意，但是很有深度。
第一个面试官主要问了我关于项目的内容和经验（老生长谈），然后就开始问比较深的问题，前端页面渲染优化，超长列表优化，
比如滑动中销毁滑动过的dom,如何将销毁过的数据保存下来？
比如如何解决首页白屏的问题（又是老生长谈的问题），被问到过很多次，还有如果判断css特性是否被浏览器支持（不使用判断浏览器类型的情况下），
还有如何用JS编译出一个让所有浏览器都兼容的CSS，比如css3的一段代码，通过js编译成浏览器通用的版本。另外还问了在输入框上
激活光标，如何让页面滚动，让光标出于页面中间，还有如何判断适配页数字键盘的高度。最后还问了一个跨域的问题，总体上 感觉
他提问是很随意的，但是都问的很深，比较难直接回答出来。
第二个面试官比较常规，根据简历一个条目一个条目提问的，我回答的还可以。比较印象深刻的是问了我boxing-sizing,BFC
的一些问题，还要ES6的一些新特性，比如generator还有async，还有promise等(JS异步)，还问了我react和vue的组件生命周期
第三个面试官是微店前端部门的leader，这个就大部分泛泛而谈了。主要问了云端构建(其实不是问，主要是讲述了他的一个想法)，还有
如果有很多个if-else,如何优化和重构，说是用到了多态的思想，不太懂。还有就是问了css的规范还有css写法对性能的影响等等
最后是HR面试了，也就不赘述了。


##阿里飞猪

阿里飞猪是电话面试，一开始也是聊项目啥的，项目结构，打包，模块加载，组件等等，问了前后端分离思想，组件化思想。由于网易
只是在工作流程上实现了前后端分离，但是并没有在代码结构上彻底分离，所以还是会有freeMark模板的存在。所以我说道我们现在仅仅是用ftl
来作为页面的入口，真正的页面渲染是通过js加载组件来完成的。但是这样其实会有个问题，如何解决首页白屏的问题，他就提到了这个问题。我
当时回答是在ftl中塞用于占位的元素和数据，其余可以用js来做。其他的也没有想出更好的方案，然后它就问了自动化流程上的实践，
还有avalon,vueJS还有angularJS的数据双向绑定的机制，还有react的生命周期，avalon兼容IE6的黑魔法等等。最后还问了我跨域的问题，
jsonp和cors的事先，有哪些资源是不跨域的，还问了节流的实现方式等等。这些基础问题中还是有不少坑的。需要回去好好总结下，

##阿里飞猪二面

飞猪二面，一开始问了我css3的一些特性，比如css动画，如何开启硬件加速，还有问了移动适配的方法，flexible的方案的具体原理（rem->px）,
q清楚浮动的方法。。还有css3的伪类等等
重绘和重排，还有好像问了left 和100px的区别，反正没答上来。。然后手写代码，写四个元素等分排列布局的方法，快排，冒泡，选择排序的方法，
还有正则表达式等等，还问了react的渲染机制（又问）...