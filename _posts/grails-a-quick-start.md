title: Grails初体验
date: 2014-01-22 16:17:09
tags:
 - grails
 - Java

---

Groovy脚本语言由于之前提到的诸多新特性，可以作为JVM平台上Java语言的有力补充，对于熟悉Java语言的开发者无疑是个好消息：能使用非常近似的语法而代码生产力数倍提升，何乐而不为？Groovy语言可以应用在不同的领域，当然因为互联网的缘故，网站应用是语言发展必须要考虑的重点，这也就是为什么[松本行弘](http://zh.wikipedia.org/wiki/%E6%9D%BE%E6%9C%AC%E8%A1%8C%E5%BC%98)在[《代码的未来》](http://book.douban.com/subject/24536403/)中提到，由于Rails的流行才使得Ruby语言逐渐火热起来。Grails便是在这种背景下产生的基于Groovy语言的Web开发框架，顾名思义：Grails即为Groovy plus Rails，所以可以理解为JVM平台下的Rails框架。
<!-- more -->

根据Grails[官方网站](http://grails.org)的[指南](http://grails.org/doc/latest/guide/gettingStarted.html)，可以非常容易地下载安装。基本的要求对于Java开发者是非常简单的，只需要配置`JAVA_HOME`和`GRAILS_HOME`然后解开下载包就可以运行了。

<img alt="grails命令窗口" src="/img/grails_cmd.png" style="width: 600px;"/>

按照指南的要求，在grails交互命令窗口创建一个Controller并在网页上显示Hello World!，都是很直观的。

浏览通过`grails create-app`创建的样板应用（Scaffolding）可以使用一般的编辑器或者大型的IDE。对于轻量型编辑器，我倾向于使用Sublime Text 3，而IDE的话，因为IntelliJ是花了钱的得多用用要不就亏了。Sublime Text倒没什么好说的，只是我用的IntelliJ 12.1.4对于最新的Grails 2.3.5支持的不好（IntelliJ也不是万能滴），出现Grails不能执行的问题，网上也有人问相似的问题，找来找去费了些时间，最后的答案却很简单，删除grails目录下dist里的`*-sources.jar*`和`*-javadoc.jar*`即可，如[本链接](http://grails.1312388.n4.nabble.com/Grails-2-3-0-RC1-and-IntelliJ-IDEA-quot-IDEA-hook-Grails-not-found-quot-td4647657.html)的最后一贴所示。这个小问题解决之后，IntelliJ还是很给力的，加油！

看Grails创建的Web App目录结构，总有一种似曾相识的感觉，比较像融合了rails和Spring风格的应用，也不奇怪，Grails就是以Spring为基础的类Rails框架。

Grails的开始指南主要告诉大家怎么下载、安装、配置以及运行Grails，用Grails写一个Hello World，并说明了grails交互命令的一些用法。如果想继续深入了解，以下资源或许有些帮助。（Grails的资源在08/09年比较活跃，之后就变少了，如IBM developerworks）

 - [Grails官方网站](http://grails.org/)
 - [Grails教程入口](http://grails.org/tutorials)
 - [Grails on InfoQ](http://www.infoq.com/grails)
 - [Groovy&Grails on SkillsMatter](http://skillsmatter.com/go/groovy-grails)

另外，在运行grails交互命令的过程中，总是能隐隐地感受到Java的稳（ben）重（zhuo），初步的感觉是从开发的效率方面可能不如Rails，不过应该会好于Spring。下面贴一张Google趋势图，看看随意选取的几个主流Web开发框架的热度，结果是：Grails这么多年了还是非主流，呵呵。

但另一方面，我们看Grails的东家[Pivotal](http://www.gopivotal.com/)，貌似是一家高端大气上档次的公司，所以学学现代化的JVM平台的Web框架也没什么坏处哦！:-)

<img alt="Web开发框架流行趋势" src="/img/grails_trend.png" style="width: 600px;"/>
