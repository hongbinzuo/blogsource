title: 安装Ubuntu 13.10虚拟机
date: 2014-03-18 21:29:02
tags:
 - Misc
---

倒腾Windows开发环境还是挺费劲的，尤其是经常使用开源软件的话。安装Cygwin神马的都烦了，还不如直接装个虚拟机。小伙伴前段时间装了一个，嘿嘿，这下方便了，按图索骥少费工夫，开装。

参考：[http://youfei.github.io/2014/02/27/others-1/](http://youfei.github.io/2014/02/27/others-1/)

<!-- more -->

1. 下载VMWare Player：[link1](https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/6_0)
2. 下载Ubuntu镜像：[link2](http://www.ubuntu.com/download/zh-CN)，我下载的是13.10桌面版
3. 设置启动安装不废话
4. 启动之后提示错误，查了一下是我的HP笔记本默认关闭了虚拟机启动，进入BIOS，找到相关选项Enable即可，参考链接: [link3](http://h30434.www3.hp.com/t5/Other-Desktop-PC-Questions/Need-to-get-into-BIOS-setup-to-change-VT-setting/td-p/1278503)
5. 重新启动之后不能显示桌面，可能是在安装中出现了错误，使用下面的命令可以修复（参考链接：[link4](http://blog.sina.com.cn/s/blog_9ffceca50101g0st.html)）
6. 最后一个问题，Ubuntu桌面不能全屏幕显示，需要安装VMWare Tools，参考：[link5](http://blog.csdn.net/woshicaixianfeng/article/details/6157407)。安装的过程可能不一定很顺利，要有耐心。

```
---- 5. 安装Ubuntu界面的命令 ----
$ sudo apt-get install ubuntu-desktop
$ reboot
$ startx
```

大功告成！玩儿去！