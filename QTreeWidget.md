# QTreeWidget

继承关系：`QTreeWidget`->`QTreeView`->`QAbstractItemView`->`QAbstractScrollArea`->`QFrame`->`QWidget`

给顶层节点添加多个子节点：

```c++
//DGps节点
QTreeWidgetItem* DGpsNode = new QTreeWidgetItem;
DGpsNode->setText(0, "DGps");

QTreeWidgetItem* DGpsItem1 = new QTreeWidgetItem(DGpsNode);
DGpsItem1->setText(0, "DGps1");
QTreeWidgetItem* DGpsItem2 = new QTreeWidgetItem(DGpsNode);
DGpsItem2->setText(0, "DGps2");
```



# 1.Properties

- `columnCount : int`

  此属性保存在树小部件中显示的列数
  默认情况下，此属性的值为1。

- `topLevelItemCount : const int`

  此属性保存顶级项目的数量
  默认情况下，此属性的值为0。

# 2.Public Functions

- `QTreeWidget(QWidget *parent = nullptr)`

- `virtual ~QTreeWidget()`

- `void addTopLevelItem(QTreeWidgetItem *item)`

  将节点追加为树控件中的顶级节点。

- `void addTopLevelItems(const QList<QTreeWidgetItem *> &items)`

  将节点列表中的所有节点追加为树控件中的顶级节点。

- `int indexOfTopLevelItem(QTreeWidgetItem *item) const`

  返回给定顶级项目的索引；如果找不到该项目，则返回-1。

- `void insertTopLevelItem(int index, QTreeWidgetItem *item)`

  在视图最顶层的索引处插入项目。
  如果该项目已经插入其他位置，则不会插入。

- `void insertTopLevelItems(int index, const QList<QTreeWidgetItem *> &items)`

  在视图最顶层的索引处插入项目。
  如果该项目已经插入其他位置，则不会插入。

- `QTreeWidgetItem *takeTopLevelItem(int index)`

  删除树中给定索引处的顶级项并返回它，否则返回nullptr。

- `QTreeWidgetItem *topLevelItem(int index) const`

  返回给定索引处的顶级项目，如果该项目不存在，则返回nullptr。

- `int topLevelItemCount() const`

  此属性保存顶级项目的数量，默认值为0。

- `void closePersistentEditor(QTreeWidgetItem *item, int column = 0)`

  关闭给定列中项目的持久性编辑器。
  如果没有为此项目和列的组合打开任何持久性编辑器，则此功能无效。

- `int columnCount() const`

  此属性保存在树控件中显示的列数，默认值为1.

- `void setColumnCount(int columns)`

  此属性保存在树小部件中显示的列数，默认值为1。

- `int currentColumn() const`

  返回树控件中当前列的列数。

- `QTreeWidgetItem *currentItem() const`

  返回树控件中的当前项。

- `void editItem(QTreeWidgetItem *item, int column = 0)`

  如果可编辑，则开始编辑给定列中的项目。

- `QList<QTreeWidgetItem *> findItems(const QString &text, Qt::MatchFlags flags, int column = 0) const`

  在给定列中使用给定标志返回与给定文本匹配的项目列表。

- `QTreeWidgetItem *headerItem() const`

  返回用于树控件标题的项目。

- `QTreeWidgetItem *invisibleRootItem() const`

  返回树控件的不可见根项。
  不可见的根项通过QTreeWidgetItem API提供对树控件的顶级项的访问，从而使得可以编写可以统一方式处理顶级项及其子级的函数； 例如，递归函数。

- `bool isPersistentEditorOpen(QTreeWidgetItem *item, int column = 0) const`

  返回是否为column列中的item打开了持久性编辑器。

- `QTreeWidgetItem *itemAbove(const QTreeWidgetItem *item) const`

  返回给定项目上方的项目。

- `QTreeWidgetItem *itemAt(const QPoint &p) const`

  返回在坐标p处指向该项目的指针。 坐标是相对于树控件的`viewport（）`的。

- `QTreeWidgetItem *itemAt(int x, int y) const`

  这是一个重载函数。
  返回指向该项目在坐标（x，y）处的指针。 坐标是相对于树控件的`viewport（）`的。

- `QTreeWidgetItem *itemBelow(const QTreeWidgetItem *item) const`

  返回给定项目下方的项目。

- `QWidget *itemWidget(QTreeWidgetItem *item, int column) const`

  返回显示在由item和给定列指定的单元格中的窗口小部件。

- `void openPersistentEditor(QTreeWidgetItem *item, int column = 0)`

  在给定列中为该项目打开一个持久性编辑器。

- `void removeItemWidget(QTreeWidgetItem *item, int column)`

  删除给定列中给定项目中设置的小部件。

- `QList<QTreeWidgetItem *> selectedItems() const`

  返回所有**选定非隐藏项目**的列表。

- `void setCurrentItem(QTreeWidgetItem *item)`

- `void setCurrentItem(QTreeWidgetItem *item, int column)`

- `void setCurrentItem(QTreeWidgetItem *item, int column, QItemSelectionModel::SelectionFlags command)`

- `void setHeaderItem(QTreeWidgetItem *item)`

  设置树控件的标题项。 标题中每列的标签由项目中的相应标签提供。
  树小部件将获得该项目的所有权。

- `void setHeaderLabel(const QString &label)`

  在标签列表中每个项目的标题中添加一列，并为每一列设置标签。
  请注意，`setHeaderLabels（）`不会删除现有列。

