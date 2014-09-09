title: Java Swing Automation Test Study (1st part)
date: 2013-11-19 00:11:43
tags:
- Java
- test
---

##Java Swing界面自动化测试初探（上）

最近有机会又学习了一下Java自动化测试框架，对于自动化测试有了进一步的了解。自动化测试的效果，业界一直都存在一些争论，不过我理解现在的基本共识是自动化测试（即利用程序实现测试工作）是有用的，至于对不同类型的软件能起到多大的作用就要依情况而定。有的软件项目自动化测试可能可以覆盖大部分场景，有的可能只能覆盖较少部分。前一段时间看Robert C. Martin大叔的《程序员的职业素养》，其中对于测试的重视程度令人印象颇深。Martin大叔花了三章的篇幅来讲述测试，分别是测试驱动开发、验收测试和测试策略。而在测试驱动开发一章中，他谈到自己和Kent Beck的一次会面，看完Kent的展示之后，他说：“这让我目瞪口呆！”。Martin大叔的结论是：“此事已有定论！TDD确实可行。”

当然是否是TDD是开发模式的选择，不一定要强求，但是对于自动化测试的重要性，大家应该是广泛认同的。在Jeff Atwood最新出版的博客文集（中文版译名《高效能程序员的修炼》）中，Jeff引用了J.Timothy King的一篇文章，题为《我同情那些不写单元测试的傻瓜》，并由此而展开了对于测试重要性和方法的探讨，并警示大家，不要因为不喜欢测试驱动就不写测试了，这是非常错误的。自动化测试活动在保障产品质量、提高开发效率和持续交付能起到十分关键的作用。

具体到我们实际的开发工作，Java自动化测试起源较早，敏捷声明的发起人之一、XP方法的倡导者Kent和Erich（《设计模式》作者之一）合作创建了JUnit单元测试框架，在Java世界里享有盛誉并成为事实上的标准。不过，现在还有一个更加流行的选择，TestNG。TestNG不仅在单元测试方面，而且在组件测试方面，甚至在功能和系统测试上都有很大的帮助。当然，本文主要不是讨论测试框架，我们主要讨论Java世界里的界面测试问题。有关自动化测试框架的话题，可参考相关网站。
<!-- more -->
说到界面（GUI）测试问题，一般分为两种，即桌面程序测试和网页程序测试，近几年移动互联网大热，因此移动端的界面测试也可以算作第三种测试类型。现代的Java桌面程序一般都是用Swing写成，因此下文会探索一下基于Swing的界面自动化测试方法。

搜索引擎是信息获取的第一助手，求助于谷歌，我们可以按图索骥，了解最新最好的工具，通过这些工具，我们就能知道具体的测试方法，并进行比较，选择适合自己的工具和方法。

因为现在TestNG比JUnit功能更强大，我们使用关键词“testNG”和“GUI”，可得到和TestNG结合的工具abbot，文章来自IBM DeveloperWorks：[追求代码质量: 使用 TestNG-Abbot 实现自动化 GUI 测试](http://www.ibm.com/developerworks/cn/java/j-cq02277/)，其中谈到了使用TestNG和Abbot结合进行Swing测试的基本方法和例子，不过这篇文章发表于2007年，可能有点老了。搜索“TestNG abbot”，找到[官方网站](https://code.google.com/p/testng-abbot/)，果然已经更名为FEST，并具有[更多新特性](https://code.google.com/p/fest/)，在这里基本上可以找到FEST的一切！当然，都是Open Source的，Bingo！

如果你对Java Swing自动化测试原理或底层机制感兴趣的话，可以读读这两篇文章：[GUI自动化测试原理剖析](http://developer.51cto.com/art/201106/267055.htm) & [Automated UI testing with Swing & FEST](http://tuhrig.de/automated-ui-testing-with-swing-fest/)。

做程序员从来都不会满足于一个工具，所以我们看看还有什么别的选择，探索下去，又看到两个耳熟能详的名字：IBM Rational Functional Tester以及HP QuickTest Profressional（QTP），这些都是收费软件，就不多展开了，下文中也不再涉及商业软件。更加全面的测试框架比较，可以参考维基百科的[列表](http://en.wikipedia.org/wiki/List_of_GUI_testing_tools)。另外，通过继续在Stackoverflow上搜索，可以找到类似的文章，如[Java Swing界面自动化测试的问题](http://stackoverflow.com/questions/91179/automated-tests-for-java-swing-guisi)等等，本文下半部分着重总结一下我的发现。
