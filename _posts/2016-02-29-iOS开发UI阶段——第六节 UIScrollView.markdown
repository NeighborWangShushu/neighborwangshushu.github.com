---
layout: post
title:  "iOS开发UI阶段——第六节 UIScrollView"
date:   2016-02-29 12:23:32
categories: iOS_Objective-C
---

定义手机屏幕的宽和高为 kWidth 和 kHeight

UIScrollView包含的主要属性

①、设置滚动区域(内容区域)的大小  scrollView.contentSize = CGSizeMake(kWidth * n, kHeight * n);//n >= 1才能滑动

②、设置滚动视图的偏移量  scrollView.contentOffset = CGPointMake(0, 0);

③、是否整页翻图 scrollView.pagingEnabled = YES; 默认是NO

④、是否显示滚动显示条 scrollView.showsHorizontalScrollIndicator = NO; //横向  默认是YES

scrollView.showsVerticalScrollIndicator = NO;//纵向默认是YES

⑤、是否开启滚动视图的回弹效果 scrollView.bounces = NO;//默认是YES

⑥、定义scrollView的缩放大小比例 scrollView.maximumZoomScale = 2;//最多放大两倍

scrollView.minimumZoomScale = 0.5;//最多缩小到0.5倍

只有遵守了UIScrollViewDelegate协议才能执行UIScrollView的方法

{% highlight ruby %}
//只要是拖拽scrollView就会触发这个方法

- (void)scrollViewDidScroll:(UIScrollView*)scrollView

//开始拖拽的时候会触发这个方法

- (void)scrollViewWillBeginDragging:(UIScrollView*)scrollView

//当结束拖拽的时候会触发这个方法

- (void)scrollViewDidEndDragging:(UIScrollView*)scrollViewwillDecelerate:(BOOL)decelerate

//当滚动减速的时候会触发这个方法

- (void)scrollViewWillBeginDecelerating:(UIScrollView*)scrollView

//当滚动彻底停止的时候会触发这个方法

- (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView

//指定缩放视图

- (UIView*)viewForZoomingInScrollView:(UIScrollView*)scrollView

//正在缩放

- (void)scrollViewDidZoom:(UIScrollView*)scrollView
{% endhighlight %}


