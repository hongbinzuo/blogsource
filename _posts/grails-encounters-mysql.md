title: 当Grails遇上MySQL
date: 2014-01-23 16:49:03
tags:
 - grails
 - Java

---

### 引语
在Grails官方网站推荐的教程里，选择了一个[初学者教程](http://grails.asia/grails-tutorial-for-beginners/)，看起来不费力。前面讲解一些理论知识如MVC、Groovy、ORM等，讲得不错，简明扼要；然后讲到GORM，这个还是需要动手实验一下的，但是[文中的教程](http://grails.asia/grails-tutorial-for-beginners-introduction-to-gorm/)实操性不强，于是找到另一篇[Grails/MySQL的使用指南](http://learnedstuffs.wordpress.com/2012/02/21/using-mysql-as-database-in-grails/)做实验（官方没有这方面的详细教程）。

<!-- more -->

### 实验过程

以下的实验在Windows 7电脑上完成。

前面一切正常，因为本机没有MySQL所以新装了MySQL数据库。需要注意的是MySQL JDBC的包是在更新的，所以需要从官网单独下载安装，最好是下载MSI安装版而不是ZIP包，下载的时候会提示注册或登录，忽略即可，直接点击最下面的链接下载即可。*注意：它的版本和MySQL Server的版本不一样。*

安装完成之后，将其添加到系统路径，并修改`BuildConfig.groovy`如下：

```
dependencies {
    // specify dependencies here under either 'build', 'compile', 'runtime', 'test' or 'provided' scopes e.g.
    runtime 'mysql:mysql-connector-java:5.1.28'    
}
```

本指望能顺利通过，结果出现下面的错误：

```
| Configuring classpath
| Error Resolve error obtaining dependencies: Failed to read artifact descriptor for mysql:mysql-connector-java:jar:5.1.28 (Use --stacktrace to see the full trace)
```

为了解决这个错误，我先后尝试了三种方法，其中前两种（添加MySQL JDBC的Jar包到应用的lib目录；给grails命令设置代理）均告失败，错误依旧。最后想到其实这应该是maven管理依赖的问题，但实际上我把MySQL JDBC的Jar放在本地lib目录之后，应该不需要了，索性注释掉这个依赖，问题解决。

```
dependencies {
    // specify dependencies here under either 'build', 'compile', 'runtime', 'test' or 'provided' scopes e.g.
    //runtime 'mysql:mysql-connector-java:5.1.28'    
}
```

解决了这个问题，以下就比较顺利了，完成！

<img alt="MySQL中Person表自动创建" src="/img/person.png" style="width:600px"/>

<img alt="Grails自动创建的CRUD页面" src="/img/webperson.png" style="width:600px"/>

### 感受

这个实验过程中我的一些体验和思考：

<strong>糟糕体验1</strong>：（和Grails无关）MySQL Connector J在安装完之后默退，居然也不提示成功与否，以为有兼容性问题，这体验真不咋地，浪费时间的小坑一个。最后还是在本地硬盘搜索才找到，路径位于`C:\Program Files (x86)\MySQL\MySQL Connector J`，这种情况也可以打开资源浏览器并定位到相应目录啊，啊。

<strong>糟糕体验2</strong>：grails这个命令执行起来速度比较慢，在出错的情况下基本上已经超过了我的忍耐极限（如果顺利执行还可以接受），而且在执行过程中很难中断（多次`Ctrl+C`无效），我终于明白为什么Grails难以流行了：程序员等机器的感受很不爽。

<strong>良好体验</strong>：总体流程比较简洁，需要配置和写的代码很少，生产率确实高！

<strong>思考</strong>：maven的包管理方面需要多了解一下，避免再栽入小坑儿。这个例子还没有完整体现出GORM的强大，需要继续跟进！

### 参考

 - 关于如何在Grails中使用MySQL的[一篇中文文章](http://hcleon.iteye.com/blog/1784216)
 - 如何[使用Java连接MySQL](http://stackoverflow.com/questions/2839321/java-connectivity-with-mysql/2840358#2840358)
 - [Grails如何手动安装依赖](http://grails.org/doc/2.3.x/ref/Command%20Line/install-dependency.html)


