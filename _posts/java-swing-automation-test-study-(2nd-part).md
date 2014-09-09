title: Java Swing Automation Test Study(2nd part)
date: 2013-11-19 14:48:59
tags:
 - test
 - Java
---

##Java Swing界面自动化测试初探（下）

本文下半部分主要介绍开源的Java Swing自动化测试工具，评价和注解完全基于个人粗浅理解。

###FEST 

>FEST is a collection of libraries, released under the Apache 2.0 license, whose mission is to simplify software testing. It is composed of various modules, which can be used with TestNG or JUnit.

>Our users include: Google, Square, Eclipse Foundation, Oracle, IBM, Guidewire, and many more!

**评价**：五星
**官方网站**：[http://fest.easytesting.org/](http://fest.easytesting.org/)
**代码下载**：[https://code.google.com/p/fest/](https://code.google.com/p/fest/)
**主要特点**：

  - 功能性Swing界面测试（Functional Swing GUI Testing）
  - 流畅的断言（Fluent Assertions）
  - 流畅的反射（Fluent Reflection）
  - mockito 作为模拟框架（Mock framework）
  - 文档丰富，应用广泛
  - 第四届ATI自动化大奖第一名
  - 没有录播（Record-Play）的功能

<!-- more -->

###Jemmy

**评价**：三星半
**官方网站**：[https://jemmy.java.net/](https://jemmy.java.net/)
**感受**：可能实现了基本功能，但看到网站界面真心不想用！也没有专门的特性列表。它是Netbeans的子项目，但是感觉像后娘的孩子。不过，在SO上看到一些正面评价，有一些其他的自动化测试框架是基于Jemmy，所以框架本身可能有一定参考价值，说不定是有料但不会卖的那种。

###UISpec4J

**评价**：四星
**官方网站**：http://www.uispec4j.org/
**感受**：UISpect4J声称其他已有的库如Abbot、JFCUnit等等的API太像Swing而过于“技术流”，所以它写出来的测试用例可能更简洁易读，面向测试而不是面向开发。从这点上看，很像是行为驱动开发（Behavior Driven Design），这里的行为其实就是系统的界面的迁移说明，这也可能是UI Spec的来源。

###Swinger

**评价**：四星
**官方网站**：https://github.com/demetriusnunes/swinger
**感受**：这可能是一个个人维护的项目，技术支持和稳定性方面有待考虑。使用JRuby开发，基于Cucumber和RSpec写成，所以要先了解[Cucumber](http://cukes.info/)等工具，并了解行为驱动开发的流程。因为Cucumber在业界是有一定知名度的，所以这个也值得一试。

###Fitnesse

**评价**：四星
**官方网站**：http://fitnesse.org/
**感受**：Fitnesse是Martin大叔开发的一款通用的测试工具，业界知名度蛮高。Fitnesse通过插件的方式支持Swing界面测试，也值得尝试。

###Abbot

**评价**：四星半
**官方网站**：http://abbot.sourceforge.net/doc/overview.shtml
**感受**：老牌测试框架。

###JFCUnit

**评价**：三星
**官方网站**：http://jfcunit.sourceforge.net/
**感受**：比较老的测试框架，只支持JUnit，而且2004年后就没与更新，不推荐使用。	
