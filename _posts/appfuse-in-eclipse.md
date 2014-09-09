title: Appfuse (1)
date: 2014-03-27 21:21:41
tags:
 - appfuse
 - Java
---

以前也用过Appfuse，不过一直也没怎么深入，最近又有机会玩一玩儿，顺便记录一下。

[Appfuse](http://appfuse.org/display/APF/Home)是一个很有意思的项目，可以把它看成是Java企业应用开发的一个最佳实践集合。在Maven的帮助下，可以生成基于Struts，Spring MVC或者Wicket等一些框架的组合，这样就免去了最初搭建脚手架（Scaffolding）的过程。这在Play Framework和Grails出现之前应该算是比较方便的，再加上作者Matt Raible（他的[博客地址](http://raibledesigns.com/)）本身在Java圈子里也有小有名气，所以这个项目还是有一定人气的。今天看了一下，最新版的Appfuse 3.0已经支持Spring 4和Java 7/Maven 3（最低要求）了，可见人家也是与时俱进的，我们就来尝试一把。

<!-- more -->

根据[快速开始文档](http://appfuse.org/display/APF/AppFuse+QuickStart)，可以很快地下载项目。我选择使用Spring MVC，具体命令如下，其中的groupId和artifactId要换成自己项目的组织和名称：

```
$ mvn archetype:generate -B -DarchetypeGroupId=
org.appfuse.archetypes -DarchetypeArtifactId=appfuse-modular-spring-archetype -D
archetypeVersion=3.0.0 -DgroupId=com.mydemo -DartifactId=demo -DarchetypeR
epository=http://oss.sonatype.org/content/repositories/appfuse
```

执行这条命令的条件是下载了Maven 3，并配置了Maven的执行路径，可以通过如下命令检查：

```
$ mvn -version
```

下载完成之后，我选择先在Eclipse中编译，使用导入Maven项目的方式将源码导入，此时遇到了三个错误。

第一个错误的具体信息如下：

```
Plugin execution not covered by lifecycle configuration: org.codehaus.mojo:hibernate3-maven-plugin:2.2:hbm2ddl (execution: default, phase: process-test-resources)
```

谷歌搜索错误的解决方法, 可以参考下面两个帖子：
 - [http://appfuse.547863.n4.nabble.com/POM-td4655717.html](http://appfuse.547863.n4.nabble.com/POM-td4655717.html)
 - [http://wiki.eclipse.org/M2E_plugin_execution_not_covered](http://wiki.eclipse.org/M2E_plugin_execution_not_covered)

文章实在比较冗长，m2e的wiki里面讲了三种方法，我采取了quick fix，选择忽略。

第二个错误是在sample-data.xsd文件中报错：```Content is not allowed in prolog```，
尝试了网上说的把文件存成ASNI格式，不成；试验了其他方法也不成，文件本身都是乱码。
因为Appfuse开放源码，所以我直接找到这个文件把内容拷贝过来就好了，从文件头定义可以看出来它是UTF-16编码，所以肯定Windows系统加了什么乱糟糟的东西，参考[这篇博客](http://blog.csdn.net/zhaoxu0312/article/details/8511792)。sample-data.xsd源码的[位置](https://github.com/appfuse/appfuse/blob/34dc1599636e15ab9e0372d67542321e25f1896c/web/common/src/test/resources/sample-data.xsd)。

第三个错误是文件default.jsp中报错：```syntax error on token "ne" invalid Assignmentoperator```。这个错误很奇怪，搜索一下找不到答案，而且我印象比较深，这个以前遇到过。后来随便改了改ne这个字符串，然后再改回来，最后使用Maven - Update Project，居然就好了。所以，Eclipse里面有些莫名其妙的问题可以通过Close/Reopen Project或者Update/Refresh Project来解决，呵呵。

这篇博客主要记录了初次使用的Appfuse 3.0的一点体验，和遇到问题的一些解决方法，下一篇会讲讲编译运行的方法。

BTW

 - Appfuse采用Apache 2的[license](http://static.appfuse.org/license.html)，无论对开源软件还是商业化软件都是友好的。
 - 在Stackoverflow上看到了相似的问题，回答了一下下：[地址](http://stackoverflow.com/questions/22521568/errors-in-spring-mvc-appfuse-app-in-eclipse/22687468#22687468)