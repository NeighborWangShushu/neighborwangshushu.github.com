---
layout: post
title:  "iOS开发UI阶段——第九节 UITabBarController"
date:   2016-03-03 13:12:24
categories: jekyll update
---

创建标签视图控制器，并且指定其为window的根视图控制器

UITabBarController *tabBar = [UITabBarController alloc] init];

设置标签视图控制器需要管理的子视图控制器

tabBar.viewControllers = @[naVC, naVC2, thirdVC, fourthVC];

改变标签视图控制器的颜色   [[UITabBar appearance] setTintColor:[UIColor orangeColor]];

设定标签栏最先显示的子视图控制器(标签下标) tabBar.selectedIndex = 2;

标签视图控制器的子视图控制器都带有tabBarItem的属性

1.标签显示文本 thirdVC.tabBarItem.title = @“”;

2.设置标签角标 thirdVC.tabBarItem.badgeValue = @“”;

3.设置标签显示图片 thirdVC.tabBarItem.image = [UIImage imageNamed:@“”]; // 图片格式必须为png

也可以通过创建item来设置标签的相关属性

第一种标签创建方式：

{% highlight ruby %}
UITabBarItem *item = [[UITabBarItem alloc] initWithTitle:@“” image:image1 selectedImage:image2];//第一个参数为显示文本，第二个参数为正常显示图片，第三个为选中状态的显示图片

fourth.tabBarItem = item;//创建完标签之后指定为某一个视图控制器的标签
{% endhighlight %}

第二种标签创建方式：

```objc
UITabBarItem *item = [[UITabBarItem alloc] initWithTitle:@“” image:image tag:101];
```

第三种标签创建方式：

{% highlight ruby%}
UITabBarItem *item = [[UITabBarItem alloc] initWithTabBarSystemItem: UITabBarSystemItemBookmarks tag:101];//创建系统标签样式
{% endhighlight %}