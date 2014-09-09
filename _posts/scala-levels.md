title: Scala levels
date: 2014-02-22 16:20:53
tags:
 - Scala
---

Martin曾于2010年在Scala讨论组内参与过一个[讨论](http://scala-programming-language.1934581.n4.nabble.com/Is-Scala-an-expert-language-td3073403i60.html)，并在最后总结了Scala语言的水平等级，发表在Scala语言官网上（[原文地址](http://www.scala-lang.org/old/node/8610)）<sup>1</sup>，目的是为Scala语言初学者和爱好者提供参考。在前面的博文[Scala for the impatient](http://hongbinzuo.github.io/2014/02/10/scala-for-the-impatient/)中书的作者也提到过，基本上分为应用开发和库开发两个大类，而每个大类可以细分成三个等级，以下为相关原文的翻译<sup>2</sup>：
<!-- more -->

######A1级：初级应用程序员

 - 类Java语句和表达式：标准操作符，方法调用，条件，循环，try/catch
 - 类，对象，定义，值，变量，导入，包
 - 方法调用的中缀表示法
 - 简单闭包
 - 集合及其相关操作如映射，过滤等
 - for表达式

######A2级：中级应用程序员

 - 模式匹配
 - 特性组合
 - 递归，特别是尾递归
 - XML字面量

######A3级：专家级应用程序员

 - 折叠，例如foldLeft，foldRight等类似的方法
 - 流以及其他延迟的数据结构
 - Actor
 - Combinator解析器

######L1：初级库设计师（注意，不是程序猿啦！）
 - 类型参数
 - 特性
 - 延迟值类型
 - 控制抽象，柯里化
 - 形参

######L2：高级库设计师

 - 变化标记
 - Existential types (e.g., to interface with Java wildcards)（纳尼？）
 - Self type annotations and the cake pattern for dependency injection
 - Structural types (aka static duck typing)
 - 为新类型的for表达式定义map/flatmap/withFilter
 - 提取器

######L3：专家级库设计师

 - 早期初始化程序
 - 抽象类型
 - 隐式定义
 - 更高级类型

###参考原文

######Level A1: Beginning application programmer

 - Java-like statements and expressions: standard operators, method calls, conditionals, loops, try/catch
 - class, object, def, val, var, import, package
 - Infix notation for method calls
 - Simple closures
 - Collections with map, filter, etc
 - for-expressions

######Level A2: Intermediate application programmer

 - Pattern matching
 - Trait composition
 - Recursion, in particular tail recursion
 - XML literals

######Level A3: Expert application programmer

 - Folds, i.e. methods such as foldLeft, foldRight
 - Streams and other lazy data structures
 - Actors
 - Combinator parsers

######Level L1: Junior library designer

 - Type parameters
 - Traits
 - Lazy vals
 - Control abstraction, currying
 - By-name parameters

######Level L2: Senior library designer

 - Variance annotations
 - Existential types (e.g., to interface with Java wildcards)
 - Self type annotations and the cake pattern for dependency injection
 - Structural types (aka static duck typing)
 - Defining map/flatmap/withFilter for new kinds of for-expressions
 - Extractors

######Level L3: Expert library designer

 - Early initializers
 - Abstract types
 - Implicit definitions
 - Higher-kinded types

### 注解

1. 原文下面还有一条评论，有位朋友对L3的标准定得过低有些质疑。
2. 有些没有翻译，因为英文更易懂一些；有些实在难翻译，等以后遇到合适的词汇再更新。
