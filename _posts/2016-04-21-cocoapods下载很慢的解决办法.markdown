---
layout: post
title: "cocoapods下载很慢的解决办法"
date: 2016-04-21 22:06:48 + 8:00
image: '/assets/img/'
description: 'Git'
tags:
- GitHub
- Git
categories:
- Git
twitter_text:
---

我们喜欢用cocoapods下载第三方的类库到我们的项目中,但是我们会遇到下载这些第三方时总是要等待很长的时间,,我在网上找到了解决这个问题的办法

***

	$ pod install
    
执行这行命令的时候下载的速度很慢,这是因为cocoapods的install和update的默认源是国外的源,所以速度很慢
我这里指的源跟之前在安装的时候更换的taobao的镜像不是一个概念,taobao的这个镜像是用在下载cocoapods时用到的,这个镜像在安装完cocoapods之后,两者就没有关系了
所以想要提高install和update的速度我这里提供了两个方法

### 方法一. 更换源

在终端中输入下面的命令更换源

    $ pod repo remove master
    $ pod repo add master https://gitcafe.com/akuandev/Specs.git
    $ pod repo update

如果想用别的镜像的话也可以将第二条命令的镜像换成 ``http://git.oschina.net/akuandev/Specs.git``

* 需要注意的是执行第二条命令的时候会很慢因为里面的东西有160M,所以慢慢等吧*


在将镜像更换之后还没有结束,在每一个项目中创建的podfile文件的第一行都要填写下面这行source命令

    source 'http://git.oschina.net/akuandev/Specs.git'

### 方法二.忽略升级specs库

在进行``pod install``和``pod update``时候忽略升级specs库

    $ pod install --verbose --no-repo-update
    $ pod update --verbose --no-repo-update


如果想跟深的了解详情请看这篇[博客](http://akinliu.github.io/2014/05/03/cocoapods-specs-/)
