title: Hibernate Object States
date: 2014-11-07 13:26:34
tags:
 - Java
 - Hibernate
 - JavaEE
---

Hibernate是一种对象/关系映射的持久化框架，它做的主要工作之一就是对象和数据库表记录之间的状态管理。Hibernate编程环境中操作的对象指的是Entity POJO对象，它存在四种状态：Transient, Persistent, Detached和Removed。下面是从网上摘录的一幅图（源自Java Persistence with Hibernate这本书），非常好地说明了这几种状态之间的转换关系。

<!-- more -->
<img alt="Hibernate对象状态转换图" src="/img/object-states.JPG" style="width: 750px;"/>

从这幅图中，我们可以看到，
 - 对象刚刚创建时是Transient（瞬时）状态，意味着和数据库没有任何关系，只在内存中存在
 - 对象在保存或更新之后，进入Persistent（持久化）状态，此时数据库中已经有对象相应的记录，并生成了ID
 - 当调用Session的clear等方法后，对象从Persistent进入Detached状态，此时Hibernate从<strong>缓存</strong>中将此对象清除，但在数据库中依然存在
 - Detached状态和Persistent状态可以相互转换，如图所示，如果保存更新对象，对象又从Detached状态进入Persistent状态
 - 也可以通过load或get方法从数据库中获取该对象，从而直接进入Persistent状态
 - 最后，调用Session的delete方法，对象就进入了不可逆转的Removed状态

其实，这些状态变化还是比较符合常理的，所以只要了解基本原理，然后就可以写写代码验证即可。

### 参考
 - [The Hibernate Object Life-Cycle](http://learningviacode.blogspot.com/2012/02/hibernate-object-life-cycle.html)
 - [Hibernate Life Cycle](http://www.roseindia.net/hibernate/HibernateLifeCycle.shtml)
