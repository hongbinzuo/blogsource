title: The first blog with Hexo
date: 2013-11-08 23:13:36
tags: 
 - hexo 
 - github 
 - blog
---


在Ubuntu 13.10 Linux环境下使用Hexo搭建Github博客系统
----------------------------------

**Github的Git环境搭建**

 - 安装git：sudo apt-get install git 
 - 生成SSH Key并验证连通性 https://help.github.com/articles/generating-ssh-keys

**Github Pages博客搭建**
  
 - 主要参考下文中使用GitHub Pages建立博客的部分：http://beiyuu.com/github-pages/
 - 需要注意的是Github的博客页面不一定能及时反映更新，有时需要等10分钟左右

**安装Hexo**

 - 安装nodejs: sudo apt-get install nodejs
	- 在不同的Linux环境或Ubuntu更早的版本安装nodejs，请参考：http://stackoverflow.com/questions/16302436/install-nodejs-on-ubuntu-12-10
 - 安装npm: sudo apt-get install npm
 - 安装Hexo的方法主要参考Hexo的官方主页 http://zespia.tw/hexo
 - 如果npm需要代理访问，直接修改Linux环境的代理http(s)_proxy或者设置npm的代理都不能奏效，最后求助于Github的问题列表，指到SO的一则回答，依法照搬，OK！（注意加sudo）http://stackoverflow.com/questions/7559648/is-there-a-way-to-make-npm-install-the-command-to-work-behind-proxy
 - 运行命令hexo init之后出错的解决方法：将hexo(/usr/local/bin/hexo)中的node改为nodejs即可

    ```
    $ hexo init         
    /usr/bin/env: node: No such file or directory    
    ```
    
  这个问题已经提交到hexo的Github主页：https://github.com/tommy351/hexo/issues/355
  [Update] Zippera回答了这个问题，建议是使用npm安装nodejs，而不是先安装nodejs 

<!--more-->

**配置Hexo**

  基础环境搭好之后就比较容易了，根据Hexo官方网站的指南即可进行配置部署，开始写博客了。

**Markdown编辑器**
    
  对于一个懒人来说，自己敲Markdown代码太累了，所以可想而知我会找一个编辑器，试用了下Stackedit还不错，所见即所得，简洁高效，小推荐一下。因为在用IDEA，IDEA也有markdown的插件用，很不错。对于Markdown语法么，到现在为止换行这个事都让人纠结。比如在Code里换行是Markdown的问题还是Hexo的问题，还需要继续探索。Markdown肯定有更好的替代方案，希望下一个版本做到完美的简洁优雅高效。参考这一篇吧，逆向思维一下：http://blog.chloerei.com/articles/4-why-I-dont-choose-markdown
 
**中文问题**
 
 - 在Linux环境下需要安装中文语言包，如果没安装的话，中文文本无法正常显示，使用UTF-8编码即可，注意putty可能不能正常显示中文，参考解决办法 http://bojack.pixnet.net/blog/post/30126860-%E3%80%90linux%E3%80%91ssh-%E9%80%A3%E7%B7%9A%E9%80%B2-ubuntu-%E4%B8%AD%E6%96%87%E4%B8%8D%E5%86%8D%E9%A1%AF%E7%A4%BA%E4%BA%82%E7%A2%BC 
 - 中英文混写的博客，不能完美地转换格式，不能确定是Markdown还是Hexo的问题

**评论分享**

 - Hexo默认使用的Disqus，只能分享到墙外
 - 试验了多说，符合中国国情

**Hexo让人小惊喜的地方**

  1. 首先是hexo server的本地预览功能
  2. hexo server可以在不重启的情况下自动装载更新，很方便
  3. 配置相对容易，Google，Stackoverflow和Github是程序员的三件利器, lol
  4. Github作者对于问题的反馈较快，而且可以用中文交流很亲切

**参考并感谢**

 - http://zespia.tw/hexo
 - http://zipperary.com/
 - http://zipperary.com/2013/05/30/hexo-guide-4/
 - http://yangjian.me/workspace/building-blog-with-hexo/
 - http://eva0919.github.io/2013/04/21/%E4%BD%BF%E7%94%A8hexo%E4%BB%A5%E5%8F%8Agithub-page%E5%BB%BA%E7%AB%8B%E8%87%AA%E5%B7%B1%E7%9A%84%E9%83%A8%E8%90%BD%E6%A0%BC/
 - http://tsgzj.me/2013/03/06/customize-hexo/
 - http://hhlux.gitcafe.com/2013/01/20/hexo%E4%B8%8A%E6%89%8B/

**写在最后**

  需要继续探索更多定制化内容，更多的使用技巧。总体体验不错，如果你是个程序员或者有一点Hacker兴趣的朋友，Github加上Hexo 算是一个比较有趣的写博客的方式。

> Written with [StackEdit](https://stackedit.io/).
