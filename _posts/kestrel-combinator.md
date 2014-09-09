title: Scala patterns (#6) - Kestrel combinator
date: 2014-03-04 12:25:31
tags:
 - Scala
 - Design Patterns
---

Kestrel combinator并不是一种传统的设计模式，这个叫法是在1985年出版的*To Mock the Mockingbird*这本书里提到的，可以参考*Scala in action*作者引用的[资源地址](http://mng.bz/WKns)详细了解这种模式，其中的例子使用的是Ruby语言。我理解这种模式的意义主要是产生**副作用**，即在不改变原有类或对象定义的情况下，使用一段附加函数体来达到产生副作用的目的。

<!-- more -->

这种模式在不同的语言里实现的方式也不一样。下面的一个例子来自*Scala in action*，其中使用了Scala的隐式转换（Implicit Conversion）特性来实现Kestrel combinator：

```

object Combinators {
  implicit def kestrel[A](a: A) = new {
    def tap(sideEffect: A => Unit): A = {
      sideEffect(a)
      a
    }
  }
}

case class Person(firstName: String, lastName: String)

case class Mailer(mailAddress: String) {
  def mail(body: String) = { println("Send mail here" )}
}

object DemoKestrel extends App {
  import Combinators._
  Person("Nilanjan", "Raychaudhuri").tap(
      p => {
        println("First name" + p.firstName)
        Mailer("Some address")
      }
  ).lastName 
}

```

这种模式具体用在什么场景下呢？再让我想想。。