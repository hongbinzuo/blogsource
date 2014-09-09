title: Scala patterns (#1) - Option
date: 2014-02-25 18:24:35
tags:
 - Scala
 - Design Patterns
---

自从1994年[《设计模式：可复用面向对象软件的基础》](http://zh.wikipedia.org/wiki/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%EF%BC%9A%E5%8F%AF%E5%A4%8D%E7%94%A8%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%BD%AF%E4%BB%B6%E7%9A%84%E5%9F%BA%E7%A1%80)问世以来，设计模式就备受关注，虽然业界褒贬不一，而且有人专门写了[反模式](http://en.wikipedia.org/wiki/Anti-pattern)来陈述其弊端，但大家对它的作用大部分还是认可的，尤其是在面向对象编程领域。但是，正如Brooks所说的[“天下没有免费的银弹”](http://zh.wikipedia.org/wiki/%E6%B2%A1%E6%9C%89%E9%93%B6%E5%BC%B9)，软件的本质问题是管理复杂度，所以能用设计模式解决问题，它必然也会带来衍生问题，工具都有利弊，如何更好地使用工具才是王道。为了减少对设计模式的滥用和简化设计（既然可复用，为什么不直接让语言天生支持呢？），多年以来，人们一直期望在语言层面增加对可复用编程模式（pattern/paradigm）的支持，而这些想法确实也逐渐被多种现代编程语言所采纳。
<!-- more -->

在学习Scala语言的过程中，我感觉程序员得到了以往学习任何语言都不曾有过的待遇：在语言层面对于模式的支持已经达到了相当丰富的程度。当然，受限于现在所学的知识，还不能把Scala中的设计模式尽数解读，但是我准备用一个系列把Scala中涉及的设计模式写出来，这样做的好处之一是能从应用层面能更好地使用这些模式（准确地说，是语言元素或语法），之二是能更深入地理解设计模式本身。当然，如果没有伟大的互联网，有些工作是很难开展的，本文内容大部分都是基于网络资源和前辈的工作完成的。

### Option模式 

*Scala in action*中提到了几种模式，今天我们先聊聊Option模式，不过这种模式不是[《设计模式》](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612/ref=sr_1_1?ie=UTF8&qid=1393315872&sr=8-1&keywords=design+pattern)书中定义的一种，是编外的一种模式(参考[Null对象模式](http://en.wikipedia.org/wiki/Null_Object_pattern))，作者在书中给出了来源，可能是较早[讨论Option模式的一篇博文](http://www.codecommit.com/blog/scala/the-option-pattern)。这篇文章有点长，我简单解释一下，博主基本上分三点（Option在Scala中的应用、Option和null的比较以及Java中Option的手工实现）讨论Option，我们重点关注第一点，那就是使用一个除法函数来说明Scala内嵌Option的用法，如下所示：

```
def div(a:Int)(b:Int):Option[Int] = if (b <= 0) None
  else if (a < b) Some(0)
  else Some(1 + div(a - b)(b).get)
```

这个函数还算比较直观，只是里面用到了Currying（[柯里化](http://zh.wikipedia.org/wiki/%E6%9F%AF%E9%87%8C%E5%8C%96)，或参见博主[另一篇文章](http://www.codecommit.com/blog/scala/function-currying-in-scala)）和递归，我们可以暂时忽略这些，只关注返回值。返回值在这里定义为Option[Int]，在函数中返回的结果可能是None、Some(0)或者Some(其他值)，很容易理解吧？

作者继续讨论了使用Option两种方式的异同：第一种就是上述除法函数的例子，这并不是一种很好的方法（思考一下为什么），而第二种则是使用模式匹配，则会更优雅一些：

```
div(13)(0) match {
  case Some(x) => println(x)
  case None => println("Problems")
}
```

### 为什么null是糟糕的？

如果你写过Java程序可能会比较有感触，100行程序至少得有10行以上得和null的处理逻辑相关吧？这篇博文也对Option和null的使用方式做了个比较，但我更喜欢SlideShare上的一个屁屁踢[Option, Either, Try](http://www.slideshare.net/MichalBigos/option-either-try-and-what-to-do-with-corner-cases-when-they-arise)中的例子，摘抄如下：

######Java中使用null的例子

```
String foo = request.params("foo");
if (foo != null) {
	String bar = request.params("bar");
	if (bar != null) {
	  doSomething(foo, bar);
	} else {
	  throw new ApplicationException("Bar not found");
	}
} else {
	throw new ApplilcationException("Foo not found");
}
```

###### 为什么null容易出错（注释译成了中文）

```
// 1. 没人知道结果是不是null，编译器也不知道
String foo = request.params("foo");
// 2. 必须要做烦人的检查
if (foo != null) {
	String bar = request.params("bar");
	//if (bar != null) {
	/* 3.臭名昭著的NullPointerException危险，很多人都可能会忘了检查*/
	doSomething(foo, bar);
	/* 4. 随意细化的错误消息，有时最后抛出错误就够了*/
	//} else {
	//  throw new ApplicationException("Bar not found");
	//}
} else {
    /* 5. 设计缺陷，只是原来Exception的替换 */
	throw new ApplilcationException("Foo not found");
}
```

看完这个例子，已经不需要解释了。强烈建议喜欢Scala的同学看完这个Slides，有内涵。

### Option模式是怎么定义的

Option在Scala中的定义只是这样的：

```
sealed abstract class Option[A]

case class Some[+A](x: A) extends Option[A]

case class None extends Option[Nothing]
```

这里Option是一个抽象类，有两个case class实现，一个是Some，代表有值，另一个是None，代表空值，也就是“具有一个或零个元素的容器”。其中+A是Scala中协变（简单理解就是对类型A以及其子类型适用）的意思，请参考相关文档。

总体来说，借用Michal Bigos的Slides，Option模式的好处有以下几点：

 - 在类型层面规定值存在或不存在
 - 编译器强迫程序员处理Option
 - 不会意外地依赖不存在的值
 - 清晰地描述了设计意图

所以，学习一下Option，在你的程序里用起来吧！

###参考资源

 1. [Scala语言中的设计模式](https://wiki.scala-lang.org/display/SYGN/Design+Patterns#)
 2. [关于“Option”模式](http://www.codecommit.com/blog/scala/the-option-pattern)
 3. [Option, Either, Try and what to do with corner cases when they arise](http://www.slideshare.net/MichalBigos/option-either-try-and-what-to-do-with-corner-cases-when-they-arise)
 4. [Design Patterns in Scala](http://pavelfatin.com/design-patterns-in-scala/)

*说明：文中任何引用部分版权均归原文作者所有，引用请注明本文地址和原文地址。文中任何拼写或摘抄错误均由本文作者负责纠正。*