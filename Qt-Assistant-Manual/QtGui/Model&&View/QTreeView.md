# QTreeView

继承关系：`QTreeView`->`QAbstractItemView`->`QAbstractScrollArea`->`QFrame`->`QWidget`->`QObject and QPaintDevice`

继承者：`QTreeWidget`

##  1.Properties

- columnCount : int

  此属性保存在树小部件中显示的列数
  默认情况下，此属性的值为1。

- topLevelItemCount : const int 

  此属性保存顶级项目的数量
  默认情况下，此属性的值为0。

## 2.Public Functions

- QTreeWidget(QWidget *parent = nullptr)

- virtual ~QTreeWidget()

- **`void addTopLevelItem(QTreeWidgetItem *item)`**

  在小部件中将项目追加为顶级项目。

- **`void addTopLevelItems(const QList<QTreeWidgetItem *> &items)`**

  将项目列表追加为小部件中的顶级项目。

- void closePersistentEditor(QTreeWidgetItem *item, int column = 0)

  关闭给定列中项目的持久性编辑器。
  如果没有为该项目和列的组合打开任何持久性编辑器，则此功能无效。

- int columnCount() const

- int currentColumn() const

  返回树小部件中的当前列。

- QTreeWidgetItem *currentItem() const

  返回树小部件中的当前项目。

- void editItem(QTreeWidgetItem *item, int column = 0)

  如果可编辑，则开始编辑给定列中的项目。

- **`QList<QTreeWidgetItem *> findItems(const QString &text, Qt::MatchFlags flags, int column = 0) const`**

  在给定列中使用给定标志返回与给定文本匹配的项目列表。

- QTreeWidgetItem *headerItem() const

  返回用于树小部件标题的项目。

- **`int indexOfTopLevelItem(QTreeWidgetItem *item) const`**

  返回给定顶级项目的索引；如果找不到该项目，则返回-1。

- **`void insertTopLevelItem(int index, QTreeWidgetItem *item)`**

  在视图的最顶层将索引处插入项目。
  **如果该项目已经插入其他位置，则不会插入**。

- **`void insertTopLevelItems(int index, const QList<QTreeWidgetItem *> &items)`**

  在视图的最高级别的索引处插入项目列表。
  已经插入其他位置的项目将不会被插入。

- QTreeWidgetItem *invisibleRootItem() const

  返回树小部件的不可见根项。
  不可见的根项通过QTreeWidgetItem API提供对树控件的顶级项的访问，从而使得可以编写可以统一方式处理顶级项及其子级的函数； 例如，递归函数。

- bool isPersistentEditorOpen(QTreeWidgetItem *item, int column = 0) const

  返回是否为column列中的item打开了持久性编辑器。

- QTreeWidgetItem *itemAbove(const QTreeWidgetItem *item) const

  返回给定项目上方的项目。

- QTreeWidgetItem *itemBelow(const QTreeWidgetItem *item) const

  返回给定项目下方的项目。

- QTreeWidgetItem *itemAt(const QPoint &p) const

  返回在坐标p处指向该项目的指针。 坐标是相对于树控件的viewport（）的。

- QTreeWidgetItem *itemAt(int x, int y) const

  返回指向该项目在坐标（x，y）处的指针。 坐标是相对于树控件的viewport（）的。

- QWidget *itemWidget(QTreeWidgetItem *item, int column) const

  返回显示在由item和给定列指定的单元格中的窗口小部件。

- void removeItemWidget(QTreeWidgetItem *item, int column)

  删除给定列中给定项目中设置的小部件。

- void openPersistentEditor(QTreeWidgetItem *item, int column = 0)

- QList<QTreeWidgetItem *> selectedItems() const

  返回所有选定非隐藏项目的列表。

- void setColumnCount(int columns)

- void setCurrentItem(QTreeWidgetItem *item)

  在树小部件中设置当前项目。
  除非选择模式为NoSelection，否则也将选择该项目。

- void setCurrentItem(QTreeWidgetItem *item, int column)

  将树小部件中的当前项目和当前列设置为column。

- void setCurrentItem(QTreeWidgetItem *item, int column, QItemSelectionModel::SelectionFlags command)

  使用给定的命令将树小部件中的当前项目和当前列设置为column。

- **`void setHeaderItem(QTreeWidgetItem *item)`**

  设置树小部件的标题项。 标题中每列的标签由项目中的相应标签提供。

- void setHeaderLabel(const QString &label)

- **`void setHeaderLabels(const QStringList &labels)`**

  在标签列表中每个项目的标题中添加一列，并为每一列设置标签。
  请注意，setHeaderLabels（）不会删除现有列。

- void setItemWidget(QTreeWidgetItem *item, int column, QWidget *widget)

- int sortColumn() const

  返回用于对窗口小部件的内容进行排序的列。

- void sortItems(int column, Qt::SortOrder order)

  按给定列中的值以指定顺序对小部件中的项目进行排序。

- QTreeWidgetItem *takeTopLevelItem(int index)

  删除树中给定索引处的顶级项并返回它，否则返回nullptr。

- QTreeWidgetItem *topLevelItem(int index) const

  返回给定索引处的顶级项目，如果该项目不存在，则返回nullptr。

- int topLevelItemCount() const

- QRect visualItemRect(const QTreeWidgetItem *item) const

  返回item处该项目所占据的视口上的矩形。

## 3.Reimplemented Public Functions

- virtual void setSelectionModel(QItemSelectionModel *selectionModel) override

## 4.Public Slots

