title: GORM查询
date: 2014-01-28 13:53:21
tags:
 - grails
---

GORM是Grails中的一项关键技术，也就是Grails的ORM层，对底层的Hibernate进行了包装，提供了特定的语法，并兼容原有的数据>库查询方式如HQL等。

根据官方推荐的教程[GORM Recipes](http://timsporcic.github.io/GORM-Recipes/)，我们可以逐步了解如何使用GORM的方式进行
数据库表的操作（教程的例子中使用了两个表，是一对多的关系），并举例说明了如何执行常见的SQL查询。由于原来的test-bed代
码是基于Grails 2.0.4的，如果直接下载使用会报错，所以我用`grails create-app`新建了一个项目，然后把相关代码导入到这个
新项目中就可以运行了。除了框架之外，实际上主要是`BootStrap.groovy`和domain中的`Artist.groovy`、`Work.groovy`三个文>件作为支持代码。我把原来教程的脚本练习了一遍，并把联系的脚本源码放到scripts目录中，然后fork了一个repo，地址在：[GORM Recipes for Grails 2.3.5](https://github.com/hongbinzuo/GORM-Recipes)，可供参考。
<!-- more -->
GORM怎么样呢？我把原作者的看法翻译如下：

>Grails 2.0中的GORM功能极其强大，同时又极其令人费解，特别是对于有SQL背景的人来说。不过，和Java一样，你可以用多种方>式完成一个任务。作为GORM中最简单的功能，动态查询器（dynamic finders）提供了一种简洁易用的执行通用查询的方法。除此之
外，GORM的where查询提供了强有力的语法来处理不同类型的查询，而我之前则更倾向于使用SQL。

我个人的看法也很相似，简单的查询可能用动态查询器更好，而复杂一些的因为GORM的where查询比较丑陋，不如使用HQL简洁清晰>。无论如何，GORM提供了更多选择，是否使用则取决于开发者的偏好。

###Grails的几个小坑儿

 - 出错的时候反应很慢，而且出错后使用`Ctrl+C`也很难退出
 - 编译较慢，所以要减少重新编译或者加载环境的操作
 - Windows环境下grails交互窗口的命令不能上下翻页
 - 出问题之后，因为用的人较少，不太容易很快找到解决方法

Grail的学习就暂时告一段落了，相比Rails来说，还是Rails的使用体验更胜一筹，不过对于Java平台的Web开发来说，Grails确实>对开发效率的提升有一定的帮助。但是，由于其流行度不高，具有此技能的开发者较少，网上资源也并不丰富，所以采用之前还是>需要多加考量。好的方面呢，Groovy/Grails的学习成本并不高，具有Java/Spring相关知识的开发者使用起来并不困难，所以应用>在小项目快速开发、制作原型以及补充开发都是可以的。

最后，附Curious Coder的[一份报告](http://zeroturnaround.com/rebellabs/the-curious-coders-java-web-frameworks-comparison-spring-mvc-grails-vaadin-gwt-wicket-play-struts-and-jsf/)，报告针对于Java平台的几大主流Web框架进行了评测，并给
出了一些建议。

