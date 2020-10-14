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

# 3.Signals

- `void currentItemChanged(QTreeWidgetItem *current, QTreeWidgetItem *previous)`

  当前项目更改时将发出此信号。 当前项目由current指定，并且它将替换先前的当前项目。

- `void itemActivated(QTreeWidgetItem *item, int column)`

  当用户通过单击或双击（取决于平台，即根据QStyle :: SH_ItemView_ActivateItemOnSingleClick样式提示）或按特殊键（例如Enter）来激活项目时，将发出此信号。
  指定的项目是被单击的项目，如果未单击任何项目，则为nullptr。 该列是已单击的项目的列，如果未单击任何项目，则为-1。

- `void itemChanged(QTreeWidgetItem *item, int column)`

  当指定项目中列的内容更改时，将发出此信号。

- `void itemClicked(QTreeWidgetItem *item, int column)`

  当用户在窗口小部件内单击时，将发出此信号。
  指定的项目是单击的项目。 该列是单击的项目的列。 如果未单击任何项目，则不会发出信号。

- `void itemCollapsed(QTreeWidgetItem *item)`

  当指定的项目折叠起来时，将发出此信号，因此不会显示其所有子项。
  注意：如果在调用crashAll（）时更改项目的状态，则不会发出此信号。

- `void itemDoubleClicked(QTreeWidgetItem *item, int column)`

  当用户双击窗口小部件内部时，将发出此信号。
  指定的项目是被单击的项目，如果未单击任何项目，则为nullptr。 该列是单击的项目的列。 如果没有双击任何项目，则不会发出信号。

- `void itemEntered(QTreeWidgetItem *item, int column)`

  当鼠标光标在指定列上输入一个项目时，将发出此信号。 要启用此功能，需要启用QTreeWidget鼠标跟踪。

- `void itemExpanded(QTreeWidgetItem *item)`

  扩展指定项目时，将显示此信号，以显示其所有子项。
  注意：如果在调用expandAll（）时项目更改了其状态，则不会发出此信号。

- `void itemPressed(QTreeWidgetItem *item, int column)`

  当用户在小部件内按下鼠标按钮时，将发出此信号。
  指定的项目是被单击的项目，如果未单击任何项目，则为nullptr。 该列是已单击的项目的列，如果未单击任何项目，则为-1。

- `void itemSelectionChanged()`

  当树形窗口小部件中的选择更改时，将发出此信号。 当前选择可以通过selectedItems（）找到。

 
