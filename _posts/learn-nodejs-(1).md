title: Learn NodeJS (1)
date: 2013-11-28 23:11:32
tags:
 - nodejs
---

学习Node.js （一）
==========================

最近业余学习一下Node.js，记录一下学习路径。

##初学乍练

###第一步 [Node初学指南（中文版）](http://www.nodebeginner.org/index-zh-cn.html)
 跟随指南做练习，其中引用到的文章，从学习效率的角度考虑，说明如下：

 - [Understanding node.js](http://debuggable.com/posts/understanding-node-js:4bd98440-45e4-4a9a-8ef7-0f7ecbdd56cb) 必读
 - [Martin Fowler关于依赖注入的大作](http://martinfowler.com/articles/injection.html) 推荐阅读
 - [Steve Yegge的大作名词王国中的死刑](http://steve-yegge.blogspot.com/2006/03/execution-in-kingdom-of-nouns.html) 可略过不读，不过特想买一本Steve的A Programmer's Rantings，想一睹吐槽大师的风采
 - [Javascript中的对象与传统面向对象语言中对象的区别](http://msdn.microsoft.com/en-us/magazine/cc163419.aspx) 已略过不读，理解概念即可
 - [理解Node.js的事件轮询](http://blog.mixu.net/2011/02/01/understanding-the-node-js-event-loop/) 必读，作者自己有一本免费的Node小书，具体见下文
<!-- more -->

**注意**

NPM下载如果需要通过代理的话，可以使用如下命令设置通过代理访问：

```
npm config set https-proxy http://proxy.company.com:8080
npm install formidable
```

更多设置方式可参考 [http://wil.boayue.com/blog/2013/06/14/using-npm-behind-a-proxy/](http://wil.boayue.com/blog/2013/06/14/using-npm-behind-a-proxy/)。

安装formidable包的时候，选择在源代码存放位置安装，可以避免出现无法找到formidable的错误，这可能是NPM的路径设置的问题，可参见[此文](http://cnt1992.blog.163.com/blog/static/21151703220134410920410/)。

通过第一步，对NodeJS的基本概念、机制有了初步了解，能写一个Web服务器程序处理基本请求。

###第二步 寻找更多免费靠谱资源
互联网资源遍地，但是靠谱又免费的不多啊！下面使用排除法，避免你掉进相同的小水沟。:)

####推荐列表
 - [nodetuts.com](http://nodetuts.com/) 多个Node的视频讲座，12/13年的，**推荐**。
 - [HowtoNode](http://howtonode.org/) 不系统，不是针对入门级选手，应该是针对中高级Node开发者的，可作日后参考。
 - [Mixu's Node小书](http://book.mixu.net/node/) 比较用心的作者，保持更新，**推荐** 

####不推荐列表
 - [Udemy的视频课程](https://www.udemy.com/learn-nodejs-by-example/) 只有少部分课程免费，不能系统学习，不推荐。
 - [Mastering Node](http://visionmedia.github.io/masteringnode/) 貌似以前比较知名的Node开源电子书，但是2年没有更新，章节不全，不推荐。
 - [Felix's beginner's guide](http://nodeguide.com/beginner.html) 可以浏览一下，但不是教程，可作为编程参考。

####参考
 
 - Stackoverflow[关于学习Node的资源问答](http://stackoverflow.com/questions/2353818/how-do-i-get-started-with-node-js) 不服不行，Stackoverflow真是码农的好朋友，赞。这是一份资源列表，还需要进一步根据学习的需要过滤。我会在学习NodeJS后续的文章中陆续引用其中的资源并给出评价。
 - developerWorks提供的[NodeJS的学习资料汇总](http://weibo.com/1894238970/zlt5hu0ft)
 - 译言文章[NodeJS学习的最好资源](http://article.yeeyan.org/view/384870/350307)

第二步，通过靠谱的资源继续推进，进入高级入门阶段。:D

###写在后面
随着学习的展开，NodeJS以及JavaScript的资源和内容会逐步增加和更新，敬请期待下面的博文。
