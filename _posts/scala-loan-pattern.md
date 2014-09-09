title: Scala patterns (#5) - the Loan Pattern
date: 2014-03-03 21:30:28
tags:
 - Scala
 - Design Patterns
---

按照*Scala in action*的说法，Scala中的借贷模式（Loan Pattern）相当于Java/C++中的模板方法（Template Method）模式。很遗憾，由于同样的原因，书中所附的引用链接已失效（囧），所以
只能从网上参考借贷模式的详解。我认为Knoldus的这篇博文[理解借贷模式](http://blog.knoldus.com/2012/11/16/scalaknol-understanding-loan-pattern/)写得非常不错，把这种模式的适用场景写得很清楚：

<!-- more -->

>Loan Pattern as the name suggests would loan a resource to your function. So if you break out the sentence. It would

> - Create a resource which you can use
> - Loan the resources to the function which would use it
> - This function would be passed by the caller
> - The resource would be destroyed

> As you would see, the advantages are multifold. First, I am not constrained by the function which can use the loaned resource. I can pass any function that I desire. Second, I am not concerned about the creation, destruction of the resource. The loan function takes care of it.

除了这篇博文，还可以看一个Youtube的视频（[地址](https://www.youtube.com/watch?v=FKbTqezP8vQ)），这个8分钟左右的教学视频生动地讲解了借贷模式的例子，对于实际应用很有借鉴意义。

另外可供参考的资源：

 - [http://www.scalaloader.org/2013/03/loan-pattern-in-scala.html](http://www.scalaloader.org/2013/03/loan-pattern-in-scala.html)
 - [Scala Pattern 之 Loan Pattern（ITEye）](http://www.iteye.com/topic/536958)

我认为这种模式也非常符合DRY（Don't Repeat Yourself）原则，只使用一个函数就可以把相同类型的资源使用代码的重复部分去除，很好。