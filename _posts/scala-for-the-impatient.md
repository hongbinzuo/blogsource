title: Scala for the Impatient
date: 2014-02-10 22:44:08
tags:
 - Scala
---

###关于这本书

花了两周左右的零散时间把这本书的免费部分（初级语法/A1 Level/共9章）读完了，同时也做完了比较有代表性的习题。感觉有些收获，起码对Scala语言有了基本的认识，并且通过上手操练，也积累了一些入门经验。不过，由于Scala的一些语法还是比较反直觉，并且语法规则、编程范式较多，因此距离真正掌握这门语言还差得远。本书中提到了Scala语言创建者Martin Odersky对于Scala开发技能的水平划分（见下图），我应该刚刚才达到A1水平。
<!-- more -->

<img alt="Scala开发者水平等级" src="/img/scala_levels.png" style="width: 600px;"/>

从这本书的内容来看，如果你有Java、C++或C#语言的背景，使用这本书学习Scala语法是最合适不过的了，用一到两周的业余时间就可以基本学完。它的习题设计也不错，基本上能够涵盖关键知识点。虽然是英语，但行文流畅，没有太多长句子和晦涩生词，不用查字典。

这本书中间有几页的bug有点密集，必须要对照着书的勘误阅读，勘误的地址是：
[http://horstmann.com/scala/bugs.html](http://horstmann.com/scala/bugs.html)

###Scala的感受

Scala到目前为止给我印象比较深的几点是：
 
 - 整合面向对象编程（准确地说是命令式编程，面向对象是和命令式编程、函数式编程以及逻辑式编程正交的一种编程模型）和函数式编程，使得语言的构建能力强大而高效
 - 省略Java中不必要的语言样板和装饰（累赘语句），呈现极简的表达方式 
 - 语法强大，导致复杂性升高、学习曲线略陡
 - 函数式编程中递归的作用（参见参考资源中第2条）
 - 多使用函数式编程的思维解决问题

下一步学习的资源包括，
 
 - Scala for the Impatient全书（可从Amazon.com购买）
 - Twitter的Scala教程
 - Coursera课程Functional programming principles in Scala
 - Scala in action
 - Scala in depth
 - Scala的小中文教程

###IDE开发环境选择

在做练习的过程中，我有意地使用了Scala IDE 3.0.2（基于Eclipse）、IntelliJ 12.1.4（通过plugin）和Netbeans 7.4（通过plugin: [地址](https://github.com/dcaoyuan/nbscala)），最后的综合体验是目前Scala IDE 3.0.2的用户体验更好一些。

 - IntelliJ无论是V12商业版还是V13社区版都是通过plugin的方式支持Scala，在IntelliJ 13的产品宣传中说的是内置支持，可能V13的商业版有（？），但是近300刀的升级费用我看我还是暂时免了吧；plugin的支持只能算是OK，其中有一个比较讨厌的问题是需要手动设置Scala的编译环境，网上的一些方法并不能轻易成功，而且缺乏对Scala创建类型的支持，微博上还有同学说有些莫名其妙的语法提示错误。
 - Scala IDE是Scala官方推荐的工具，用起来还算顺滑。Scala的多种应用类型都默认支持，如Scala Class、Scala Application以及Scala Worksheet（虽然有些bug）等。从这款工具的开发历史来看，从2013年初的版本2.1，用了一年的时间到3.0，应该是全速在发展这款开发工具，虽然暂时有些小问题，但还是非常值得期待的！
 - Netbeans 7.4也是通过plugin支持Scala，这款plugin是国人（邓草原）开发的，很不错。只是我在练习阶段，有些小程序就在Worksheet里直接看结果，所以因为它不支持Scala worksheet还是稍有不便。不过，如果开发大的项目应该是可以的，这个需要更多评估。另外一点，就是Scala项目倒底是使用Maven还是SBT这个还是需要进一步研究一下。
 - Sublime Text是有相应的插件的，但比较折腾，没试。
 - LightTable目前为止还没有插件支持。

###参考资源

1. 这本书的免费部分可以在Typesafe上下载，下载地址是：[Scala for the Impatient](http://typesafe.com/resources/book/scala-for-the-impatient)。
2. [有趣的 Scala 语言: 使用递归的方式去思考](http://www.ibm.com/developerworks/cn/java/j-lo-funinscala1/)
3. [Twitter的Scala教程](http://twitter.github.io/scala_school/zh_cn/)
4. [Scala的小中文教程](http://zh.scala-tour.com/#/welcome)