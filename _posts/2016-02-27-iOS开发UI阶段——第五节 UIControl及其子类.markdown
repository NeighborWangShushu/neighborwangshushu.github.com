---
layout: post
title:  "iOS开发UI阶段——第五节 UIControl及其子类"
date:   2016-02-27 12:07:32
categories: iOS_Object-C
---

UIControl

UIControl:有控制功能的视图的父类

只要跟控制有关的类都是继承自该类，同时我们通常不会直接用这个类，而用的都是该类的子类

常用方法

{% highlight ruby %}
- (void)addTarget:(id)target action:(SEL)action forControlEvents:(UIControlEvents)controlEvents; // 添加一个事件

- (void)removeTarget:(id)target action:(SEL)action forControlEvents:(UIControlEvents)controlEvents; // 移除一个事件
{% endhighlight %}

UISwitch

在创建过程中在frame里的size是没有意义的，因为系统开关控件大小是固定的

UISwitch相关属性

{% highlight ruby %}
UISwitch *firstSwitch = [[UISwitch alloc] initWithFrame:CGRectMake(100,100,0,0)]; // 创建UISwitch

firstSwitch.onTintColor= [UIColor redColor];// 设置开关开启状态的颜色

firstSwitch.tintColor= [UIColor blackColor];// 设置开关风格颜色

firstSwitch.thumbTintColor= [UIColor blueColor];// 设置开关按钮颜色

[firstSwitch setOn:YES animated:YES];// 手动设置开关状态 

// firstSwitch.on 获取开关当前状态

[self.view addSubview:firstSwitch]; // 将UISwitch放入视图中
{% endhighlight %}


UISlider

滑块通常用于控制视频或者音频的播放的进度，控制音量等操作

UISlider相关属性

{% highlight ruby %}
UISlider *slider = [[UISlider alloc] initWithFrame:CGRectMake(100,200,100,40)]; // 创建UISlider

slider.minimumValue=0.0;// 设置滑块的最小值

slider.maximumValue=100.0;// 设置滑块的最大值

slider.value=50;// 设置滑块的值

slider.minimumTrackTintColor= [UIColorblackColor];// 设置滑块划过区域的颜色

[slider addTarget:selfaction:@selector(slider:) forControlEvents:UIControlEventValueChanged];// 滑块添加事件，触发方式为值的改变
{% endhighlight %}


UISegmentedControl

分段控件常用在不同类别的信息之间选择，或者切换不同的视图

UISegmentedControl相关属性

{% highlight ruby %}
UISegmentedControl *segmentedControl = [[UISegmentedControl alloc] initWithItems:@[@"你",@"我"]];segmentedControl.frame = CGRectMake(100,300,100,40); // 创建UISegmentedControl

// selectedSegmentIndex 指定被选中的分段

// segmentedControlStyle 设置样式

segmentedControl.momentary=YES;// 设置在点击后是否恢复原样

// [segmentedControl setTitle:nil forSegmentAtIndex:0]; 为指定下标的分段这是title

// [segmentedControl setImage: forSegmentAtIndex:]; 为指定小标的分段这只图片[segmentedControl setEnabled:NO forSegmentAtIndex:1]; // 设置指定索引是否可点

segmentedControl.tintColor= [UIColor grayColor];// 样式颜色

[segmentedControl addTarget:selfaction:@selector(segmentedControl:) forControlEvents:UIControlEventValueChanged];
{% endhighlight %}


UIPageControl

UIPageControl相关属性

{% highlight ruby %}
UIPageControl *pageControl = [[UIPageControl alloc] initWithFrame:CGRectMake(100,400,100,40)]; // 创建UIPageControl

pageControl.backgroundColor= [UIColorgrayColor];

pageControl.numberOfPages=3;// 指定页数

pageControl.currentPage=1;// 设置当前页数，第一页为0

pageControl.currentPageIndicatorTintColor= [UIColor redColor];// 设置当前选中页数的颜色

pageControl.pageIndicatorTintColor= [UIColor whiteColor];// 没有选中页数的颜色
{% endhighlight %}


{% highlight ruby %}

@implementationViewController

- (void)sliderAction:(UISlider*)slider {

NSLog(@"%.2f", slider.value);

}

- (void)segmentedAction:(UISegmentedControl*)segment {

switch(segment.selectedSegmentIndex) {

case0:

NSLog(@"第一");

self.view.backgroundColor= [UIColorgreenColor];

break;

case1:

NSLog(@"第二");

self.view.backgroundColor= [UIColororangeColor];

break;

case2:

NSLog(@"第三");

self.view.backgroundColor= [UIColorlightGrayColor];

break;

default:

break;

}

}

- (void)pageControlAction:(UIPageControl*)pageControl {

NSLog(@"翻页");

}

- (void)viewDidLoad {

[superviewDidLoad];

//开关

UISwitch*newSwitch = [[UISwitchalloc]initWithFrame:CGRectMake(200,80,0,0)];//开关大小只能是系统默认值

[self.viewaddSubview:newSwitch];

//设置开关开启状态的颜色

newSwitch.onTintColor= [UIColorblueColor];

//设置开关风格颜色

newSwitch.tintColor= [UIColororangeColor];

//设置开关按钮颜色

newSwitch.thumbTintColor= [UIColorblackColor];

//设置开关是否开启

//    newSwitch.on = NO;

//手动设置开关状态

[newSwitchsetOn:YESanimated:NO];

//滑块

UISlider*slider = [[UISlideralloc]initWithFrame:CGRectMake(20,150,350,40)];

[self.viewaddSubview:slider];

//设置slider的最大、最小值

slider.maximumValue=5.0;

slider.minimumValue=0.0;

//设置划过区域的颜色

slider.minimumTrackTintColor= [UIColorredColor];

//设置未划过区域的颜色

slider.maximumTrackTintColor= [UIColorgreenColor];

//设置滑块的颜色

slider.thumbTintColor= [UIColorblueColor];

//添加点击事件

[slideraddTarget:selfaction:@selector(sliderAction:)forControlEvents:UIControlEventValueChanged];

//在滑块终点加载图片

//    [slider setMaximumTrackImage:image forState:UIControlStateNormal];

//分段控件

UISegmentedControl*segment = [[UISegmentedControlalloc]initWithItems:@[@"第一",@"第二",@"第三"]];

segment.frame=CGRectMake(90,300,250,40);

[self.viewaddSubview:segment];

//指定segment的颜色

segment.tintColor= [UIColorpurpleColor];

//添加事件

[segmentaddTarget:selfaction:@selector(segmentedAction:)forControlEvents:UIControlEventValueChanged];

//UIPageControl

UIPageControl*pageControl = [[UIPageControlalloc]initWithFrame:CGRectMake(90,600,200,40)];

//设置页数

pageControl.numberOfPages=5;

//设置当前页默认是0(第一页)

pageControl.currentPage=1;

pageControl.backgroundColor= [UIColorbrownColor];

//设置圆点的颜色

pageControl.currentPageIndicatorTintColor= [UIColorredColor];

pageControl.pageIndicatorTintColor= [UIColorwhiteColor];

[self.viewaddSubview:pageControl];

//添加事件

[pageControladdTarget:selfaction:@selector(pageControlAction:)forControlEvents:UIControlEventValueChanged];

}

@end
{% endhighlight %}

