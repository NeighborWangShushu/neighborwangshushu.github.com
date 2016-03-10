---
layout: post
title:  "iOS开发UI阶段——第十五节 UICollectionView"
date:   2016-03-10 14:00:13
categories: iOS_Objective-C
---

集合视图的创建必须指定布局，如果没有布局，则显示不了任何东西，所以在创建集合视图对象之前必须先创建一个布局对象

采用系统布局类UICollectViewLayout(布局基类)

```objc
UICollectionViewFlowLayout*layout = [[UICollectionViewFlowLayout alloc]init];
```

设置布局对象的相关属性

设置最小的行间距(默认是10)layout.minimumLineSpacing = 20;

设置item与item之间的间距layout.minimumInteritemSpacing = 10;

设置每个item的尺寸大小layout.itemSize = CGSizeMake((kWidth - 45) / 3, 100);

设置集合视图的分区间隔(上，左，下，右)layout.sectionInset = UIEdgeInsetsMake(10, 10, 10, 10);

设置集合视图的滑动方向layout.scrollDirection=UICollectionViewScrollDirectionVertical;//竖向滚动

创建集合视图
```objc
UICollectionView *collectionView = [[UICollectionView alloc]initWithFrame:[UIScreen mainScreen].bounds collectionViewLayout:layout];
```

集合视图想要显示内容，必须将cell进行注册
```objc
[collectionView registerClass:[UICollectionViewCell class] forCellWithReuseIdentifier:string];
```
集合视图包含以下代理

UICollectionViewDataSource 数据源协议

UICollectionViewDelegate 代理协议  （其中的方法与UITableView的代理协议相似）

布局包含的代理

UICollectionViewDelegateFlowLayout

UICollectionViewDataSource协议包含的方法（前两个必须实现）

//设置每个分区包含的item个数
```objc
- (NSInteger)collectionView:(UICollectionView*)collectionView numberOfItemsInSection:(NSInteger)section;
```
//设置每个需要显示的cell
```objc
- (UICollectionViewCell*)collectionView:(UICollectionView*)collectionView cellForItemAtIndexPath:(NSIndexPath*)indexPath;
```
//设置包含的分区个数
```objc
- (NSInteger)numberOfSectionsInCollectionView:(UICollectionView*)collectionView;
```
//设置增广视图，即每个分区的头视图或者尾视图
```objc
- (UICollectionReusableView*)collectionView:(UICollectionView*)collectionView viewForSupplementaryElementOfKind:(NSString*)kind atIndexPath:(NSIndexPath*)indexPath;
```
UICollectionViewDelegateFlowLayout协议包含的方法

//返回每个item的尺寸大小
```objc
- (CGSize)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath*)indexPath;
```
//返回视图与屏幕边缘的距离
```objc
- (UIEdgeInsets)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout insetForSectionAtIndex:(NSInteger)section;
```
//返回最小的行间距
```objc
- (CGFloat)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout minimumLineSpacingForSectionAtIndex:(NSInteger)section;
```
//返回item与item之间的距离
```objc
- (CGFloat)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout minimumInteritemSpacingForSectionAtIndex:(NSInteger)section;
```
//返回分区头视图的尺寸大小
```objc
- (CGSize)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout referenceSizeForHeaderInSection:(NSInteger)section;
```
//返回分区尾视图的尺寸大小
```objc
- (CGSize)collectionView:(UICollectionView*)collectionView layout:(UICollectionViewLayout*)collectionViewLayout referenceSizeForFooterInSection:(NSInteger)section;
```