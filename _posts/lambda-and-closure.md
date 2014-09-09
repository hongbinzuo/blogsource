title: lambda and closure
date: 2014-02-23 11:06:15
tags:
 - Scala
---

lambda又称为**lambda表达式**或**lambda演算子**，名字听起来挺高端，其实在编程语言里倒也不难理解。但是，和lamba相比**闭包**却没那么直观。这两个概念作为函数式编程基础的一部分，是必须要掌握的。另外，Java 8也引入了lambda表达式，C#也从版本3.0后开始支持lambda，可见这些函数式编程的特性已经逐渐被主流的面向对象语言所借鉴吸收。
<!-- more -->

下面的正文部分译自*Scala in action*的一段解释，算是对这两个概念的初步澄清。在译文后面的参考链接中，我也列举了一些资源，从而帮助理解lambda和闭包的概念以及在不同语言中的应用。

<img alt="lambda算子" src="http://upload.wikimedia.org/wikipedia/commons/e/ee/Lambda_uc_lc.svg" style="width: 450px;"/>

###lambda和闭包（closure）的区别是什么

lambda就是匿名函数——即没有名字的函数。前面你已经看到过一些例子了。闭包就是封闭在其定义所处环境的任意函数。让我们用一个例子来解释一下，比如，将一个百分比应用到一个列表上：

```
scala> List(100, 200, 300) map { _ * 10/100 }
res34: List[Int] = List(10, 20, 30)
```

在这个例子中，传递给map的函数就是一个lambda表达式（译者注：其中 `_ * 10/100`也可以写成`(x:Int) => x * 10/100`）或`x => x * 10/100`）。现在假设这个百分比数值会随着时间变化，所以要把当前的百分比数值存在一个变量里。

```
scala> var percentage = 10
percentage: Int = 10
scala> val applyPercentage = (amount: Int) =>
amount * percentage/100
applyPercentage: (Int) => Int = <function1>
```

在这种情况下，`applyPercentage`就是一个闭包，因为它保持了它被创建时的环境，此处主要是`percentage`变量：

```
scala> percentage = 20
percentage: Int = 20
scala> List(100, 200, 300) map applyPercentage
res33: List[Int] = List(20, 40, 60)
```

lambda和闭包是不同的概念，但却紧密相关。

###参考资源

1. 中文维基百科：[λ演算的定义](http://zh.wikipedia.org/wiki/%CE%9B%E6%BC%94%E7%AE%97)
2. 中文维基百科：[匿名函数的定义及其在编程语言中的应用情况](http://zh.wikipedia.org/wiki/%E5%8C%BF%E5%90%8D%E5%87%BD%E6%95%B0)
3. 中文维基百科：[闭包的定义] [1]
5. 酷壳：[理解Javascript的闭包](http://coolshell.cn/articles/6731.html)
6. 阮一峰的网络日志：[学习Javascript的闭包](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)
7. 知乎：[Lambda表达式有何用处？如何使用？](http://www.zhihu.com/question/20125256)
8. 徐青枫的技术博客：[说说Java8中的Lambda表达式](http://www.cnblogs.com/xuqingfeng/archive/2013/04/26/about-Java8-lambda-expression.html)
9. Stackoverflow：[Closure in Java 7](http://stackoverflow.com/questions/5443510/closure-in-java-7)
10. Oracle文档库：[Java 8的lambda表达式指南](http://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)
11. MSDN：[C#中的lambda表达式编程指南](http://msdn.microsoft.com/zh-cn/library/bb397687.aspx)
12. Stackoverflow：[C++ 11中的lambda表达式讨论](http://stackoverflow.com/questions/7627098/what-is-a-lambda-expression-in-c11)

[1]: http://zh.wikipedia.org/zh-cn/%E9%97%AD%E5%8C%85_(%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)