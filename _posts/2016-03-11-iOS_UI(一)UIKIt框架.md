---
layout: post
title: "iOS_UI(一)UIKit框架"
date: 2016-02-23 2:23:32
image: '/assets/img/'
description: 'UIView'
tags:
- iOS
- UI
- Objective-C
categories:
- iOS_Objective-C
twitter_text:
---

一个视图默认其左上角就是这个视图的坐标系原点，每一个视图都有一个自己的坐标系，一个视图布局时，frame中的x，y是相对于父视图的坐标系原点的距离

1.frame,center是相对于父视图而言的，改变视图本身的frame,center会直接影响自身在其父视图上的显示位置

2.bounds是相对于自身而言的，改变bounds的值会影响自身坐标系原点的位置，进而会影响子视图在其上的显示位置

3.一个视图的bounds的默认值为（0，0，宽，高），因为bounds前面的两个值x，y代表的含义是视图本身左上角点距离其自身坐标系原点的距离。因为视图本身坐标系与左上角重合，所以是0

4.改变一个视图的bounds中的x，y值，不会造成自身位置的变化，因为父视图的bounds没有改变，自身的frame以及center没有改变，所以与父视图的关系没有任何变化，所以不会动

* 获取随机色的方法：
{% highlight ruby %}
[UIColor colorWithRed:arc4random()%256 / 255.0 green:arc4random()%256 / 255.0 blue:arc4random()%256 / 255.0 alpha:1.0]
{% endhighlight %}