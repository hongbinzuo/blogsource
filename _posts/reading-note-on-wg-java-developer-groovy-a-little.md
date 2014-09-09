title: Reading Note on WG Java Developer Groovy a little
date: 2014-01-13 10:25:01
tags:
 - Java
 - Groovy
 - reading
---

《Java程序员修炼之道》之Groovy入门
===============================================

### 简介

Groovy是JVM上的一种动态语言，主要用来解决快速Web开发、原型设计、脚本处理以及其他很多问题。一个简单的例子是把Java Bean转成XML输出，使用Java会比较笨拙，而用Groovy完成则非常简洁。Groovy实现的Java不具备的几个语言特性如下：

 - 函数字面值（[闭包] [1]）
 - 对集合的一等（即语法内置）支持
 - 对正则表达式的一等支持
 - 对XML处理一等支持

<!-- more -->

### 简化特性
 
 - 默认导入：不需要显示import的包，包括`groovy.lang.\*`, `groovy.util.\*`, `java.lang.\*`, `java.io.\*`, `java.math.BigDecimal`, `java.math.BigInteger`, `java.net.\*`, `java.util.\*`；使用和Java相同的语法导入更多的类
 - 数字处理：采用了最小意外原则，底层使用`BigDecimal`表示浮点数。解决Java中`BigDecimal`的问题：采用字符串初始化`BigDecimal`，并正确支持BEDMAS（括号、次方、除法、乘法、加法和减法）。Java中BigDecimal问题的例子如下（猜猜结果是什么）：
 ```
 BigDecimal x = new BigDecimal(3);
 BigDecimal x = new BigDecimal(0.2);
 System.out.println(x.add(y));
 ```
 - Groovy是动态类型语言，同时支持静态类型用法
 - Groovy中类的作用域和Java相同；Groovy脚本的作用域和其他脚本的相似，但并不完全一样，注意。 
 - 列表和映射的语法更简洁

### 新手陷阱
 
 - 可选的分号和返回语句：返回语句返回最后一个表达式的值
 - 可选的参数括号：如果不存在二义性，括号可以省略
 - 访问限定符：默认访问权限是`public`，所以所有`public`可以去掉
 - 不区分已检查异常和未检查异常，书中没说清楚
 - 相等把`==`当作Java中的`equals`方法
 - 内部类，一般使用函数字面值（闭包）代替

### Java不具备的Groovy特性

 - GroovyBean：详细了解的话可以参考[官方网站](http://groovy.codehaus.org/Groovy+Beans)，第一是简化，第二是加入属性规则例如只读属性设定，通过这个例子可以知道，Groovy会比Java省很多代码
 - 安全解引用操作符：就是使用神奇的?.省去很多判断`null`的代码！更详细参考[NullObjectPattern](http://groovy.codehaus.org/Null+Object+Pattern) 
 - 猫王操作符：`?:`的作用，例如：
 ```
 String agentStatus = "Active"
 String status = agentStatus ?: "Inactive"
 ```
 - 增强型字符串：更多详情参见 [GString](http://groovy.codehaus.org/Strings+and+GString)
 - 内置的集合操作：减少套路化代码，且容易看懂和维护。使用`it`变量使代码更加简洁。
 - 对正则表达式的支持：简单的例子对比Java和Groovy的实现方式。
 - 简单的XML处理
 - Groovy与Java的合作：互操作，如何调用；Java->Groovy：BSF，GroovyShell，GroovyClassLoader，GroovyScriptEngine

### 总结见图

<img alt="Groovy入门小结（高清慎入）" src="/img/wg_java_groovy.jpg" style="width: 600px;"/>

[1]: http://zh.wikipedia.org/wiki/%E9%97%AD%E5%8C%85_(%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)
