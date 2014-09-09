title: Scala Patterns(#2) - Lazy initialization
date: 2014-02-26 20:59:06
tags:
 - Scala
 - Design Patterns
---

### 延迟初始化

[**延迟初始化**](http://zh.wikipedia.org/wiki/%E5%BB%B6%E8%BF%9F%E5%88%9D%E5%A7%8B%E5%8C%96%E6%A8%A1%E5%BC%8F)是程序设计中减少开销、提高性能的一种做法，同时它也是创建型设计模式中的一种。在*Effective Java*里，Bloch是这么描述延迟初始化的，

> Lazy initialization is the act of delaying the initialization of a field until its
value is needed. If the value is never needed, the field is never initialized.

<!-- more -->

简单翻译一下就是，“延迟初始化就是把一个成员的初始化延迟到需要使用它的值的时候才进行。如果不需要使用这个成员的值，那么就一直不用初始化。” 延迟初始化又叫做延迟实例化，更加广义的概念是延迟计算（Lazy Evaluation）。我们可以同时参考MSDN中的定义，描述和适用范围也比较清楚：[延迟初始化][1]。在Scala中，我们不用自己费心写这种模式的代码，因为有一个关键字`lazy`来帮助我们完成，`lazy`是作为修饰符关键字出现的，它的定义如下（参考[Scala语言手册](http://www.scala-lang.org/docu/files/ScalaReference.pdf)），

>The lazy modifier applies to value definitions. A lazy value is initialized the
first time it is accessed (which might never happen at all). Attempting to access
a lazy value during its initialization might lead to looping behavior. If
an exception is thrown during initialization, the value is considered uninitialized,
and a later access will retry to evaluate its right hand side.

综上，要注意几个点：
 
 - lazy只能修饰value值（val）
 - lazy值在第一次访问时初始化
 - 在初始化过程中访问可能会导致循环行为（纳尼？）
 - 在初始化时抛出异常则认为未初始化

先不管那么高深的问题，我们先来看个例子（来自Scala语言手册）：

```
import compat.Platform._

val t0 = currentTime
lazy val t1 = currentTime
val t2 = currentTime

println("t0 <= t2: " + (t0 <= t2)) //true
println("t1 <= t2: " + (t1 <= t2)) //false (lazy evaluation of t1)
```

看完这个例子就更容易理解lazy的含义了，它的使用还是比较简单的。在[Design patterns in Scala](http://pavelfatin.com/design-patterns-in-scala/#lazy-initialization)中也比较了Java的实现和Scala的实现，同时也给出了这种模式的优缺点：优点是语法简洁、可以含有null值并且是线程安全的，缺点是降低了对初始化过程的控制能力。

### 延迟集合

理解了延迟初始化，也就容易理解**延迟集合**了，在*Scala in action*讲解这个概念的时候，又提到了另外两个术语，即**严格集合**（strict collections）和**非严格集合**（non-strict collections），下面是原书的例子，第一个是严格集合（缺省）：
```
scala> def strictProcessing = List(-2, -1, 0, 1, 2) map { 2 / _ }
strictProcessing: List[Int]

scala> strictProcessing(0)
java.lang.ArithmeticException: / by zero
        at $anonfun$strictProcessing$1.apply$mcII$sp(<console>:12)
```
第二个是非严格集合（延迟集合的技术术语）：

```
scala> def nonstrictProcessing = List(-2, -1, 0, 1, 2).view map { 2 / _ }
nonstrictProcessing: scala.collection.SeqView[Int,Seq[_]]

scala> nonstrictProcessing(0)
res38: Int = -1

scala> nonstrictProcessing(2)
java.lang.ArithmeticException: / by zero
        at $anonfun$nonstrictProcessing$1.apply$mcII$sp(<console>:12)
```
从第二个例子可以看出，使用View的方式可以把严格集合转换成非严格集合，从而实现延迟的效果，这对于在集合中Cache大的对象是非常有用的，书中列举了从Twitter里下载大量Tweets的方法，说明了延迟集合的好处，这里就不再赘述。

最后，通过这篇文章，我们快速了解了Scala对于延迟初始化和延迟计算（集合）的支持，后面需要花更多的时间了解和掌握如何更好地在程序中使用这项技术。Bloch说过，一定要谨慎地使用延迟初始化。嗯，一定要谨慎，不要过早优化。


###参考资源

 1. [改进的Lazy实现](http://docs.scala-lang.org/sips/pending/improved-lazy-val-initialization.html)
 2. [Scala语言手册下载](http://www.scala-lang.org/docu/files/ScalaReference.pdf)
 3. [Java中的延迟初始化](http://www.javaworld.com/article/2077568/learn-java/java-tip-67--lazy-instantiation.html)
 4. [Lazy val in Scala](http://daily-scala.blogspot.com/2009/09/lazy-val.html)
 5. [What does a lazy val do](http://stackoverflow.com/questions/7484928/what-does-a-lazy-val-do)
 6. [Non-strict lazy collections](http://daily-scala.blogspot.com/2009/11/non-strict-lazy-collections.html)
 7. [Effective Java 2nd edition](http://www.amazon.com/Effective-Java-Edition-Joshua-Bloch/dp/0321356683/ref=sr_1_1?ie=UTF8&qid=1393396679&sr=8-1&keywords=effective+java)


[1]: http://msdn.microsoft.com/ZH-CN/library/dd997286%28v=vs.110%29.aspx