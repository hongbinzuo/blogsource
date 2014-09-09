title: Appfuse (2)
date: 2014-03-28 09:09:15
tags:
 - appfuse
 - maven
 - Java
---

书接上文。

Eclipse里编译成功之后，下一个要执行的任务是下载Appfuse的全部源码。按照官网的方法就是一条命令，很简单：`mvn appfuse:full-source`，但实际的过程往往并不顺利。

首先要注意的是，在下载源码之前不要修改pom.xml，否则可能遇到一些奇怪的问题。

<!-- more -->

###代理问题

在下载源码的过程中，遇到了几个Connection Time Out的问题，所以要注意设置系统的代理、Maven的代理和SVN的代理。具体命令如下，其中系统环境的代理是否设置根据自己的网络情况而定：

```
D:\appfuse-demo> set http_proxy=PROXY_HOST:PROXY_PORT

D:\appfuse-demo> set https_proxy=PROXY_HOST:PROXY_PORT

D:\appfuse-demo> set MAVEN_OPTS=-Dhttp.proxyHost=PROXY_HOST -Dhttp.proxyPort=PROXY_PORT -Dhttps.proxyHost=PROXY_HOST -Dhttps.proxyPort=PROXY_PORT
```

SVN的连接超时问题，需要设置SVN的代理，即修改server配置文件，这个文件一般存放在`%APPDATA%\Subversion`下，其中有很多注释的配置，打开代理这一项设置即可：

```
[global]
http-proxy-host = ProxyServerHost
http-proxy-port = Port
```

如果出现错误，在Eclipse里重新保存pom.xml，也就是恢复成原始的pom.xml，错误就可以去除。吐槽：各种代理设置是最烦人滴，你们就不能都用操作系统或浏览器的网络代理吗？

###小错误

为了避免文件更新冲突，我关闭了Eclipse中的项目，在配好一切代理的情况下下载，总体是成功的，只是有一个文件hibernate.properties需要手动删除。


###Jetty插件

full-source下载成功之后，可以通过命令行的方式运行Appfuse，运行命令是：

```
D:\appfuse-demo> mvn jetty:run
```

但是没有Jetty插件，需要下载，配置了Maven的settings.xml文件几次之后还是不能成功，找到这个Plugin的[主页](https://docs.codehaus.org/display/JETTY/Maven+Jetty+Plugin)，原来很简单，增加一个pluginGroup即可。

```
<profile>
  ...
  <pluginGroups>
    <pluginGroup>org.mortbay.jetty</pluginGroup>
  </pluginGroups>
</profile>
```

Jetty可以运行了不代表一切工作良好，下一篇会讲讲具体的编译和运行方法。

###M2E

因为下载了全部源代码，Eclipse又得重新编译，哦，麦糕德～！使用Eclipse和m2e搭配工作最大的好处就是**特别杀时间**；如果你想高效，一定要谨慎注意你的每个操作，否则极有可能进入貌似有希望实则希望渺茫的漫长等待中。比如现在的这个例子：重新编译。在Eclipse里我尝试使用Maven/Update Project的方式更新依赖，重建项目，最后可耻地失败了。我想，重头来可能更靠谱，于是删除现有项目，然后重新导入，还是有错，来回折腾真是能憋出内伤啊。于是想到一不做二不休，干脆不用内嵌的Maven来编译了，用刚弄好的命令行Maven就OK了。参考这篇Maven绝杀技巧：[missing artifact but jars are in place](http://stackoverflow.com/questions/6111408/maven2-missing-artifact-but-jars-are-in-place)。我们用到了[这个技巧](http://books.sonatype.com/m2eclipse-book/reference/preferences.html#fig-preferences-maven-installations)，使用外部Maven管理依赖，经过反复Update之后，一切终于安静了。

为了庆祝这个阶段性成果，我果断消灭了两个枇杷！

且听下回分解。

###参考链接

 - 文中有些内容参考这篇博客，表示感谢：[飞哥也是哥](http://hi.baidu.com/imlidapeng/item/6ff00536ea0107ffa884288a)。
