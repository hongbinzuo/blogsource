title: REST client scala script
date: 2014-02-19 19:32:42
tags:
 - Scala
---

*This post is written in English*, because I read [one article](http://michaelochurch.wordpress.com/2012/07/27/six-languages-to-master/) recently that says English is one of the key (programming) languages you need to master. I cannot agree more, :). English is very important for progammers, especially if you want to be a top programmer in specific area. There are much more great resources in English than in other languages, so why not start to write some posts or articles in English and make yourself comfortable with reading, writing and thinking? I appologize for any readers of this blog who do not master English well, but I have to do it for me and for you, because anyhow we need improve ourselves up to the next level and it's almost impossible without English. Get used to it and you'll be happy with it soon.

<!-- more -->

At the end of Chapter 2 of *Scala in action*, there is one example used to revisit Scala features introduced in this chapter. It is called HTTP REST client that can communicate with server side via RESTful requests and responses. In the last post, I have given the method to setup a simple servlet to handle HTTP requests and here I copy the complete example servlet from the book and list it as below,

```
/**
 * Class: RestServlet.java
 */
package com.freelemon;

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;

public class RestServlet extends HttpServlet {
	public void doGet(HttpServletRequest request, HttpServletResponse response)
	  throws ServletException, IOException {
	  	PrintWriter out = response.getWriter();
	  	out.println("Get method called.");
	  	out.println("parameters: " + parameters(request));
	  	out.println("headers: " + headers(request));
	  }

	public void doPost(HttpServletRequest request, HttpServletResponse response)
	  throws ServletException, IOException {
	  	PrintWriter out = response.getWriter();
	  	out.println("Post method called.");
	  	out.println("parameters: " + parameters(request));
	  	out.println("headers: " + headers(request));
	  }

	public void doDelete(HttpServletRequest request, HttpServletResponse response)
	  throws ServletException, IOException {
	  	PrintWriter out = response.getWriter();
	  	out.println("Delete method called");
	  }

	private String parameters(HttpServletRequest request) {
		StringBuilder builder = new StringBuilder();
		for (Enumeration e = request.getParameterNames() ; e.hasMoreElements();)
		{
		String name = (String)e.nextElement();
		builder.append("|" + name + "->" + request.getParameter(name));
		}
		return builder.toString();
	}
	private String headers(HttpServletRequest request) {
		StringBuilder builder = new StringBuilder();
		for (Enumeration e = request.getHeaderNames() ; e.hasMoreElements();) {
		String name = (String)e.nextElement();
		builder.append("|" + name + "->" + request.getHeader(name));
		}
		return builder.toString();
	}
}
```

We have this servlet running at server side with the help of Gradle and its Jetty plugin. So before we move to client side, we need first make sure it works fine by openning a browser to test it with a url like `http://localhost:8080/chapter2/`, the web app name may vary depending on your build directory. Then, a similar response will be shown as follows,

```
Get method called.
parameters: 
headers: |Host->localhost:8080|Connection->keep-alive|Accept->text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8|User-Agent->Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.107 Safari/537.36|Accept-Encoding->gzip,deflate,sdch|Accept-Language->en-US,en;q=0.8
```

At the client side, we need to write a Scala script to implement a lightweight RESTful application. Since the complete code has been presented in the book, we just copy it here:

```
// RestClient.scala
import org.apache.http._
import org.apache.http.client.entity._
import org.apache.http.client.methods._
import org.apache.http.impl.client._
import org.apache.http.client.utils._
import org.apache.http.message._
import org.apache.http.params._

def parseArgs(args: Array[String]): Map[String, List[String]] = {
	def nameValuePair(paramName: String) = {
		def values(commaSeparatedValues: String) = commaSeparatedValues.split(",").toList

	    //val index = args.findIndexOf(_ == paramName)
	    // the original findIndexOf is wrong, instead, we use indexWhere
	    //https://github.com/nraychaudhuri/scalainaction/pull/1
	    val index = args.indexWhere(_ == paramName)
	    (paramName, if(index == -1) Nil else values(args(index+1)))
	}

	Map(nameValuePair("-d"), nameValuePair("-h"))

}

def splitByEqual(nameValue: String): Array[String] = nameValue.split('=')

def headers = for(nameValue <- params("-h")) yield {
	def tokens = splitByEqual(nameValue)
	new BasicHeader(tokens(0), tokens(1))
}

def formEntity = {
	def toJavaList(scalaList: List[BasicNameValuePair]) = {
		java.util.Arrays.asList(scalaList.toArray:_*)
	}

	def formParams = for(nameValue <- params("-d")) yield {
		def tokens = splitByEqual(nameValue)
		new BasicNameValuePair(tokens(0), tokens(1))
	}

	def formEntity = new UrlEncodedFormEntity(toJavaList(formParams), "UTF-8")
	formEntity
}

def handlePostRequest = {
	val httppost = new HttpPost(url)
	headers.foreach{httppost.addHeader(_)}
	httppost.setEntity(formEntity)
	val responseBody = new DefaultHttpClient().execute(httppost,new BasicResponseHandler())
	println(responseBody)
}

def handleGetRequest = {
	val query = params("-d").mkString("&")
	val httpget = new HttpGet(s"${url}?${query}")
	headers.foreach { httpget.addHeader(_)}

	val responseBody = new DefaultHttpClient().execute(httpget, new BasicResponseHandler())
	println(responseBody)
}

def handleDeleteRequest = {
	val httpDelete = new HttpDelete(url)
	val httpResponse = new DefaultHttpClient().execute(httpDelete)
	println(httpResponse.getStatusLine())
}

def handleOptionsRequest = {
	val httpOptions = new HttpOptions(url)
	headers.foreach { httpOptions.addHeader(_)}
	val httpResponse = new DefaultHttpClient().execute(httpOptions)
	println(httpOptions.getAllowedMethods(httpResponse))
}

require(args.size >= 2, "at minimum you should specify action(post, get, delete, options) and url")

val command = args.head
val params = parseArgs(args)
val url = args.last

command match {
	case "post" => handlePostRequest
	case "get" => handleGetRequest
	case "delete" => handleDeleteRequest
	case "options" => handleOptionsRequest
}

```
The first thing I encountered when I was trying to execute this script is classpath, yes, I remember it is also the first thing when I ran my first Java program, it annoyed me at that time. Programmers mainly care about programs instead of environments, but sometimes environment may take us more time than real programming, but we have to face it directly. Scala program(scala) cannot recognize classpath by environment variable `$CLASSPATH` by default, so I tried to use the argument `-usejavacp` to let it happen, but no luck. Then I ran scala with another argument `-classpath` to indicate specific classpath, in our case, it is httpclient's location. The weird thing is the wildcard "\*" or "\*.jar" doen't work either, so I have to list all the jar files one by one, as shown below,

```
scala -classpath "/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/commons-codec-1.6.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/commons-logging-1.1.3.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpcore-4.3.1.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpclient-4.3.2.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpmime-4.3.2.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/fluent-hc-4.3.2.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpclient-cache-4.3.2.jar" RestClient.scala 
```

Maybe it's my own environment issue, anyway, I don't feel scala works well with classpath.

The second thing is the method `findIndexOf` is deprecated from Scala 2.9.1, another method called `indexWhere` should be used instead, more details can be found at [https://github.com/nraychaudhuri/scalainaction/pull/1](https://github.com/nraychaudhuri/scalainaction/pull/1).

The last thing is the httpclient library. This library is good but it is easily changed from version to version. So don't panic if you get any deprecation message. Just check the documentation to see the current way of usage.

For the code itself, we need to notice the difference between `def` and `val`, we can refer to the answer in [this thread](http://stackoverflow.com/questions/3646756/scala-def-versus-val) of Stackoverflow, which explains it clearly: *val is evaluated on initialization while def is evaluated only when, and every time, the function is called.*

OK, so far so good. Run it and we will get the response. It rocks. :D

```
scala -classpath "/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/commons-codec-1.6.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/commons-logging-1.1.3.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpcore-4.3.1.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpclient-4.3.2.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpmime-4.3.2.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/fluent-hc-4.3.2.jar:/Users/admin/Downloads/httpcomponents-client-4.3.2/lib/httpclient-cache-4.3.2.jar" RestClient.scala get http://localhost:8080/chapter2
```


###References
1. Code samples for *Scala in action* are available at its [official website](http://www.manning.com/raychaudhuri/)
2. An article about Scala script: [Scala as a scripting language](http://www.codecommit.com/blog/scala/scala-as-a-scripting-language)
