title: A tip for Ubuntu 14.04 update
date: 2014-11-07 01:14:41
tags:
 - Ubuntu
---

安装了Ubuntu 14.04之后，出现一个小问题，软件自动更新时经常提示空间不足。搜一下，下面的链接提供了一些解决方案。
http://askubuntu.com/questions/2793/how-do-i-remove-or-hide-old-kernel-versions-to-clean-up-the-boot-menu

简单说想快速解决就是一条命令：
`sudo apt-get remove --purge $(dpkg -l 'linux-image-*' | sed '/^ii/!d;/'"$(uname -r | sed "s/\(.*\)-\([^0-9]\+\)/\1/")"'/d;s/^[^ ]* [^ ]* \([^ ]*\).*/\1/;/[0-9]/!d')`

这条命令会移除所有除了当前版本之外所有旧的Kernel安装包，以腾出空间。当然，如果想要彻底解决这个问题，可以参考上面的文章。