- void clear()

  通过删除其所有项目和选择来清除树小部件。
  注意：由于每个项目在删除之前都已从树小部件中删除，因此从项目的析构函数调用QTreeWidgetItem :: treeWidget（）的返回值将无效。

- **`void collapseItem(const QTreeWidgetItem *item)`**

  **关闭项目。 这将导致包含该项目子项的树被折叠**。

- **`void expandItem(const QTreeWidgetItem *item)`**

  **展开项目。 这将导致包含该项目子项的树被展开**。

- **`void scrollToItem(const QTreeWidgetItem *item, QAbstractItemView::ScrollHint hint = EnsureVisible)`**

  **确保该项目可见，如有必要，使用指定的提示滚动视图**。

  

## 5.Signals

- void currentItemChanged(QTreeWidgetItem *current, QTreeWidgetItem *previous)

  当前项目更改时将发出此信号。 当前项目由current指定，并且它将替换先前的当前项目。

- void itemActivated(QTreeWidgetItem *item, int column)

  当用户通过单击或双击（取决于平台，即根据QStyle :: SH_ItemView_ActivateItemOnSingleClick样式提示）或按特殊键（例如Enter）来激活项目时，将发出此信号。
  指定的项目是被单击的项目，如果未单击任何项目，则为nullptr。 该列是已单击的项目的列，如果未单击任何项目，则为-1。

- void itemChanged(QTreeWidgetItem *item, int column)

  当指定项目中列的内容更改时，将发出此信号。

- void itemClicked(QTreeWidgetItem *item, int column)

  当用户在窗口小部件内单击时，将发出此信号。
  指定的项目是单击的项目。 该列是单击的项目的列。 如果未单击任何项目，则不会发出信号。

- void itemCollapsed(QTreeWidgetItem *item)

  当指定的项目折叠起来时，将发出此信号，因此不会显示其所有子项。
  注意：如果在调用crashAll（）时更改项目的状态，则不会发出此信号。

- void itemDoubleClicked(QTreeWidgetItem *item, int column)

  当用户双击窗口小部件内部时，将发出此信号。
  指定的项目是被单击的项目，如果未单击任何项目，则为nullptr。 该列是单击的项目的列。 如果没有双击任何项目，则不会发出信号。

- **void itemEntered(QTreeWidgetItem *item, int column)**

  当鼠标光标在指定列上输入一个项目时，将发出此信号。 **要启用此功能，需要启用QTreeWidget鼠标跟踪。**

- void itemExpanded(QTreeWidgetItem *item)

  扩展指定项目时，将显示此信号，以便显示其所有子项。
  **注意：如果在调用expandAll（）时项目更改了其状态，则不会发出此信号**。

- void itemPressed(QTreeWidgetItem *item, int column)

  当用户在小部件内按下鼠标按钮时，将发出此信号。
  指定的项目是被单击的项目，如果未单击任何项目，则为nullptr。 该列是已单击的项目的列，如果未单击任何项目，则为-1。

- void itemSelectionChanged()

  当树形窗口小部件中的选择更改时，将发出此信号。 可以使用**selectedItems（）**找到当前选择。

## 6.Protected Functions

- virtual bool dropMimeData(QTreeWidgetItem *parent, int index, const QMimeData *data, Qt::DropAction action)
- QModelIndex indexFromItem(const QTreeWidgetItem *item, int column = 0) const
- QTreeWidgetItem *itemFromIndex(const QModelIndex &index) const
- virtual QMimeData *mimeData(const QList<QTreeWidgetItem *> items) const
- virtual QStringList mimeTypes() const
- virtual Qt::DropActions supportedDropActions() const

## 7.Reimplemented Protected Functions

- virtual void dropEvent(QDropEvent *event) override
- virtual bool event(QEvent *e) override

## 8.Detailed Description

QTreeWidget类是一个便利类，它为标准树小部件提供了一个经典的基于项目的界面，类似于Qt 3中的QListView类所使用的界面。此类基于Qt的Model / View体系结构，并使用默认模型来保存项目。 ，每个都是QTreeWidgetItem。
不需要Model / View框架灵活性的开发人员可以使用此类轻松创建简单的层次结构列表。 一种更灵活的方法涉及将QTreeView与标准项目模型结合在一起。 这允许将数据存储与其表示分离。

以最简单的形式，可以用以下方式构造树小部件：

```c++
QTreeWidget *treeWidget = new QTreeWidget();
treeWidget->setColumnCount(1);
QList<QTreeWidgetItem *> items;
for (int i = 0; i < 10; ++i)
	items.append(new QTreeWidgetItem(static_cast<QTreeWidget *>(nullptr), QStringList(QString("item: %1").arg(i))));
treeWidget->insertTopLevelItems(0, items);
```

在将项目添加到树小部件之前，必须使用setColumnCount（）设置列数。 这允许每个项目具有一个或多个标签或其他装饰。 使用中的列数可以通过columnCount（）函数找到。
该树可以具有一个标题，该标题包含窗口小部件中每个列的一部分。 通过提供带有setHeaderLabels（）的字符串列表来为每个部分设置标签是最容易的，但是可以使用QTreeWidgetItem构造自定义标头，并使用setHeaderItem（）函数将其插入树中。
树中的项目可以根据预定义的排序顺序按列进行排序。 如果启用了排序，则用户可以通过单击列标题来对项目进行排序。 可以通过调用setSortingEnabled（）启用或禁用排序。 isSortingEnabled（）函数指示是否启用排序。