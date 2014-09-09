title: Why Twitter Uses Java
date: 2014-03-14 23:49:28
tags:
 - Java
 - Scala
---

Rails在Web应用快速开发方面几乎很少有框架能与之媲美，但是Rails的性能和系统架构的友好性和Java平台相比可能还是存在一定的劣势。大多数的Web应用，Rails是足能抵挡的，比如现在Github在用Rails，而Twitter以前也主要用Rails。但是Twitter毕竟是一个数一数二的高并发大流量的网站，所以它总会对性能有更高的要求。下面的译文段落来自InfoQ中的[一篇访谈](http://www.infoq.com/articles/twitter-java-use)，主要是讲Twitter是为什么迁移部分代码和服务到Java平台的。

<!-- more -->

###译文

我们原来是一个Rails商店，我相信我们是世界上最大的Rails站点，但是当我们成长为一个组织，并且提供服务的时候，性能和封装问题就日益凸显了。我并不是说Rails在哪方面做的不好，只是我们的系统增长地太快太大了，而Rails不能适应。在我们这种情况下Rails有两点不太理想。

首先，Ruby的运行时比较慢，特别是和Java虚拟机（JVM）比起来的话，虽然我们已经在垃圾收集器上努力地使其达到较高的性能了。

其次，Rails所实现的LAMP模型有好几层，每一层都和上下层相互通信，却没有垂直封装，这样的模型不能在我们这样的组织里提供较好的服务。

因为我们一直都比较关注性能和封装，我们也通过缓存（cache）或者优化虚拟机解决了必要的性能问题。

现在Twitter的大部分请求都走Rails，但是当我们构建新的服务时，如果是从头开始，为了达到更好的封装性我们把服务放到JVM里，因为性能方面的考虑要远远比这些语言的生产力或者敏捷性方面的弱势更重要。所以，当我们重新构建Tweet存储时，我们就把它构建到Gizzard里作为同种类型的服务，然后暴露一个领域接口，那是一个Scala系统，划分并管理MySQL节点。所以，这样就可以从核心的Rails软件包里有效地消除ActiveRecord的使用。

队列的情况也是一样的；当我们想重新构建并封装队列的时候，为了性能的考虑我们在JVM上实现。所以，当那些轻量级的、面向服务的项目开始的时候，我们越来越多地考虑从核心的Rails应用中脱离开来。

另一方面，当把渲染代码迁移到基于浏览器的Javascript中时，我们从Rails的构建网页的模板模型里就得不到什么好处了。所以，我们从两端剥离关注，并且当我们重写代码的时候，在更快的软件栈上就更合理一些，因为性能对我们来说太重要了。我们是世界上最大的网站之一，但是和其他大的动态站点相比我们只是在很少的硬件资源上运行。

###原文

>We were originally a Rails shop, and I believe we are the largest Rails site in the world, but as we've grown as an organization, and as a service, performance and encapsulation have become very critical. I wouldn't say that Rails has served as poorly in any way, it's just that we outgrew it very quickly. So there are two things about Rails that make it no longer ideal for our situation.
First, the Ruby runtime is slow, particularly in comparison to the JVM. We've worked hard on the garbage collector to get reasonable performance.

>And also the LAMP model that Rails embodies, where you have a set of tiers each of which only talks to the one above and below, and no vertical encapsulation, doesn't serve a large organization like us very well.

>As we've been focusing on performance and encapsulation, we've fixed performance problems as necessary, with caches, or working on the VMs.

>The majority of requests on Twitter go through Rails right now, but as we build new services, if we choose to build them from scratch, in order to achieve better encapsulation we move them into the JVM, because the performance concerns outweigh any sort of productivity or agility downside those languages might have. So when we re-built Tweet storage we built it in Gizzard as a homogenous service, it exposes a domain interface, and that's a Scala system that partitions and manages uncoordinated MySQL nodes. So that effectively eliminated ActiveRecord use for tweets from the core Rails stack.

>The same with the queue; when we wanted to rebuild it and re-encapsulate it for performance reasons we wrote it on JVM. So as those kind of lightweight, service-oriented projects proceed, more and more concerns are being taken out of the core Rails application.

>On the opposite side, as we've moved the render code into browser-based JavaScript, we no longer get much benefit from Rails' templating model for building web pages. So we're pulling concerns out from both sides, and when rewrite them it makes sense to rewrite them in a faster stack, because performance is so critical for us. We're one of the largest websites in the world, but run on a very small hardware footprint compared to other big dynamic sites.