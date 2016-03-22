---
layout: post
title: "iOS_UI(七)UINavigationController"
date: 2016-03-01 12:08:01
image: '/assets/img/'
description: 'UINavigationController'
tags:
- iOS
- UI
- Objective-C
categories:
- iOS_Objective-C
twitter_text:
---

导航视图控制器也是一个视图控制器，TA管理了多个子视图控制器，是系统提供给我们的容器视图控制器

导航视图控制器至少管理了一个子视图控制器，这个视图控制器称为根视图控制器

如果我们的程序想要采用导航视图控制器进行布局，我们需要指定window的根视图控制器为导航视图控制器

每一个加到导航视图控制器内部的视图控制器自带一个属性叫navigationItem，可以配置当前页面导航条的显示内容，比如左按钮，标题，右按钮等

设置导航栏的整体属性  一般在指定导航视图控制器的根视图时设置

1.显隐属性 naVC.navigationBarHidden = YES;

2.导航栏样式 naVC.navigationBar.barStyle = UIBarStyleDefault;

3.导航栏的背景颜色 naVC.navigationBar.backgroundColor = [UIColor whiteColor];

4.导航栏的颜色 naVC.navigationBar.barTintColor = [UIColor whiteColor];

5.导航栏元素颜色 naVC.navigationBar.tintColor = [UIColor whiteColor];

设置导航栏标题 self.navigationItem.title = @“”;

设置导航栏上的标题视图 self.navigationItem.titleView = 视图控件；

创建左右按钮（四种初始化方法）

1.显示自定义图片 initWithImage:image  style:UIBarButtonItemStylePlain target:self action:SEL

2.使用系统自带图标样式

3.使用文本显示

4.使用自定义视图显示

指定左右按钮 self.navigationItem.leftBarButtonItem = left;

是否开启导航栏的半透明度关系到自身的原点位置，系统默认为YES，其原点为屏幕左上角点

关闭时导航栏左下角的点为坐标原点

self.navigationController.navigationBar.translucent=NO;

界面跳转

1.创建想要跳转到的视图控制器

2.导航视图控制器完成推出操作  [self.navigationController pushViewController:secondVC animated:YES];

返回界面

1.返回到上一级视图控制器 [self.navigationController popViewControllerAnimated:YES];

2.返回到根视图控制器  [self.navigationController popToRootViewControllerAnimated:YES];

3.返回到指定的视图控制器 UIViewController *vc = [self.navigationController.viewControllers objectAtIndex:1];

[self.navigationController popToViewController:vc animated:YES];