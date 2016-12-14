# cell 高度自适应
  
参考文章：[Raywenderich](https://www.raywenderlich.com/129059/self-sizing-table-view-cells)  
  
*	 通过约束布局 cell 的子视图，四条边都需要建立约束；
*	 `tableview`要设置属性`rowHeight`, `estimateRowHeight`

```
	self.tableView.rowHeight = UITableViewAutomaticDimension;
    self.tableView.estimatedRowHeight = 380;
```
So Easy!!