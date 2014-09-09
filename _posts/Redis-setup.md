title: Redis setup
date: 2014-09-06 11:42:09
tags:
 - Redis
---

Redis是一个非常流行的No-SQL数据库，在互联网网站的技术架构中应用相当广泛。这几天通过阅读《Redis in action》学习Redis，准备用博客简单记录一些有用的信息，以供未来参考。第一篇是Redis的开发环境搭建，这里使用的是书中推荐的Python开发环境，整个搭建过程比较简单。

<!-- more -->

###更新构建工具

因为Redis是用C写的，我们将使用源码编译的方式安装Redis，所以可以使用如下命令（适用于Debian Linux）更新构建工具：

```
$ sudo apt-get update
$ sudo apt-get install make gcc python-dev
```

###下载源码包并安装

从Redis官网下载最新稳定的安装包，如2.8.14并编译安装：

```
$ wget http://download.redis.io/releases/redis-2.8.14.tar.gz
$ tar xzf redis-2.8.14.tar.gz
$ cd redis-2.8.14
$ make
$ sudo make install
```

安装完成之后，启动Redis：

```
$ redis-server redis.conf
```

我使用的操作系统是Ubuntu 14.04，系统已经默认安装了Python 2.7，所以只需要安装Redis的Python客户端开发库就可以了。我们使用Python的简易包安装工具`setuptools`来帮助我们安装。

```
$ wget -q http://peak.telecommunity.com/dist/ez_setup.py
$ sudo python ez_setup.py
$ sudo python -m easy_install redis hiredis
```

注意，如果是通过代理上网的话，需要在`sudo`时带上环境，即：

```
$ sudo -E python ez_setup.py
$ sudo -E python -m easy_install redis hiredis
```

###验证安装结果

最后我们简单测试一下安装是否正常：
```
$ python
Python 2.7.6 (default, Mar 22 2014, 22:59:56)
[GCC 4.8.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import redis
>>> conn = redis.Redis()
Create a connection to Redis.
>>> conn.set('hello', 'world')
True
>>> conn.get('hello')
Get the value
'world'
```

一切OK。至此，Redis服务器和Python开发环境搭建成功。

### 参考资源
- [easy install will not connect through proxy](http://superuser.com/questions/258819/easy-install-will-not-connect-through-proxy)
