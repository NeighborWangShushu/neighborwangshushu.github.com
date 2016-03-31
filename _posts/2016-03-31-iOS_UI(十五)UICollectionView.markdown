---
layout: post
title: "iOS_UI(十五)UICollectionView"
date: 2016-03-10 14:00:13
image: '/assets/img/'
description: '集合视图'
tags:
- iOS
- UI
- Objective-C
categories:
- iOS_Objective-C
twitter_text:
---


集合视图的创建必须指定布局，如果没有布局，则显示不了任何东西，所以在创建集合视图对象之前必须先创建一个布局对象

采用系统布局类UICollectViewLayout(布局基类)

{% highlight ruby %}
UICollectionViewFlowLayout*layout = [[UICollectionViewFlowLayout alloc]init];
{% endhighlight %}

设置布局对象的相关属性

设置最小的行间距(默认是10)layout.minimumLineSpacing = 20;

设置item与item之间的间距layout.minimumInteritemSpacing = 10;

设置每个item的尺寸大小layout.itemSize = CGSizeMake((kWidth - 45) / 3, 100);

设置集合视图的分区间隔(上，左，下，右)layout.sectionInset = UIEdgeInsetsMake(10, 10, 10, 10);

设置集合视图的滑动方向layout.scrollDirection=UICollectionViewScrollDirectionVertical;//竖向滚动

创建集合视图

{% highlight ruby %}
UICollectionView *collectionView = [[UICollectionView alloc]initWithFrame:[UIScreen mainScreen].bounds collectionViewLayout:layout];
{% endhighlight %}

集合视图想要显示内容，必须将cell进行注册

{% highlight ruby %}
[collectionView registerClass:[UICollectionViewCell class] forCellWithReuseIdentifier:string];
{% endhighlight %}

集合视图包含以下代理

UICollectionViewDataSource 数据源协议

UICollectionViewDelegate 代理协议  （其中的方法与UITableView的代理协议相似）

布局包含的代理

UICollectionViewDelegateFlowLayout

UICollectionViewDataSource协议包含的方法（前两个必须实现）

//设置每个分区包含的item个数

{% highlight ruby %}
- (NSInteger)collectionView:(UICollectionView*)collectionView numberOfItemsInSection:(NSInteger)section;
{% endhighlight %}

//设置每个需要显示的cell

{% highlight ruby %}
- (UICollectionViewCell*)collectionView:(UICollectionView*)collectionView cellForItemAtIndexPath:(NSIndexPath*)indexPath;
{% endhighlight %}

//设置包含的分区个数

{% highlight ruby %}
- (NSInteger)numberOfSectionsInCollectionView:(UICollectionView*)collectionView;
{% endhighlight %}

//设置增广视图，即每个分区的头视图或者尾视图

{% highlight ruby %}
- (UICollectionReusableView*)collectionView:(UICollectionView*)collectionView viewForSupplementaryElementOfKind:(NSString*)kind atIndexPath:(NSIndexPath*)indexPath;
{% endhighlight %}

UICollectionViewDelegateFlowLayout协议包含的方法

//返回每个item的尺寸大小

{% highlight ruby %}
- (CGSize)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath*)indexPath;
{% endhighlight %}

//返回视图与屏幕边缘的距离

{% highlight ruby %}
- (UIEdgeInsets)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout insetForSectionAtIndex:(NSInteger)section;
{% endhighlight %}

//返回最小的行间距

{% highlight ruby %}
- (CGFloat)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout minimumLineSpacingForSectionAtIndex:(NSInteger)section;
{% endhighlight %}

//返回item与item之间的距离

{% highlight ruby %}
- (CGFloat)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout minimumInteritemSpacingForSectionAtIndex:(NSInteger)section;
{% endhighlight %}

//返回分区头视图的尺寸大小

{% highlight ruby %}
- (CGSize)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout referenceSizeForHeaderInSection:(NSInteger)section;
{% endhighlight %}

//返回分区尾视图的尺寸大小

{% highlight ruby %}
- (CGSize)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout referenceSizeForFooterInSection:(NSInteger)section;
{% endhighlight %}
