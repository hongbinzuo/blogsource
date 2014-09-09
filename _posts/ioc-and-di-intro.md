title: IoC and DI intro
date: 2013-11-22 22:43:57
tags:
  - IoC
  - DI
  - Design Patterns
---


##控制反转与依赖注入导读

早年参加工作的时候，大家普遍说，不一定要掌握那么多语言细节，也不一定要学那么多语言，需要的时候查查书、上上网就行了，重要的是“编程思想”。好高级啊！“编程思想”这个当年流行的词儿似乎代表着“高端大气上档次”，似乎意味着掌握编程思想的人都是码农界的高富帅。呃，编程思想，嘛玩意儿？难道就是一系列系统的想法精粹，就像《毛泽东思想》吗？好像不是。后来捧读了巨著《C++编程思想》和《Java编程思想》，也没窥透所谓的思想。后来才觉着，在编程界，英文里可能就不存在思想的准确对应词吧？Idea？Thought？Thinking？Ideology？都不像。

最近在看[《Java程序员修炼之道》](http://book.douban.com/subject/24841235/)（我最近是迷上各种“道”了），其中提到了DIP，又激起我重新厘清编程思想的机会。现在想来，编程，或者说程序设计的思想，应该可以归在设计方法学之下，即有了某种方法，按照这种方法去思考问题、构建软件和设计程序，就是这种方法的思想，比如面向过程的设计思想，或面向对象的设计思想。现在，我们也可以说面向组件的设计思想，或者是面向云的设计思想，甚至是用户体验至上的设计思想。我们不自觉地从“编程”思想演进到“设计”思想了，思想总算正本清源，设计需要思想，而编程只是设计的结果。设计在哪儿？设计无处不在。软件设计从需求获取阶段就已经开始，直到程序员编写每一行代码都贯穿始终，只是体现在设计的不同层面而已。所以，程序员的80%的工作都是在设计（Think&Design），而只有20%的时间是在编程（Programming）。
<!-- more -->

说多了题外话，今天的主题是IoC和DIP。在《Java程序员修炼之道》提到了IoC，并引用了Martin Fowler大师2004年的文章[控制反转容器和依赖注入模式](http://martinfowler.com/articles/injection.html)，于是我花了一点时间细读了这篇文章，文章本身较长但值得一读，核心思想是澄清控制反转和依赖注入的关系，给出依赖注入的起源、定义以及具体类型描述，并且比较了依赖注入和服务定位子（Service Locator）的异同以及应用中的选择考虑。文章本身对于理解依赖注入是很有帮助的，不过我可能更喜欢最简洁的方式来描述概念本身，所以我先后翻阅了阎宏的[《Java与模式》](http://book.douban.com/subject/1214074/)以及Robert C. Martin的经典之作[《敏捷软件开发》（2003）](http://book.douban.com/subject/1140457/)，我个人比较喜欢Robert Martin给出的定义（书中称作依赖反转）：
>a. High-level modules should not depend on low-level modules. Both should depend on abstractions.
b. Abstractions should not depend on details. Details should depend on abstractions.

三位前辈Fowler, 阎宏和Martin大叔都把控制反转和依赖注入从不同侧面解释地非常详细。Fowler的解读清晰明确，把IoC和DIP的概念澄清，并针对容器（如PicoContainer或Spring）的应用给出了范例。阎宏从面向对象的角度“针对抽象、针对接口编程”，给出了Java的范例。而Martin大叔行文畅快，短短几页也把DI的思想表述清楚，所以都可以作为理解上的参考。如果只读一篇的话，我推荐Martin大叔。

当然，不能忘了互联网，查阅基本概念，快速了解基础知识，维基百科是我们的好朋友，下面给出链接，

  - [中文维基关于控制反转的定义](http://zh.wikipedia.org/wiki/%E6%8E%A7%E5%88%B6%E5%8F%8D%E8%BD%AC)
  - [English Wikipedia about Inversion of Control](http://en.wikipedia.org/wiki/Inversion_of_control)
  - [English Wikipedia about Dependency injection](http://en.wikipedia.org/wiki/Dependency_injection)

Stackoverflow上也有关于概念的澄清和讨论：

  - [What is inversion of control](http://stackoverflow.com/questions/3058/what-is-inversion-of-control)
  - [What is dependency injection](http://stackoverflow.com/questions/130794/what-is-dependency-injection?rq=1)

从IoC和DI的学习和讨论中，我们可以看到诸多想法的交汇，无论是大师级的人物，还是普通的程序员，都在使用相似的语言沟通，那就是通过特定的原则或模式来实现某种设计的思想，具体到IoC/DI，就是如何使用面向对象的设计方法，来提高软件复用性、减少耦合（依赖）以及使用高级语言的特性实现软件开发的灵活性。这可能就是思想的真正意义！

IoC和DI只是面向对象设计的五个原则之一，如果想全面了解五个原则，可以参考《敏捷软件开发》。

至此，对于IoC和DI算是有了一个初步的了解，知行合一很重要，下面有几种方式可以让理解更加深刻：

  - 阅读或参考Spring关于IoC/DI的源码解析
  - 找到自己从事项目中现有源码，看是否有相似实现
  - 写1～2个例子
  - 和其他人探讨

###进一步阅读

  - [Fowler的另一篇关于InversionOfControl](http://martinfowler.com/bliki/InversionOfControl.html)
  - [Spring IoC原理（中文）](http://blog.csdn.net/it_man/article/details/4402245)
  - [Robert Martin关于DIP的文章](http://www.objectmentor.com/resources/articles/dip.pdf)，和《敏捷软件开发》中内容相似

