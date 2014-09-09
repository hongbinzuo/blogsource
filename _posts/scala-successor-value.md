title: Scala patterns (#3) - Successor Value
date: 2014-03-02 11:25:27
tags:
 - Scala
 - Design Patterns
---

其实这个设计模式也不是Scala语言特有的，只是因为在*Scala in action*（下文中提到的书都是指本书）中提到，因此做一个小结。在书的第五章Functional Programming中讨论函数式编程的时候，谈到了纯函数式编程、面向对象编程和非纯函数式编程的一些特点。Scala是一门杂糅的编程语言，它不是纯函数式语言，这样就涉及到一个问题：如何尽量多地使用它的函数式特性，同时避免或者减少对于对象状态的改变。作者在这时举了一个小例子，就是Successor Value模式（书中也叫Functional Object模式，但是没有查到相关资料）。

<!-- more -->

非常遗憾的是，作者引用Object Mentor的一篇关于Successor Value的原始博文已经失效（[地址](mng.bz/b27e)），所以我们不知道原来Michael Feathers是怎么详细定义这个模式的。但是从书中的例子可以基本了解这个模式的思路，和Java中的String可以类比，主要达到的目的是不改变原有对象的状态而是通过某种方式创建一个新的对象。下面把书中的例子摘录如下：

**可变的Square对象定义**：

```
class Square(var side: Int) {
  def area = side * side
}
```

**不可变的Square定义**：
```
class PureSquare(val side: Int) {
  def newSide(s: Int): PureSquare = new PureSquare(s)
  def area = side * side
}
```

在PureSquare类的定义中，side是val参数，所以新创建的对象是不可变的，通过新定义的newSide方法，如果想调用已有对象改变side的话，那就返回一个新建的PureSquare对象。我们借用[Stackoverflow问答中的例子](http://stackoverflow.com/questions/18999709/what-is-successor-value-pattern)来进一步理解一下：

```
val square1 = new PureSquare(1)
assert(square1.area == 1)

//this is similar to changing the side of square1
val square2 = square1.newSide(2)

//and the area changes consequently
assert(square2.area == 4)
//while the original call is still referentially transparent [*]
assert(square1.area == 1)
```

这应该不是面向对象编程中常用的一个模式，但是可能在Scala编程中会用的到。
