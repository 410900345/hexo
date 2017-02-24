---
title: tableviewcell左对齐
categories: 'ios'
date: 2016-11-24 10:47:54
tags:
---

1.解决tableview separatorInset cell分割线左对齐

```
- (void)tableView:(UITableView *)tableView willDisplayCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath {
    // Remove seperator inset
    if ([cell respondsToSelector:@selector(setSeparatorInset:)]) {
        [cell setSeparatorInset:UIEdgeInsetsZero];
    }
    // Prevent the cell from inheriting the Table View's margin settings
    if ([cell respondsToSelector:@selector(setPreservesSuperviewLayoutMargins:)]) {
        [cell setPreservesSuperviewLayoutMargins:NO];
    }
    // Explictly set your cell's layout margins
    if ([cell respondsToSelector:@selector(setLayoutMargins:)]) {
        [cell setLayoutMargins:UIEdgeInsetsZero];
    }
}
```
`解释说明:`
iOS7，想要设置cell的分割线显示到最左端，只需要设置separatorInset的值为UIEdgeInsetsZero。

iOS8，简单设置separatorInset的值为UIEdgeInsetsZero的方法已经无效了。UIView的layoutMargins 默认为{8, 8, 8, 8}。

cell的preservesSuperviewLayoutMargins默认为true时，可能会导致cell被其父UITableView的LayoutMargin影响。如果设置为false时，cell不被UITableView的LayoutMargin影响。

2.全局设置方法(iOS7 8 9 通用)

```
[[UITableView appearance] setSeparatorStyle:UITableViewCellSeparatorStyleSingleLine];

[[UITableView appearance] setSeparatorInset:UIEdgeInsetsZero];

[[UITableViewCell appearance] setSeparatorInset:UIEdgeInsetsZero];

if ([UITableView instancesRespondToSelector:@selector(setLayoutMargins:)]) {

[[UITableView appearance] setLayoutMargins:UIEdgeInsetsZero];

[[UITableViewCell appearance] setLayoutMargins:UIEdgeInsetsZero];

[[UITableViewCell appearance] setPreservesSuperviewLayoutMargins:NO];

}
```
参考链接:

1.[stackoverflow](http://stackoverflow.com/questions/25770119/ios-8-uitableview-separator-inset-0-not-working?page=1&tab=active#tab-top)

2.[http://www.cnblogs.com/Zev_Fung/p/5650922.html](http://www.cnblogs.com/Zev_Fung/p/5650922.html)
