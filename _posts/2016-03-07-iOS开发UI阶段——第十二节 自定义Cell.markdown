---
layout: post
title:  "iOS开发UI阶段——第十二节 自定义Cell"
date:   2016-03-07 10:53:50
categories: iOS_Object-C
---
自定义cell的步骤

1.将cell所有要显示的子视图声明为属性(不能和cell自带子视图重名)

2.重写cell的初始化方法,将子视图添加到self.contentView中，frame指定为0

3.重写layoutSubviews方法，给定内部控件的具体位置

4.导入模型头文件，在cell内部声明一个绑定模型属性

5.重写模型的setter方法，给cell内部控件进行赋值

6.内存管理