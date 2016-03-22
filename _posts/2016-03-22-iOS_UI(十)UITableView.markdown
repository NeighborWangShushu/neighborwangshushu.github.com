---
layout: post
title: "iOS_UI(十)UITableView"
date: 2016-03-04 14:07:09
image: '/assets/img/'
description: 'UITableViewCell'
tags:
- iOS
- UI
- Objective-C
categories:
- iOS_Objective-C
twitter_text:
---
UITableView的属性

分割线样式

**tableView.separatorStyle=UITableViewCellSeparatorStyleSingleLine;**

分割线颜色

tableView.separatorColor= [UIColor redColor];

指定cell的高度

tableView.rowHeight = 150;

UITableView有两个协议 UITableViewDataSource 和 UITableViewDelegate

UITableViewDataSource协议（前两个为必须实现的方法）

设置每个分区显示多少行
{% highlight ruby %}
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section { }
{% endhighlight %}

设置每行显示什么内容，也就是指定每一行的cell

{% highlight ruby %}
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath { }
{% endhighlight %}

设置分区个数

{% highlight ruby %}
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView { }
{% endhighlight %}

设置每个分区组名

{% highlight ruby %}
- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section { }
{% endhighlight %}

UITableViewDelegate协议

设置分区头的高度

{% highlight ruby %}
- (CGFloat)tableView:(UITableView*)tableView heightForHeaderInSection:(NSInteger)section { }
{% endhighlight %}

设置分区头的显示的视图(与设置分组名有一定相同的效果)

{% highlight ruby %}
- (UIView*)tableView:(UITableView*)tableView viewForHeaderInSection:(NSInteger)section { }
{% endhighlight %}

设置每一行的高度，也就是cell的高度

{% highlight ruby %}
- (CGFloat)tableView:(UITableView*)tableView heightForRowAtIndexPath:(NSIndexPath*)indexPath { }
{% endhighlight %}

指定右侧边栏索引
{% highlight ruby %}
- (NSArray *)sectionIndexTitlesForTableView:(UITableView*)tableView { }
//点击单元格之后触发的方法(可以完成跳转，传值等)
- (void)tableView:(UITableView*)tableView didSelectRowAtIndexPath:(NSIndexPath*)indexPath { }
{% endhighlight %}