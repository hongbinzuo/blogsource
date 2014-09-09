title: Talk about DI again
date: 2013-11-26 13:10:49
tags:
 - Java
 - DI
 - Design Patterns

---

再谈依赖注入
==========================

理解了控制反转和依赖注入的基本概念之后，就可以了解一些实际的应用了。在《Java程序员修炼之道》第三章，作者深入剖析了依赖注入的技术背景和应用实例。

主要内容包括：

1. 控制反转和依赖注入
2. 掌握依赖注入技术为什么如此重要
3. JSR-330如何统一了Java中的DI
4. 常见的JSR-330的注解，如@Inject
5. Guice 3简介，JSR-330的参考实现

<!-- more -->

其中，一些值得注意的重点是：

1. 依赖注入的好处：松耦合、易测性、更强的内聚性、可重用组件、更轻盈的代码
2. 实际的例子带领读者从不用DI的代码变成使用工厂（或服务定位器）模式的代码，再变成使用DI的代码，是一个不断重构的过程，用到的关键技术是面向接口编程。和Martin Fowler的论述有相似之处。可能对于有经验的Java程序员，最后得到的依赖注入代码是自然而然的。
3. Java标准化DI的由来 JSR-330 & JSR-299
4. 注解：@Inject，@Qualifier，@Named，@Scope，@Singleton以及接口Provider&lt;T&gt;
5. Java中DI的参考实现：Guice 3及其详细介绍

总之，了解依赖注入（DI）在现代Java开发中，尤其对于设计解耦和理解容器中很有帮助，我们不仅要知道其原理和益处，更要熟悉其使用场景和方法。

接下来
-----------------

  - 有时间的话，接下来要探索一下Guice 3的用法和例子，同时了解一下Spring中DI的使用方法。
  - 还有一个问题，除了Java之外，DI在其他语言中是如何应用的呢？（NodeJS的入门教程也提到了Martin Fowler的文章）
  - 除了DI之外，面向对象的其他原则是否在新的Java语言规范中提供支持？
