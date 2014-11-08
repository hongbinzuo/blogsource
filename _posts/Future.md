title: Future
date: 2014-11-07 20:04:44
tags:
 - Java
 - Concurrency
---

之前在看《Java程序员修炼之道》（主要讲的是Java 7的新特性）的时候就看过并发这块儿，但是感觉看完过段儿时间印象也有点儿模糊。最近重温Java并发编程，拿起了《Java并发编程实战》，只能用四个字儿来形容：干货太多。书里讲的几乎没有废话，大部分例子也都不错，对于理解新的Java并发编程模型很有帮助。不过，也有些例子可能受篇幅所限，讲解的不够细致，所以我就需要从网上再找些相对丰富的例子补充上以加深理解。Future就是其中一例。

<!-- more -->

下面的代码段摘自[java.util.concurrent.Future Basics](http://java.dzone.com/articles/javautilconcurrentfuture)，感觉这篇教程讲解虽然基础但是很清晰，看看代码基本上就理解Future的简单用法了。

### 单线程应用

```
public String downloadContents(URL url) throws IOException {
    try(InputStream input = url.openStream()) {
        return IOUtils.toString(input, StandardCharsets.UTF_8);
    }
}

//...

final String contents = downloadContents(new URL("http://www.example.com"));
```

### 使用Future接口，并行处理

```
public static Future<String> startDownloading(URL url) {
    //...
}

final Future<String> contentsFuture = startDownloading(new URL("http://www.example.com"));
//other computation
final String contents = contentsFuture.get();
```

### 调用isDone方法判断是否执行完成

```
final Future<String> contentsFuture = startDownloading(new URL("http://www.example.com"));
while (!contentsFuture.isDone()) {
    askUserToWait();
    doSomeComputationInTheMeantime();
}
contentsFuture.get();
```

### 取消任务

```
contentsFuture.cancel(true);    //meh...
```

### 两种获得Future实例的方法

#### 使用线程池
```
private final ExecutorService pool = Executors.newFixedThreadPool(10);

public Future<String> startDownloading(final URL url) throws IOException {
    return pool.submit(new Callable<String>() {
        @Override
        public String call() throws Exception {
            try (InputStream input = url.openStream()) {
                return IOUtils.toString(input, StandardCharsets.UTF_8);
            }
        }
    });
}
```

#### 使用容器，如Spring或EJB
```
@Async
public Future<String> startDownloading(final URL url) throws IOException {
    try (InputStream input = url.openStream()) {
        return new AsyncResult<>(
                IOUtils.toString(input, StandardCharsets.UTF_8)
        );
    }
}
```

代码实例能帮助理解，同时也要通读一下原文，注意其中的一些细节，比如超时和中断的处理逻辑等等。

最后，我们摘抄《Java并发实战》第7章的例子看看相对完整的一个取消操作是怎么完成的：

```
public static void timedRun(Runnable r, long timeout, TimeUnit unit) throws InterruptedException {
  Future<?> task = taskExec.submit(r);
  try {
    task.get(timeout, unit);
  } catch(TimeoutException e) {
    // 接下来的任务将被取消
  } catch(ExecutionException e){
    // 如果在任务中抛出了异常，那么重新抛出异常
    throw launderThrowable(e.getCause());
  } finally {
    // 如果任务已经结束，那么执行取消操作也不会带来任何影响
    // 如果任务正在运行，那么将被中断
    task.cancel(true);
  }
}
```

### 参考资源

 - http://www.cnblogs.com/hanyuan/archive/2013/03/10/2952229.html
 - http://blog.csdn.net/lingchixin/article/details/38906849
 - http://10kloc.wordpress.com/2013/12/24/cancelling-tasks-in-executors/
 - http://www.javacodegeeks.com/2011/09/java-concurrency-tutorial-callable.html
 - http://www.journaldev.com/1090/java-callable-future-example
