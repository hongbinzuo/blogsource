title: Scala中的面向对象编程
date: 2014-02-21 20:48:04
tags:
 - Scala
---

前几天看到一篇有关Scala的文章，其中对它的发展有些担心：Scala会不会成为下一个C++？这种担心也并非毫无道理，看完*Scala in action*的第三章，我的感觉是Scala确实强大，但也增加了一些不必要的特性，或者换句话说，有些特性是一般应用开发者不需要关心的，只有库开发者才有必要掌握。所以，在适当的时候，我需要把Martin的Scala开发水平等级和Twitter的Effective Scala再好好研究一下，以免过早被一些高级的语法细节纠缠却忽视了实用性强的基本特性。

第三章*OOP in Scala*中介绍了Scala面向对象编程方面的一些基本概念，这些概念或者说语法元素有的是和Java类似的，有的是全新的，所以有必要简单总结一下再继续阅读。

<!-- more -->

类（class）的构建、构造方法（constructor）和包（package）、导入（import）等和Java大同小异，只是在一些细节上有所区别，特别注意的有以下几点：

 - 类的修饰符和Java不一样，比如，Scala的类不需要加`public`修饰就是公开的
 - Scala文件的名字和类的名字不一定要保持一致
 - 构造方法可以在类定义时声明，并有主构造方法（primary constructor）的概念，其中又有一些比较特别的规定比如每个构造方法都必须先调用其它构造方法（含主构造方法）；也特别需要注意其中访问权限修饰符对于实际产生构造方法的影响，可以使用程序javap查看产生的Java类字节码的具体内容
 - 包的使用方法特别灵活，但是现在可以不用了解那么多，暂时使用和Java类似的组织方式即可
 - 导入也有一些变化，但都不是根本性的

**Mixin**一般翻译成“混入”，Scala使用**trait**（特性）来支持混入。C++是支持多继承的，Java是通过单继承加接口的方式来实现混入的，而Scala则引入了trait。Trait可以看作是一个接口（interface），不同的是它可以含有已实现的方法。trait和抽象类（abstract class）的区别是：抽象类可以用构造方法参数，而trait不可以。在继承方面，Scala和Java也有所不同，比如，如果覆盖父类方法，那么必须要加上`override`关键字（这点我很喜欢），这样使用起来比较安全。

**Case class**这个概念也很有意思，作者总结了引入Case class的好处：

 - 默认所有的参数都是val类型，并且公开，当然也是通过访问器（accessor）访问
 - 根据提供的参数默认实现了`equals`和`hashCode`方法
 - 默认实现了`toString`方法
 - 有一个默认的方法`copy`，方便创建当前实例的拷贝
 - 伴随对象（companion object）通过`apply`方法默认创建，对象的参数和类的参数定义保持一致
 - 默认实现`unapply`方法，允许类名作为模式匹配（pattern matching）的提取器（extractor）
 - 序列化也有默认的实现

想一想，这还真是一个不错的特性，作者也提到，这就是Java里常写的DTO，使用Scala就不用那么麻烦啦！

**具名参数**就是在创建对象时指定参数的名字，作用是能避免传参错误，个人认为在IDE功能这么强大的情况下，这个特性有点多余。**缺省参数**就是在定义参数时赋初值，这个还比较有用。**拷贝构造方法**这个概念，我们只要了解拷贝过程可以自己定义就行了。

另外，Scala在修饰符上也更加灵活一些。例如private修饰符可以加入修饰范围，参见下面的例子：

```
package outerpkg.innerpkg
class Outer {
  class Inner {
    private[Outer] def f()  = "This is f"
    private[innerpkg] def g() = "This is g"
    private[outerpkg] def h() = "This is h"
} }
```

在Scala中，标准的访问修饰符有`private`和`protected`，为什么没有`public`呢？因为Scala中不加任何修饰符的成员就是public成员。除了标准的修饰符之外，Scala还引入了`sealed`修饰符，只对类定义有用，意为只在当前源文件中可见。

最后两个新特性是**值类**（values classes，在版本2.10中引入）和**隐式转换**（implicit conversions）。第一个特性没理解到底有什么用，第二个倒是觉得有点价值，只是用多了就会降低代码的可读性。

总体来看，Scala在面向对象的基本架构上和Java相比并没有本质的变化，类和对象为基础的封装、继承和多态是很相似的，只是Scala在Java的基础上有所改进，有些细节需要在使用中多加注意。

*好玩的事儿：本章还学到了一点点MongoDB的知识，算是意外收获吧。*
