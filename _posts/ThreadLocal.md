title: ThreadLocal
date: 2014-11-08 11:56:59
tags:
 - Java
 - Concurrency
---


>当访问共享的可变数据时，通常需要使用同步。一种避免使用同步的方式就是不共享数据。如果仅在单线程内访问数据，就不需要同步。这种技术被称为线程封闭，它是实现线程安全性的最简单方式之一。……在Swing中大量使用了线程封闭技术。……线程封闭技术的另一种常见应用是JDBC的Connection对象。

>Java语言及其核心库提供了一些机制来帮助维持线程封闭性，例如局部变量和ThreadLocal类，但即便如此，程序员仍然需要负责确保封闭在线程中的对象不会从线程中逸出。

<!-- more -->

<strong>线程封闭</strong>的实现方式分为：
 - <strong>Ad-hoc线程封闭</strong>：完全由程序实现来确保线程封闭性，非常脆弱。
 - <strong>栈封闭</strong>：局部变量的固有属性之一就是封闭在执行线程中，它们位于执行线程的栈中，其他线程无法访问。比Ad-hoc更易于维护、更加健壮。需要注意的是基本类型的局部变量始终封闭在线程内（Java语言的语义保证），但是对象类型的局部变量则需要格外小心确保不会逸出。
 - <strong>ThreadLocal类</strong>：这是维持线程封闭的规范方法。

>这个类能使线程中的某个值与保存值的对象关联起来。ThreadLocal提供了get与set等访问接口或方法，这些方法为每个使用该变量的线程都存有一份独立的副本，因为get总是返回由当前执行线程在调用set时设置的最新值。

下面是来自网上的一个例子，我稍微修改了一下，这样打印结果更容易理解：

```
public class ThreadLocalExample {
    public static class MyRunnable implements Runnable {
        private ThreadLocal<Integer> threadLocal =
                new ThreadLocal<Integer>();

        @Override
        public void run() {
            int myValue = (int) (Math.random() * 100D);
            System.out.println(Thread.currentThread().getName()
                + ": my value is set:"+ myValue);

            threadLocal.set(myValue);

            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
            }

            System.out.println(Thread.currentThread().getName()
                + ": my value is:"+ threadLocal.get());
        }
    }


    public static void main(String[] args) {
        MyRunnable sharedRunnableInstance = new MyRunnable();

        Thread thread1 = new Thread(sharedRunnableInstance);
        Thread thread2 = new Thread(sharedRunnableInstance);

        thread1.start();
        thread2.start();
    }

}

```

运行结果如下：
```
Thread-0: my value is set:95
Thread-1: my value is set:27
Thread-1: my value is:27
Thread-0: my value is:95
```

### 参考资料
 - 文中引用部分摘自《Java并发编程实战》
 - 例子代码来自：http://tutorials.jenkov.com/java-concurrency/threadlocal.html
