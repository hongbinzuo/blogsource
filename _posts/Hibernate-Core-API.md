title: Hibernate Core API
date: 2014-11-06 21:11:49
tags:
 - Java
 - JavaEE
 - Hibernate
---

整理一下Hibernate核心API的笔记，感谢马老师。因为博客的发布形式，中间内容有些节略和修改。

## 关于API文档
因为Hibernate是属于JBoss的，按照JBoss的商业模式，文档和技术支持是收费的，所以官方不提供离线文档下载，只提供在线文档查看。当然，总有热心的网友看不过去，所以网上有非官方整理的API文档可供参考。

<!-- more -->

## Configuration
 - AnnotationConfiguration 基于注解的配置
 - 配置信息管理
 - 用来产生SessionFactory
 - 可以在configure方法中指定Hibernate配置文件
 - 只关注一个方法即可：buildSessionFactory

## SessionFactory
 - 用来产生和管理Session
 - 通常情况下，每个应用只需要一个SessionFactory （单例），除非要访问多个数据库
 - 关注两个方法即可
   - openSession每次都是新的，需要close
   - getCurrentSession从上下文找，如果有，用已有的，否则，创建新的
     - 用途，界定事务边界
     - 事务提交后自动close
     - 上下文配置可参见XML文件中`current_session_context_classs`属性
     - `current_session_context_classs`属性取值JTA和thread常用，managed和custom.class较少使用
       - thread：使用Connection连接的数据库管理事务
       - JTA（Java Transaction API）：Java分布式事务管理（多数据库访问），JTA由中间件提供（JBoss、Weblogic等，Tomcat不支持）

## Session
 - 管理一个数据库的任务单元（简单说就是增删改查），中文名为“会话”
 - 方法（CRUD）
  - Save `session.save(对象)`
  - Delete `session.delete(对象)`
  - Load `Student s1=(Student)session.load(Student.class, 1);`
  - Get `Student s1=(Student)session.get(Student.class, 1);`
  - Get与Load的区别（原理，面试重点）
    - 不存在对应记录时表现不一样
    - Load返回的是代理对象,等到真正用到对象内容时才发出SQL语句
    - Get直接从数据库加载不会延迟
  - Update `session.update(对象)`
    - 用来更新detached对象，更新完成后转为persistent
    - 更新transient对象会报错
    - 更新自己设定ID的transient对象可以（数据库有对应记录）
    - persistent状态的对象只要设定（如:t.setName…）不同字段就会更新
    - 更新部分更改的字段
      - XML配置文件中设定property标签的update属性，annotation设定 @Column 的 updatable属性，不过这种方式很少用，因为不灵活
      - 使用XML中的dynamic-update，JPA1.0 Annotation 没有对应的属性，可能为Hibernate扩展
       - 同一个session可以，跨session不行，不过可以用merge()(不重要）
    - 建议使用HQL(EJBQL)
  - saveOrUpdate方法
  - clear方法
    - 无论是load还是get,都会首先査找缓存（一级缓存)，如果没有，才会去数据库査找，调用clear()方法可以强制清除session缓存
  - flush方法
    - 当session的事务提交后,会强制将内存(session缓存)与数据库同步。默认情况下是session的事务提交(commit)时才同步!
    - session的FlushMode设置,可以设定在什么时候同步缓存与数据库(很少用)，例如: `session.setFlushMode(FlushMode.AUTO)`
  - find方法已过时

## SchemaExport (自动建表)
 - 了解使用方法即可：`new SchemaExport(new AnnotationConfiguration().configure()).create(false, true);`

## 查询接口
 - 参考Hibernate査询(HQL/EJBQL)的内容

## 注意
 - Hibernate中涉及很多非常细节的区别,但在实际应用中用得极少
  - 比如save和persist的区别
  - merge、evict 等方法
  - 比如 refresh、lock 等
 - 建议的学习方法，动手实验
