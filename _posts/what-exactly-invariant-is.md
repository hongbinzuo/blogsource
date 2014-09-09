title: What exactly invariant is
date: 2013-12-12 16:39:36
tags:
 - Java
 - Concurrency
---

invariant到底是什么意思
=====================================

经常在英文计算机书籍或文章中看到invariant这个词，不过如果要我立刻说出它的意思，我的反应肯定是：**一愣**。本着对科学认真负责的态度，还是得上网搜索一下，以正视听，哇哈哈。

在著名的问答网站[知乎](http://www.zhihu.com/)上搜索invariant(s)无果，尝试“不变量”、“不变式”均无果。哼，知乎对计算机科学不够重视啊。在国外著名的问答网站[Quora](http://www.quora.com)也没找到精确结果，囧；只能求助程序员问答网站[Stackoverflow](http://stackoverflow.com)了，Bingo！果然给力，答案[在这](http://stackoverflow.com/questions/112064/what-is-an-invariant)。为了更清晰地解释这个概念，我把原文翻译成中文如下：

<!-- more -->
An invariant is more "conceptual" than a variable. In general, it's a property of the program state that is always true. A function or method that ensures that the invariant holds is said to maintain the invariant.

For instance, a binary search tree might have the invariant that for every node, the key of the node's left child is less than the node's own key. A correctly written insertion function for this tree will maintain that invariant.

As you can tell, that's not the sort of thing you can store in a variable: it's more a statement about the program. By figuring out what sort of invariants your program should maintain, then reviewing your code to make sure that it actually maintains those invariants, you can avoid logical errors in your code.

[译文]不变性（或不变量）比变量更加“概念化”一些。通常来说，它指的是程序状态的一个属性，这个属性的特点是永远为真。能够确保不变性维持不变的函数或方法，叫做维持不变性。

例如，一个二叉搜索树可能有一个不变性，即对每个节点来说，它的左子节点键值小于节点本身的键值。对于这棵树来说，编写正确的插入函数会维持这个不变性。

这样你就明白了，不变性不是那种存储到变量中的东西，而是对于程序的一个声明。通过弄清楚你的程序应该维持什么类型的不变性，然后检查你的代码以确保维持了那些不变性，你就可以避免代码中的逻辑错误。[译文结束]

最后，从一般性概念来讲，我们可以参阅维基百科，其定义是 [Invariant(computer science)] [1]，中文版的比较简略：[不变条件] [2]。维基的定义稍微学术和抽象了一些，我们还是采纳Stackoverflow的解释。看，一个词都是学问，可见计算机科学之博大精深啊！

[1]: http://en.wikipedia.org/wiki/Invariant_(computer_science)
[2]: http://zh.wikipedia.org/wiki/%E4%B8%8D%E5%8F%98%E6%9D%A1%E4%BB%B6

**更新：关于invariant和immutability** 又翻到[Java程序员修炼之道](http://book.douban.com/subject/24841235/)，看到关于不可变性（应是immutability）的陈述：

不可变对象的应用是十分有价值的技术。这些对象或没有状态，或只有final域（因此只能在构造方法中赋值）。它们总是安全又活跃的。它们的状态不能修改，所以不可能出现不一致的情况。

在这段陈述之后，作者给出了创建不可变对象的一些方法和技术，例如使用工厂方法代替构造方法等。这里就有一个问题，invariant和immutability这两个名词到底是什么关系？查阅后才发现，实际上invariant和immutability不是一个概念。如Stackoverflow中的[回答](http://stackoverflow.com/questions/12749749/for-oop-are-immutable-and-invariant-synonymous)所述：

Immutable refers to an object not changing during it's lifetime.

 * An immutable string. If you concatenate, it creates a new string. The original one is unchanged.

Invariants are guarantees that don't change for a specified duration. They do not have to explicitly exist as attributes or values.

 * Object must be in a valid state at all times.
 * Object must be in state-X to perform operation-Y.
 * If the operation-X is called, the object is guaranteed to be in state-X.
 * Entity can be a Company or a Person, but cannot be both at the same time.
 * A file cannot be both opened and closed at the same time.

同时，如果想进一步了解不可变对象的特点话，可以参阅SO的另一篇回答 [Mutable vs immutable objects](http://stackoverflow.com/questions/214714/mutable-vs-immutable-objects?rq=1)。

综上，在中文里，我们可以采用如下表述：

 * invariant 不变量，不变性，不变条件
 * immutability 不可变性
 * immutable object 不可变对象