- `void setHeaderLabels(const QStringList &labels)`

  在标签列表中每个项目的标题中添加一列，并为每一列设置标签。
  请注意，`setHeaderLabels（）`不会删除现有列。

- `void setItemWidget(QTreeWidgetItem *item, int column, QWidget *widget)`

- `int sortColumn() const`

  返回用于对窗口小部件的内容进行排序的列。

- `void sortItems(int column, Qt::SortOrder order)`

  按给定列中的值以指定顺序对小部件中的项目进行排序。

- `QRect visualItemRect(const QTreeWidgetItem *item) const`

  返回item处该项目所占据的视口上的矩形。

 

# QTreeWidgetItem

# 1.Public Types

- enum ChildIndicatorPolicy { ShowIndicator, DontShowIndicator, DontShowIndicatorWhenChildless }
- enum ItemType { Type, UserType }

# 2.Public Functions

- `QTreeWidgetItem(const QTreeWidgetItem &other)`

- `QTreeWidgetItem(QTreeWidgetItem *parent, QTreeWidgetItem *preceding, int type = Type)`

- `QTreeWidgetItem(QTreeWidgetItem *parent, const QStringList &strings, int type = Type)`

- `QTreeWidgetItem(QTreeWidgetItem *parent, int type = Type)`

- `QTreeWidgetItem(QTreeWidget *parent, QTreeWidgetItem *preceding, int type = Type)`

- `QTreeWidgetItem(QTreeWidget *parent, const QStringList &strings, int type = Type)`

  parent为当前节点的父节点，strings是当前节点的名称，如果该TreeWidget设定了只有一列，则只显示strings[0]的内容。

- `QTreeWidgetItem(QTreeWidget *parent, int type = Type)`

  指定父节点parent而不制定节点名称，则在界面上显示为空节点。

- `QTreeWidgetItem(const QStringList &strings, int type = Type)`

  指定节点名称而不指定父节点，在当前界面不会显示出来，需要其父节点调用`addChild()`或者`addChildren()`才会显示在界面上。

- `QTreeWidgetItem(int type = Type)`

- `QTreeWidgetItem &operator=(const QTreeWidgetItem &other)`

- `virtual ~QTreeWidgetItem()`

- `void addChild(QTreeWidgetItem *child)`

  将子项追加到子项列表。子项即节点的名称，子项列表即节点的多个列的名称

- `void addChildren(const QList<QTreeWidgetItem *> &children)`

  将子项列表追加到该节点。

- `int indexOfChild(QTreeWidgetItem *child) const`

  返回项的子项列表中给定子项的索引。如果前面插入的子项正确的话，索引是正确的，否则返回-1。

- `void insertChild(int index, QTreeWidgetItem *child)`

  将给定的子级列表插入index处的子项列表。
  已经插入其他位置的子项将不会被插入。若插入位置index之前有空，则会插入空的位置。

- `void insertChildren(int index, const QList<QTreeWidgetItem *> &children)`

  将给定的子级列表插入index处的子项列表。
  已经插入其他位置的子项将不会被插入。若插入位置index之前有空，则会插入空的位置。

- `QBrush background(int column) const`

- `Qt::CheckState checkState(int column) const`

- `QTreeWidgetItem *child(int index) const`

- `int childCount() const`

- `QTreeWidgetItem::ChildIndicatorPolicy childIndicatorPolicy() const`

- `virtual QTreeWidgetItem *clone() const`

- `int columnCount() const`

- `virtual QVariant data(int column, int role) const`

- `Qt::ItemFlags flags() const`

- `QFont font(int column) const`

- `QBrush foreground(int column) const`

- `QIcon icon(int column) const`

- `bool isDisabled() const`

- `bool isExpanded() const`

- `bool isFirstColumnSpanned() const`

- `bool isHidden() const`

- `bool isSelected() const`

- `QTreeWidgetItem *parent() const`

- `virtual void read(QDataStream &in)`

- `void removeChild(QTreeWidgetItem *child)`

- `void setBackground(int column, const QBrush &brush)`

- `void setCheckState(int column, Qt::CheckState state)`

- `void setChildIndicatorPolicy(QTreeWidgetItem::ChildIndicatorPolicy policy)`

- `virtual void setData(int column, int role, const QVariant &value)`

- `void setDisabled(bool disabled)`

- `void setExpanded(bool expand)`

- `void setFirstColumnSpanned(bool span)`

- `void setFlags(Qt::ItemFlags flags)`

- `void setFont(int column, const QFont &font)`

- `void setForeground(int column, const QBrush &brush)`

- `void setHidden(bool hide)`

- `void setIcon(int column, const QIcon &icon)`

- `void setSelected(bool select)`

- `void setSizeHint(int column, const QSize &size)`

- `void setStatusTip(int column, const QString &statusTip)`

- `void setText(int column, const QString &text)`

- `void setTextAlignment(int column, int alignment)`

- `void setToolTip(int column, const QString &toolTip)`

- `void setWhatsThis(int column, const QString &whatsThis)`

- `QSize sizeHint(int column) const`

- `void sortChildren(int column, Qt::SortOrder order)`

- `QString statusTip(int column) const`

- `QTreeWidgetItem *takeChild(int index)`

- `QList<QTreeWidgetItem *> takeChildren()`

- `QString text(int column) const`

- `int textAlignment(int column) const`

- `QString toolTip(int column) const`

- `QTreeWidget *treeWidget() const`

- `int type() const`

- `QString whatsThis(int column) const`

- `virtual void write(QDataStream &out) const`

- `virtual bool operator<(const QTreeWidgetItem &other) const`