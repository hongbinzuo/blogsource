title: Play做Build的小坑儿一枚
date: 2014-03-25 21:44:38
tags:
 - play!
 - SBT
 - Scala
---

在看《Play for Scala》，跟着做点小练习。

###小坑儿

第二章给出了一个比较全面的Web应用，这个应用在显示详情页面的时候，需要依赖外部库，所以需要更新构建脚本。书里提到的是用`project/Build.scala`这个文件，结果出现编译错误，大意是`Build.scala`应该是有对象或类的定义的，明显是把它当成普通的Scala文件了，这很奇怪。

<!-- more -->

在网上找找，翻到Play 2.2.x[关于构建的文档](http://www.playframework.com/documentation/2.2.x/Build)，没有提到`Build.scala`这个文件，所以问题的根源可能是在Play 2.0（或SBT的早期版本）的时候曾经支持过`Build.scala`，而现在最新的不支持了，当然这只是个猜想。

###解决方法

把下面这段配置（清单1）放到`project/build.sbt`中去（清单2）：

#####清单-1

```
val appDependencies = Seq(
"net.sf.barcode4j" % "barcode4j" % "2.0"
)
```

#####清单-2

```
libraryDependencies += "net.sf.barcode4j" % "barcode4j" % "2.0"
```

当然，翻墙还是不可避免的，要不然下载不了Maven的库。


