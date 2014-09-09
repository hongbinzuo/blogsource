title: A quick web application with SBT
date: 2014-03-19 19:18:01
tags:
 - Scala
 - SBT
---

In the chapter 6 of *Scala in action*, the author decides to show something concrete. The example is a web application that provide Kanban service. It's called **weKanban**. In order to get this example to run, there's something to do for project setup, Scala web development and database development and so on. Here I would like to briefly describe the procedure to get it working for current environment, because some libraries used by the example are outdated in the book.

<!-- more -->

The very first thing is sbt. In the previous example, the HTTP client sample, I did not follow the instruction to setup SBT(Simple Build Tool). Instead, I used Gradle and its jetty plugin. If this time I still insist on Gradle, then I may encounter some unexpected problem, so I have to turn the build tool to SBT to make it easy. Anyway, I need to learn SBT gradully, after all, SBT is the first choice for Scala programming.

The first step is to create the project skeleton for weKanban. This step really took me some time, and I think it is a bad idea to remove the support for project template since after SBT version 0.7, because none of the alternative ways is easy. There are actually three ways mentioned in *Scala in action*, one is **np**, one is **giter8**, and the last one is command. I tried them one by one and tried to fix the problems, but at last, I lost my patience and created the directory mannually. giter8 is still hard to setup, it requires **conscript** first and this conscript didn't work after many attempts.. Even at last I installed it correctly, giter8 still cannot get the project template correctly. Although the author said giter8 nearly becomes the standard way to create Scala projects, I dont like it. 

So, I end up with creating the project structure by hand. It looks like below,

```
bash-3.2$ tree .
.
├── build.sbt
├── lib
├── project
│   ├── build.properties
│   ├── build.scala
│   ├── plugins.sbt
│   ├── project
│   │   └── target
│   └── target
├── src
│   ├── main
│   │   ├── java
│   │   ├── resourcs
│   │   ├── scala
│   │   │   └── weKanban.scala
│   │   └── webapp
│   │       ├── WEB-INF
│   │       │   ├── target
│   │       │   └── web.xml
│   │       ├── css
│   │       ├── index.html
│   │       └── js
│   ├── target
│   └── test
│       ├── java
│       ├── resources
│       └── scala
└── target
```

Note: all the directories named 'target' were genereated automatically by SBT, so dont create them manually.

The second step is to make sure SBT has been installed correctly and it works well with required plugins and libraries,

```
bash-3.2$ sbt
[info] Loading project definition from /Users/admin/Scala/projects/weKanban/project
[info] Set current project to weKanban (in build file:/Users/admin/Scala/projects/weKanban/)
> sbt-version
[info] 0.13.1
> scala-version
[info] 2.10.3
```

The content of *build.sbt* is different from the original one in the book. It is shown as follows, the main difference is the Scala version, jetty's dependency details and the xsbt webplugin path:
```
name := "weKanban"

organization := "scalainaction"

version := "0.1"

scalaVersion := "2.10.0"

scalacOptions ++= Seq("-unchecked", "-deprecation")

libraryDependencies ++= Seq(
  "org.scalaz" %% "scalaz-core" % "6.0.3",
  "org.scalaz" %% "scalaz-http" % "6.0.3",
  "org.eclipse.jetty" % "jetty-webapp" % "9.1.0.v20131115" % "container",
  "org.eclipse.jetty" % "jetty-plus"   % "9.1.0.v20131115" % "container"
)

seq(com.earldouglas.xsbtwebplugin.WebPlugin.webSettings :_*)
```

I also changed the content of *build.properties* to ensure it reflects the correctly used version,
```
sbt.version=0.13.1
```

And of course the content of *plugin.sbt* as below,
```
addSbtPlugin("com.earldouglas" % "xsbt-web-plugin" % "0.7.0")
```

After all these are set up, the simple web application can be started via SBT. Of course, you need follow the instructions of the book to copy the content of *web.xml* and *index.html* and most importantly the file *weKanban.scala*. I'd ignore the first two and only list the content of the scala source file to illustrate its usage of Scalaz library in order to implement a simple Servlet,
```
package com.kanban.application

import scalaz._
import Scalaz._
import scalaz.http._
import response._
import request._
import servlet._
import HttpServlet._
import Slinky._

final class WeKanbanApplication extends StreamStreamServletApplication {
	val application = new ServletApplication[Stream, Stream] {
		def application(implicit servlet: HttpServlet, servletRequest: HttpServletRequest, request: Request[Stream]) = {
			def found(x: Iterator[Byte]): Response[Stream] = OK << x.toStream
			HttpServlet.resource(found, NotFound.xhtml)
		}
	}
}
```

So far so good. Given all the files are ready, we come to the third step: we can launch the web server now to show the result. Here the book author said 'jetty-run' command, I'd say it's replaced with the command 'container' inside SBT like below, 
```
> container:start
2014-03-19 16:05:02.091:INFO:oejs.Server:pool-6-thread-4: jetty-9.1.0.v20131115
2014-03-19 16:05:03.102:INFO:oejw.StandardDescriptorProcessor:pool-6-thread-4: NO JSP Support for /, did not find org.apache.jasper.servlet.JspServlet
2014-03-19 16:05:03.106:INFO:oejsh.ContextHandler:pool-6-thread-4: Started o.e.j.w.WebAppContext@3d4dd7e7{/,[file:/Users/admin/Scala/projects/weKanban/src/main/webapp/],AVAILABLE}
2014-03-19 16:05:03.174:INFO:oejs.ServerConnector:pool-6-thread-4: Started ServerConnector@4def267d{HTTP/1.1}{0.0.0.0:8080}
[success] Total time: 1 s, completed 2014-3-19 16:05:03
```

Finally let's see the result:
```
$ curl -i localhost:8080/index.html
HTTP/1.1 200 OK
Content-Length: 85
Server: Jetty(9.1.0.v20131115)

<html>
    <body>
      <h1>weKanban board will come shortly</h1>
    </body>
</html>
```

OK, so I ended learning this chapter and learned some knowledge about Scala web development and SBT. The next step is to read the next chapter and complete this example for some useful user stories.


######References

 - [How to setup SBT](http://www.scala-sbt.org/release/docs/Getting-Started/Setup.html)
 - [xsbt web plugin](https://github.com/earldouglas/xsbt-web-plugin/wiki)






