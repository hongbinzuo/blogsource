title: Gradle 1-2-3
date: 2014-02-17 22:06:47
tags:
 - Java
 - Gradle
---

上一篇提到了Gradle，没想到这么快就用上了。Twitter的Scala教程<sup>1</sup>基本看完之后，就开始看[《Scala in Action》](http://www.amazon.com/Scala-Action-Nilanjan-Raychaudhuri/dp/1935182757/ref=sr_1_1?ie=UTF8&qid=1392621526&sr=8-1&keywords=scala+in+action)<sup>2</sup>了，作者在书的第二章给出了一个例子：用Scala写一个Http客户端，实现命令模式的REST请求交互，在例子中作者使用了Jetty/Maven构建后台的Java Servlet。我想这是一个学习Gradle的好机会，于是就有了*Gradle的1-2-3*作为入门篇。
<!-- more -->

Gradle作为新一代的自动化构建（Build）工具，主要以简洁、实用为主，相比Maven冗杂的XML语法，Gradle使用了Groovy语言<sup>3</sup>作为构建DSL（[Domain Specific Language](http://en.wikipedia.org/wiki/Domain-specific_language)）使得代码量大幅减少，增强了可维护性。Gradle的官方网站上简要地描述了Gradle的使命：

> Gradle is build automation evolved. Gradle can automate the building, testing, publishing, deployment and more of software packages or other types of projects such as generated static websites, generated documentation or indeed anything else.

> Gradle combines the power and flexibility of Ant with the dependency management and conventions of Maven into a more effective way to build. Powered by a Groovy DSL and packed with innovation, Gradle provides a declarative way to describe all kinds of builds through sensible defaults. Gradle is quickly becoming the build system of choice for many open source projects, leading edge enterprises and legacy automation challenges.

一句话总结就是：Gradle是一种更加高效的构建方式，和Ant一样强大和灵活，同时兼有Maven的依赖管理和约定（Convention）特性。 InfoQ上Maven专家许晓斌也对Gradle做出了比较全面的介绍，中文全文请戳[这里](http://www.infoq.com/cn/news/2011/04/xxb-maven-6-gradle)。

好，让我们开始Gradle之旅吧！（以下操作在OS X 10.9.1上完成）

首先，到Gradle的[官方网站](http://www.gradle.org/)上下载Gradle的安装包。现在的最新版本是1.11，我们下载最新的gradle-1.11-all.zip（包含执行文件、源代码和文档），然后解压缩。整个下载、安装和设置的过程可以参考[官方指南](http://www.gradle.org/docs/current/userguide/installation.html)，非常清楚。简要总结一下：确认Java环境已经安装（如果没有，呃，我相信你造该怎么做），下载解压之后设置环境变量`GRADLE_HOME`，并在PATH目录中加入`$GRADLE_HOME/bin`，这样`gradle`命令就可以在任何地方运行了。最后运行`gradle -v`检查是否设置正确。

接下来，我们通过浏览文档中[关于Java项目的部分](http://www.gradle.org/docs/current/userguide/tutorial_java_projects.html)简单了解一下Gradle是怎么管理Java项目的。Gradle使用插件的方式扩展功能，使用任务的方式进行构建过程管理（这些概念听起来是不是很熟悉），使用Groovy进行配置，总体掌握起来比Maven要容易一些。下面，我们参考[这篇博文](http://codetutr.com/2013/03/23/simple-gradle-web-application/)来构建一个简单的Java Web项目。

在这个例子中，首先要构建一个基本的项目目录（有没有一条命令就可以完成的方法呢？），要符合Java Web项目构建的约定。然后在项目的根目录中创建`build.gradle`，其中指定了需要应用的插件，包含`java`、`war`、`jetty`和`eclipse-wtp`，以及代码库（使用Maven的Central库）和具体的依赖。在`web.xml`中，加入Servlet条目，然后写一个简单的Servlet放在相应的目录。最后，运行命令完成构建和部署，是不是很简单呢？

```
bash-3.2$ gradle jettyRunWar
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:war UP-TO-DATE
> Building 80% > :jettyRunWar > Running at http://localhost:8080/chapter2
```

Gradle的构建过程清爽宜人，习惯了看Gradle的配置文件之后再看`pom.xml`是不是有点想吐了？哈哈。

###注解

1. [Twitter的Scala教程](http://twitter.github.io/scala_school/index.html)：不推荐。讲解过于简略，而且有些内容已经过时，不过Twitter的[Effective Scala](http://twitter.github.io/effectivescala/)很是不错，推荐阅读！
2. [Scala in action](http://www.amazon.com/Scala-Action-Nilanjan-Raychaudhuri/dp/1935182757/ref=sr_1_1?ie=UTF8&qid=1392621526&sr=8-1&keywords=scala+in+action)：这本书的第一印象不错，希望是本实用的好书。
3. [Groovy](http://groovy.codehaus.org/): JVM上运行的脚本语言，和Java的语法很相似，学习成本较低。

