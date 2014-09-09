title: Hexo写作环境从Ubuntu迁移到Windows
date: 2014-02-05 13:00:58
tags:
 - hexo
---

### 引言
之前一直在Ubuntu Linux上写博客，不是很方便。今天抽空把Windows的环境也搭一搭。我自己电脑用的是Windows 8，不过本文对于大多数版本的Windows环境都适用。

### 迁移过程
首先，移步到Hexo的[官方博客](http://zipperary.com/categories/hexo/)，找到[Windows下部署的博文](http://zipperary.com/2013/05/28/hexo-guide-2/)，先把基础环境搭好。博主写得很详细，而且通俗易懂，就不用我多废话了。如果你是刚开始用Hexo写博客，就直接用这个当向导就可以了，如果你像我一样是从Linux下迁移过来的，那么需要把Node.js和Hexo环境安装好，然后按照下面的步骤继续进行。

<!-- more -->

这个环境迁移总共分为四个步骤，如下：

1. 在Windows下安装Node.js和Hexo
2. 更改Hexo的默认主题为light并应用相应的配置（Hexo自带Landscape主题）
3. 拷贝原来的source文件，主要是博客的markdown文件
4. 连接github库，测试发博，完成迁移

第1步已经完成。下面假设原来的博客文件目录已经下载打包放在本地。

第2步，找到[light主题的主页](https://github.com/hexojs/hexo-theme-light)，clone这个主题即可。

```
$ git clone git://github.com/tommy351/hexo-theme-light.git themes/light
```

Clone完之后，修改light下的配置文件_config.yml，并把原来博客目录中layout文件夹覆盖刚刚clone的layout文件夹。

第3步，把原来source下的所有文件夹和文件都拷贝过来，其中包含_drafts, _posts和img等。

第4步，连接github的库。这一步稍微有点麻烦，首先要重新生成ssh key并添加到Github里，如Github的[SSH帮助页面](https://help.github.com/articles/generating-ssh-keys)所示。即便完成ssh连通性测试之后，也可能会出现*'github' does not appear to be a git repository*的问题，可以尝试采用下面的方法解决：

 - 重新初始化git
 - [Windows下Hexo指南](http://zipperary.com/2013/05/28/hexo-guide-2/)中的bugs说明
 - 删除deploy文件，并重新deploy

我自己的具体操作是重开Git bash窗口，然后执行如下命令：
```
$ rm -fr .deploy
$ hexo g
$ hexo d
```

OK，最后，因为github上的库已经存在，所以要先`git pull`下，然后执行命令`hexo d`才能成功。

###体验
因为平常使用Windows环境较多，Windows下的文本编辑器也比较丰富，例如Sublime Text和Lighttable等等，这样写博客的速度就会提升。但令人遗憾的是，博客生成的速度却慢了下来。以我目前不多的博客数量，在Windows下居然需要15秒以上的生成时间，而在Linux上只需要不到1秒。不过幸亏博客生成的时间只占一小部分，所以也就暂不计较了。

Enjoy Hexo on Windows!