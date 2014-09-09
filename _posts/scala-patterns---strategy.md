title: Scala patterns (#4) - Strategy
date: 2014-03-02 15:38:41
tags:
 - Scala
 - Design Patterns
---

策略模式是一种经典的设计模式，简而言之，就是做同一件事情，但在不同的场景中（或针对不同的对象）采用不同的算法。由于Scala简洁的语法和对高阶函数的支持，相比Java写出的代码会更加精简。

下面给出几个例子来感受一下Scala中策略模式的写法，首先是*Scala in action*书中的例子。

<!-- more -->

```
def calculatePrice(product: String, taxingStrategy: String => Double) = {
  ...  
  val tax = taxingStrategy(product)
  ...
}
```

这个例子简直是简单地过分，只需要传入一个函数（参数是String类型，返回值是Double类型），借由传入函数来决定具体的计算方法（策略）就可以了。由于这个例子过分简单，我们再来看一个更具体的例子（来自[Memetic Musings Blog](http://memuser.blogspot.com/2008/03/design-patterns-in-scala.html#7399152332218666295)）：

```
trait TaxPayer
case class Employee(sal: Long) extends TaxPayer
case class NonProfitOrg(funds: BigInt) extends TaxPayer

//Consider a generic tax calculation function. (It can be in TaxPayer also).
def calculateTax[T <: TaxPayer](victim: T, taxingStrategy: (T => long)) = {
  taxingStrategy(victim)
}

val employee = new Employee(1000)
//A strategy to calculate tax for employees
def empStrategy(e: Employee) = Math.ceil(e.sal * .3) toLong
calculateTax(employee, empStrategy)

val npo = new NonProfitOrg(100000000)
//The tax calculation strategy for npo is trivial, so we can inline it
calculateTax(nonProfit, ((t: TaxPayer) => 0)
```

这个例子更加Scala一些，其中用到了类型上限`T <: TaxPayer`，意思是T为TaxPayer类型及其子类型。其实仔细一看核心部分和第一个例子是一样的，只不过多用了一些对象的继承关系，使得Strategy的声明和实现更加明确化。

最后一个例子来自于之前提到过的[Design Patterns in Scala](http://pavelfatin.com/design-patterns-in-scala/#strategy)，这篇博客的好处是能看到Java实现和Scala实现的比较：

**Java实现**

```
public interface Strategy {
    int compute(int a, int b);
}

public class Add implements Strategy {
    public int compute(int a, int b) { return a + b; }
}

public class Multiply implements Strategy {
    public int compute(int a, int b) { return a * b; }
}

public class Context  {
    private final Strategy strategy;

    public Context(Strategy strategy) { this.strategy = strategy; }

    public void use(int a, int b) { strategy.compute(a, b); }
}

new Context(new Multiply()).use(2, 3);
```

**Scala实现**

```
type Strategy = (Int, Int) => Int 

class Context(computer: Strategy) {
  def use(a: Int, b: Int)  { computer(a, b) }
}

val add: Strategy = _ + _
val multiply: Strategy = _ * _

new Context(multiply).use(2, 3)
```

是不是觉得尝到一点儿函数式编程的甜头儿了呢？:)


**参考资源**

 - 维基百科对策略模式的定义：[http://en.wikipedia.org/wiki/Strategy_pattern](http://en.wikipedia.org/wiki/Strategy_pattern)
 - Stackoverflow中的问答：[Better alternative to Strategy pattern in Scala?](http://stackoverflow.com/questions/4950524/better-alternative-to-strategy-pattern-in-scala)
 - Design Patterns in Scala: [http://memuser.blogspot.com/2008/03/design-patterns-in-scala.html](http://memuser.blogspot.com/2008/03/design-patterns-in-scala.html) 
 - 一个更加详细的策略模式实现：[http://scalasim.blogspot.com/2010/09/strategy-pattern-and-traits.html](http://scalasim.blogspot.com/2010/09/strategy-pattern-and-traits.html)
 - Design Patterns in Scala again: [http://pavelfatin.com/design-patterns-in-scala](http://pavelfatin.com/design-patterns-in-scala)
 - 神奇的长文：[How Scala killed the Strategy Pattern](http://alvinalexander.com/scala/how-scala-killed-oop-strategy-design-pattern)
