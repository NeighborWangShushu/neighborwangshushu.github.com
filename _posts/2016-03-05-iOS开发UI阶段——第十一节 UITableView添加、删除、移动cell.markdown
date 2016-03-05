---
layout: post
title:  "iOS开发UI阶段——第十一节 UITableView添加、删除、移动cell"
date:   2016-03-05 11:22:18
categories: iOS_Object-C
---
添加删除数据

1.让将要执行删除、添加操作的表视图处于编辑状态

{% highlight ruby %}
- (void)setEditing:(BOOL)editing animated:(BOOL)animated {

//先执行父类中的这个方法

[supersetEditing:editinganimated:animated];

//表视图执行此方法

[self.tableViewsetEditing:editinganimated:animated];

}
{% endhighlight %}

2.指定表视图中哪些行可以处于编辑状态默认是所有行都可以编辑

{% highlight ruby %}
- (BOOL)tableView:(UITableView*)tableView canEditRowAtIndexPath:(NSIndexPath*)indexPath { }
{% endhighlight %}

3.指定编辑样式，到底是删除还是添加默认全部都是删除样式

{% highlight ruby %}
- (UITableViewCellEditingStyle)tableView:(UITableView*)tableView editingStyleForRowAtIndexPath:(NSIndexPath*)indexPath {

if(indexPath.row>10) {

return UITableViewCellEditingStyleDelete;

} else {

return UITableViewCellEditingStyleInsert;

}

}
{% endhighlight %}

4.当点击删除、添加按钮式，需要做什么事情，怎样才能完成删除或者添加操作，全部在这个方法内部实现，是这四步的核心

{% highlight ruby %}
- (void)tableView:(UITableView*)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath*)indexPath {

[tableView beginUpdates];//表视图开始更新

if(editingStyle == UITableViewCellEditingStyleDelete) {

//1.将该位置下的单元格删除

[tableView deleteRowsAtIndexPaths:@[indexPath]withRowAnimation:UITableViewRowAnimationFade];

//2.删除数据数组中与该单元格绑定的数据

[_dataArray  removeObjectAtIndex:indexPath.row];

} else if (editingStyle == UITableViewCellEditingStyleInsert) {

Student*student =_dataArray[indexPath.row];

//构建一个位置信息

NSIndexPath *index = [NSIndexPath indexPathForRow:0inSection:0];//添加显示在第一行

[tableView insertRowsAtIndexPaths:@[index]withRowAnimation:UITableViewRowAnimationTop];

[_dataArray insertObject:student atIndex:index.row];

}
[tableViewendUpdates];//表视图结束更新

}
{% endhighlight %}

移动数据的操作

1.让将要执行删除、添加操作的表视图处于编辑状态

{% highlight ruby %}
- (void)setEditing:(BOOL)editing animated:(BOOL)animated {

//先执行父类中的这个方法

[supersetEditing:editinganimated:animated];

//表视图执行此方法

[self.tableView setEditing:editing animated:animated];

}
{% endhighlight %}

2.指定哪些行可以移动默认是全部

{% highlight ruby %}
- (BOOL)tableView:(UITableView*)tableView canMoveRowAtIndexPath:(NSIndexPath*)indexPath { }
{% endhighlight %}

3.移动完成之后要做什么事，怎么完成移动

{% highlight ruby %}
- (void)tableView:(UITableView*)tableView moveRowAtIndexPath:(NSIndexPath*)sourceIndexPath toIndexPath:(NSIndexPath*)destinationIndexPath {
//先记录原有位置下的模型数据

Student*student =_dataArray[sourceIndexPath.row];

[student retain];//在MRC下必须retain一次 否则删除数据时记录的student对象会被销毁
//删除原位置下的模型数据

[_dataArray removeObjectAtIndex:sourceIndexPath.row];
//在新的位置将记录的模型数据添加到数据数组中

[_dataArray insertObject:student atIndex:destinationIndexPath.row];

[student release];

}
- (void)tableView:(UITableView*)tableView didSelectRowAtIndexPath:(NSIndexPath*)indexPath { }
{% endhighlight %}