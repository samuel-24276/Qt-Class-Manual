# QStringListModel

继承关系：`QStringListModel`->`QAbstractListModel`->`QAbstractItemModel`->`QObject`

继承者： `QHelpIndexModel`

## 1.Public Functions

- QStringListModel ( QObject * parent = 0 )
- QStringListModel ( const QStringList & strings, QObject * parent = 0 )
- void	setStringList ( const QStringList & strings )
- QStringList	stringList () const

## 2.Reimplemented Public Functions

- virtual QVariant	data ( const QModelIndex & index, int role ) const
- virtual Qt::ItemFlags	flags ( const QModelIndex & index ) const
- virtual bool	insertRows ( int row, int count, const QModelIndex & parent = QModelIndex() )
- virtual bool	removeRows ( int row, int count, const QModelIndex & parent = QModelIndex() )
- virtual int	rowCount ( const QModelIndex & parent = QModelIndex() ) const
- virtual bool	setData ( const QModelIndex & index, const QVariant & value, int role = Qt::EditRole )
- virtual void	sort ( int column, Qt::SortOrder order = Qt::AscendingOrder )
- virtual Qt::DropActions	supportedDropActions () const

## 3.Detailed Description

QStringListModel类提供了一个**向视图提供字符串的模型**。

QStringListModel是一个可编辑的模型，可以用于需要在一个视图小部件中显示一些字符串的简单情况，比如QListView或QComboBox。

该模型提供了可编辑模型的所有标准功能，将字符串列表中的数据表示为一个模型，其中一列和行数等于列表中的项数。

**通过index()函数获得项目对应的模型索引，通过flags()获得项目标志。使用data()函数读取项数据，使用setData()函数写入项数据。可以通过rowCount()函数找到行数(和字符串列表中的项数)。**

可以使用现有的字符串列表构建模型，也可以稍后使用setStringList()方便函数设置字符串。也可以使用insertRows()函数以通常的方式插入字符串，并使用removeRows()删除字符串。字符串列表的内容可以用stringList()方便函数检索。

QStringListModel的用法示例:

```c++
 QStringListModel *model = new QStringListModel();
 QStringList list;
 list << "a" << "b" << "c";
 model->setStringList(list);
```

