title: SBT真的简单吗？
date: 2014-02-13 23:50:13
tags:
 - Scala
---

正在学习Twitter的Scala教程，前面的基础部分就是复习，相对容易理解一些。一看到Advanced Types这一节，尤其是后面的部分就有点缺氧。终于熬着算是看完了这一节，心想：这下轻松了，看看SBT（Simple Build Tool），动手实验一下，没有那么多抽象概念了，多好！谁知道还是想错了，SBT并不简单。
<!-- more -->

头一个问题是Twitter的[SBT教程](http://twitter.github.io/scala_school/sbt.html)已经过时了，这应该是版本0.7的教程，而现在的最新版本是0.13.1，相比之前的版本改动较大。没关系，简单搜搜就能找到一篇比较清晰的[中文教程](https://github.com/CSUG/real_world_scala/blob/master/02_sbt.markdown)，这篇教程真是不错，写得很详细很全面，基本可以了解SBT的背景、特性以及具体用法等等。

按照这篇中文教程，尝试在电脑上安装运行之。SBT本身安装在Windows/Mac倒都没什么问题，只是正如教程中所强调的从0.7之后，SBT交互工具不再自动创建项目的目录结构了，这个让人很是不爽！居然还要使用什么giter8来下载项目模板什么的，真是不让人省心（StackOverflow上有位大神儿总结了替代方案，详见[此贴](http://stackoverflow.com/questions/5910791/scala-application-structure)）。当然了，我还是免不了要试一下，结果是：不怎么顺利。这时候我就想起来Rails，哎，甭管快慢，易用性上真是有差别啊！

SBT毕竟只是一个构建工具，到这里得想想它到底是否值得我投入更多时间来研究了，原因有两个：现在还没有具体的Scala项目能用到SBT的诸多特性；除了SBT之外是不是还有更容易、更高效的工具？答案是有的，那就是Gradle！见[此贴以及相关评论](http://stackoverflow.com/questions/11061938/comparing-sbt-and-gradle#)，下面引用一位小神儿的回复，我一下就释然了：

>SBT in some sense is like a Vim: if you grok it, you'll be pleased. 

Ant，Maven，Gradle，应该是这个节奏吧？hmm，下一步有空要学习[Gradle](http://www.gradle.org/)咯！太晚了，碎觉。