title: Understanding Spring
date: 2014-08-06 23:08:50
tags:
 - Java
 - Spring
---

今天在公司做了一个Spring入门的介绍，感觉思路值得总结一下，可能对于以后深入理解类似主题有些帮助。

在多年以前的一个公司，我曾经参与过一段时间的Java企业应用开发，如果没有记错的话，应该是电信工单运维类的项目。我那时还比较青涩，对于Java企业开发以及相关框架和架构都理解的不深。当时组里有个架构师，是他主持了开发的设计决策，应该选的就是Struts/Spring/Hibernate这个经典组合。但是，项目持续的时间并不长，再加之任务繁杂，而我主要负责写前端页面实现，所以对于这些框架开发的精髓也并没有特别深入的了解，有点遗憾。但就是在这个项目，我认识的这位架构师，非常推荐阎宏的书《Java与模式》，所以我听从他的建议买了这本书，我的评价是：如果用Java语言做面向对象设计，这本书到现在依然有较高的阅读价值。

<!-- more -->

再往前的话，我的经验也仅限于写Java应用以及Servlet和JSP，所以总体上对于Java企业应用的开发经验确实有限。

这几年公司内部有些机会用Java开发Web类或移动类项目，Spring就能派上用场了。不过，事情总有两面性，项目开发的时候因为时间紧任务重，虽然通过网络学习到一些快餐式的知识并迅速应用到项目中去，但是往往系统性的理解并不够。趁着现在有一点时间，我索性把《Java EE 6 Tutorial（Basics）》（英文版）和《Spring in action》（第三版，中文）看完了，同时也看了一本叫《Servlet/JSP笔记》的书复习一下Servlet和JSP。在这三本书的基础上，我又通过搜索引擎，以及Slideshare和Stackoverflow等网站寻找合适的讲解材料，最后促成了三个介绍性的讲解：Java EE入门，Servlet/JSP/JDBC介绍以及Spring入门。

这三个讲解风格不一样，具体到Spring的讲解，我是今天上午写的Slides，下午讲。写Slides就是厘请思路，也就是用Powerpoint描述出讲解的主线。Spring的思想现在理解起来并不复杂，但是要把这些思想串起来还是需要费一点功夫，昨天下午我已经在开始想，今天上午动笔，下午讲解，还算顺利。只是讲解的东东可能不够生动丰满，下次争取提高。以下是基本思路：

* 重新看完《Spring in action》的第一章，然后用关键词描述出Spring的历史、出现的原因以及想要解决的问题
* 同时在《Spring in action》书中找到Spring的四条关键策略，个人认为这是理解Spring框架的要领
* 在Slideshare上寻找合适的材料，最终从中挑选出3个左右
* 展开Spring，主要分为DI和AOP，针对DI和AOP分别寻找合适的材料
* DI：因为之前了解过DI，这次是复习，所以讲解起来没又太大障碍，只是补充一些DI的周围知识
* AOP：这个方面了解的不多，因为只讲思想，所以还能蒙混过关，同时找到了一个Slides讲的不错，可以作为以后进阶的参考
* 另外想到，如果直接讲DI又有点仓促，所以又加上面向对象设计的原则和一些相关的设计模式作为背景补充
* 这次主要是入门介绍，所以不涉及Spring的太多细节，细节以参考资料的方式给出

至此，基本主线完成。至于后续的学习和分享，则需要更多的实操以加深理解。是以为记。
