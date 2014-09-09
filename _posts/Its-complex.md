title: "It's complex"
date: 2014-08-04 23:33:08
tags:
 - Java
 - Ruby
---

事情有点复杂，不知道从哪里说起。因为没什么主题，索性就叫杂感吧。

这段时间又重新学起了Java EE的知识，算作是之前一直没有认真了解的一个代价吧。一个礼拜多的时间看完了Java EE 6 Tutorial，也把有些典型的例子看了看，这次的感觉是原来Java EE还算好，没有想象的沉重，尤其是EJB，新的版本3.1已经算是轻量级的开发技术了。也从网上看了一些评论，主要是Java EE和Spring的比较，如果真的做一个新的企业应用项目，可能还是有点难以取舍。Spring的发展很快，现在已经出到4.0，而Java EE也并不示弱，现在已经有了Java EE 7。从历史上来看，Java EE在较早的版本名声不好，因为过于沉重了，所以Spring顺理成章地赢得了很大的市场，所以现在Java EE想要赢回这场持久战，还真得需要点耐心。一般来说，因为Spring并不受JCP的控制，所以在应用先进思想方面要更敏捷一些，而Java EE涵盖多个JSR的标准更新需要协调各方意见，步调怕是要略显迟缓。另外，Spring集成其他框架的灵活性是Java EE难以比拟的。所以，可能需要考察开发项目的特性，充分了解两种主要框架的能力和缺陷，以作判断。最后一句，Java EE因为包含很多标准来适配企业开发的方方面面，但并不见得在实际的项目都能用到，所以还是要量体裁衣，不要过多的Upfront Design。

<!-- more -->

所以还是要敏捷。说道敏捷，自然就得说生产力。前两天看了一篇文章叫《[痛苦的Java程序员](http://ourjs.com/detail/53dbb5292ee109090700000c)》，其实人家英文根本就没有痛苦一说，只是译者给加上了，不过文章本身确实传递着一种痛苦的情绪，而且最近我确实也觉得Java有点罗嗦了。文中提到的比较重要的两句话，当然稍显偏激，不过也能代表了有些Java程序员的一种感觉：

>每个人都把自己想像成架构师。我在阅读代码的时侯感觉他们不是在解决问题，而是在计划问题。
>Java也迫使一种高水平的形式主义和冗长啰嗦的东西在开发者身上显现。

[Java](http://zh.wikipedia.org/wiki/Java)也出现了近20年了，一种语言在出现20年之后还能在语言流行度排行榜上排名前三也算是非常成功了。不得不说，Java的面向对象与简洁性在当初的语言中脱颖而出，C++太复杂了，C很简洁，但是和Java所关注的领域不一样。Smalltalk会觉得很冤，但是套用Steve Yeggie的话说，Java人家那广告做的好啊，你没辙。所以，时势早英雄，Java胜出。Java在跨平台、互联网应用、企业应用中表现优异，并且最近几年延伸到移动平台的Android，更使这种强类型语言大放异彩。随着Java虚拟机的不断优化，它的性能已经仅次于C/C++，所以它的成功也绝非偶然。

但是Java确实接近中年，老成持重，但也有点过于笨拙。Java冗长的语法在Ruby和Scala面前确实有点不好意思。所以有人说，雇一个Ruby程序员可以干三个Java程序员的活，这话在一定程度上不错。但是，语言各有所长，以己之长攻彼之弱，必然易于取胜，所以选择语言方面更要多加考虑，而不是人云亦云。我的感受是，企业应用或性能要求较高的互联网后台应用还是用Java比较好，而轻量级的网站用Ruby配合Rails则是上佳之选。之前我写过一些关于Scala语言的博客，个人比较喜欢Scala，因为它的好处在于揉合了面向对象编程和函数式编程两种范式，同时又更加简洁轻盈，再配合Play!以及Akka框架的支持，真如同如虎添翼。看好Scala的发展，但并不代表现在Scala有足够的市场，尤其在国内，过于冷门的语言可能会对就业造成不便。另外，Scala复杂的语法学习起来确实比Java困难，所以流行起来真不太容易。

下面有几条Java和Ruby语言的比较仅供参考：

https://www.ruby-lang.org/en/documentation/ruby-from-other-languages/to-ruby-from-java/
http://carlosbecker.com/posts/twitter-drops-ruby-bullshit/
http://a-developer-life.blogspot.com/2013/03/ruby-vs-java.html
http://www.tuicool.com/articles/ZrQBbu
http://stackoverflow.com/questions/442216/java-or-python-or-ruby-for-web-application
http://stackoverflow.com/questions/5083292/playframework-vs-ruby-on-rails
http://blog.codinghorror.com/why-ruby/

如果有机会，还是多看一些优秀的源码，并多参与比较有代表性的应用开发，以体会语言的优势以及解决问题的方式。讨论厘清思路固然重要，但是对于语言的使用其实是存在很多误解的，所以上手实践不失为一个好的鉴别方法。最后，非常推荐Steve Yeggie的《程序员的呐喊》，里面讲了很多关于程序设计的方方面面，喜欢编程的同学一定要入一本！

太晚了，扯到这里，晚安！
