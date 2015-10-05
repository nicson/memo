# Xamarinまとめ

## UITableView

* __NSIndexPathの作り方__

  * セクション、アイテムを指定し、取得
```csharp
 //1セクション目の 1アイテム目のインデックスパス
 var indexPath = NSIndexPath.FromItemSection(0,0);
```

  * セルから取得
```csharp
//ボタンの親viewの親viewであるUITableViewCellインスタンスからインデックスパスを取得
var indexPath = TableView.IndexPathForCell((UITableViewCell)button.Superview.Superview);
```
