---
layout: post
title:  "iOS开发UI阶段——第十节 UITableView"
date:   2016-03-04 14:07:09
categories: iOS_Object-C
---
UITableView的属性

分割线样式

tableView.separatorStyle=UITableViewCellSeparatorStyleSingleLine;

分割线颜色

tableView.separatorColor= [UIColor redColor];

指定cell的高度

tableView.rowHeight = 150;

UITableView有两个协议 UITableViewDataSource 和 UITableViewDelegate

UITableViewDataSource协议（前两个为必须实现的方法）

设置每个分区显示多少行

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section { }
设置每行显示什么内容，也就是指定每一行的cell

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath { }
设置分区个数

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView { }
设置每个分区组名

- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section { }
UITableViewDelegate协议

设置分区头的高度

- (CGFloat)tableView:(UITableView*)tableView heightForHeaderInSection:(NSInteger)section { }
设置分区头的显示的视图(与设置分组名有一定相同的效果)

- (UIView*)tableView:(UITableView*)tableView viewForHeaderInSection:(NSInteger)section { }
设置每一行的高度，也就是cell的高度

- (CGFloat)tableView:(UITableView*)tableView heightForRowAtIndexPath:(NSIndexPath*)indexPath { }
指定右侧边栏索引

- (NSArray *)sectionIndexTitlesForTableView:(UITableView*)tableView { }
//点击单元格之后触发的方法(可以完成跳转，传值等)

- (void)tableView:(UITableView*)tableView didSelectRowAtIndexPath:(NSIndexPath*)indexPath { }
