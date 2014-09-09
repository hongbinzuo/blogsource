title: Scala不容小视
date: 2014-02-05 16:22:04
tags:
 - Java
 - Scala
---

春节这几天学习了一下Scala，因为每天时间都非常有限，也就平均1到2个小时的样子，所以只关注了两个资源，一个是Coursera上Scala语言发明者Martin Odersky的[Functional Programming Principles in Scala](https://class.coursera.org/progfun-003)课程，另一个是Typesafe上的电子书[*Scala for the impatient*](http://typesafe.com/resources/book/scala-for-the-impatient)。

Coursera上的课程还是不错的，很正宗、原汁原味，对于深入理解Scala的函数式编程范式非常有帮助，但是后面的一些内容对于应用开发者来说应该是有点难了（呵呵，我自己感受啊），更适用于中高级应用开发或者库开发者，所以在看完了前5周的课程之后，为了能重新巩固基础，我使用了第二个资源，即*Scala for the impatient*。作为后续的学习计划，当然还是要学完Coursera，然后把课程中推荐的书看一下。

<!-- more -->

*Scala for the impatient*这本书只有前9章，对于入门是足够了，如果想要继续学习可能要花钱买电子书，或者看其他书。这本书有几个好处，

1. 免费正版。
2. 经常和Java/C++的语法进行对比，对于从传统语言转过来的开发者非常有用。
3. 100多页的小书，需要花的时间比较短，可以很快掌握基础语法然后开始写程序；而且作者行文流畅，读起来感觉比较舒服。
4. 每章都附有练习，难度适中。

总体上比较推荐这本书作为入门教材，看完之后可以再学习其他资源。下面是我在看完第2章之后的一个小练习，供参考：

Write a function that computes x<sup>n</sup>, where *n* is an integer. Use the following
recursive definition:

 - x<sup>n</sup> = y<sup>2</sup> if *n* is even and positive, where y = x<sup>n / 2</sup>.
 - x<sup>n</sup> = x· x<sup>n</sup> – 1 if *n* is odd and positive.
 - x<sup>0</sup> = 1.
 - x<sup>n</sup> = 1 / x<sup>–n</sup> if *n* is negative.

Don’t use a **return** statement.

我的实现如下：

```
def power(x: Int, n: Int): Double = n match {
  case 0 => 1
  case a: Int if 0 > a => 1 / power(x, -n)
  case a: Int if a % 2 == 0 => power(x, n/2) * power(x, n/2)
  case a: Int if a % 2 != 0 => x * power(x, n-1)
}                                              
```

回顾这几天的学习路径：先是看《Java程序员修炼之道》中关于Scala的概览，然后学习了Coursera的课程，现在在看*Scala for the impatient*这本书。通过这次学习，基本上想达到几个目的：

 - 了解并掌握Scala的基本特性和编程范式
 - 理解Scala语言的适用范围
 - 了解Scala的代表性框架或组件库

Scala结合了强大的面向对象编程和函数式编程，使得语言的可用性范围很广。基于Java平台，和Java能够互操作，继承并扩展Java类库达到了令人发指的程度（看一下Scala语言的API文档你就能理解我为什么这么说），可能最强大而我尚未发掘的是Actor特性，听说这个特性（尤以Akka为代表）极大地增强了Java平台并发编程的能力。Scala不是一门脚本语言，所以尽管Groovy使用语法糖和扩展库能够帮助Java提升开发效率，但是Scala却进一步扩展了这种能力，使得这门语言在JVM平台上可以完全胜出！Twitter和Linkedin可以佐证一下。:)

在一篇[Scala很难的文章](http://www.aqee.net/yes-virginia-scala-is-hard/)里（其中提到的开发工具一说，我认为现在已经有所改善了，基于Eclipse的Scala IDE初步用起来很不错！），作者详细地介绍了Scala令人觉得困难的一些特性。在选择语言的时候，我们需要花时间仔细考量语言的特性、生态圈、社区、开发工具、开发人员以及性价比等等，这是值得的：全面考量能让我们充分利用语言的优势为团队和客户创造价值！

天下事有难易乎？为之，则难者亦易矣，不为，则易者亦难矣。所以，不如学习起来，让你的编程技能库增加一套强大的工具还是值得的，不是吗？

Keep learning, keep coding!