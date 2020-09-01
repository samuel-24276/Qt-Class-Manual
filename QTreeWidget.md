# 一，QTreeWidget

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

 

# 二，QTreeWidgetItem

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

  将项目的标志设置为给定标志。 这些决定了是否可以选择或修改项目。 通常用于禁用项目。

  enum Qt::ItemFlag
  flags Qt::ItemFlags

  | Constant                 | Value              | Description                                                  |
  | ------------------------ | ------------------ | ------------------------------------------------------------ |
  | Qt::NoItemFlags          | 0                  | 它没有设置任何属性。                                         |
  | Qt::ItemIsSelectable     | 1                  | 可被选中                                                     |
  | Qt::ItemIsEditable       | 2                  | 可被编辑                                                     |
  | Qt::ItemIsDragEnabled    | 4                  | 可被拖拽                                                     |
  | Qt::ItemIsDropEnabled    | 8                  | 可以用作放置目标。                                           |
  | Qt::ItemIsUserCheckable  | 16                 | 用户可以选中或取消选中它。                                   |
  | Qt::ItemIsEnabled        | 32                 | 用户可以与该项目进行交互。                                   |
  | Qt::ItemIsAutoTristate   | 64                 | 项目的状态取决于其子级的状态。 这样可以自动管理QTreeWidget中父项的状态（检查是否选中了所有子项；如果选中了所有子项，则不选中；如果仅选中了一些子项，则部分选中）。 |
  | Qt::ItemIsTristate       | ItemIsAutoTristate | 此枚举值已弃用。 请改用Qt :: ItemIsAutoTristate。            |
  | Qt::ItemNeverHasChildren | 128                | 该物品永远不会有子物品。 这仅用于优化目的。                  |
  | Qt::ItemIsUserTristate   | 256                | 用户可以循环浏览三个单独的状态。                             |

  

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

# 三，QAbstractItemModel

继承关系：`QAbstractItemModel`->`QObject`

继承者：

- QAbstractListModel
-  QAbstractProxyModel 
- QAbstractTableModel
- QConcatenateTablesProxyModel
- QDirModel
- QFileSystemModel
- QStandardItemModel

# 1.Public Types

- `enum class CheckIndexOption { NoOption, IndexIsValid, DoNotUseParent, ParentIsInvalid }`
- `flags CheckIndexOptions`
- `enum LayoutChangeHint { NoLayoutChangeHint, VerticalSortHint, HorizontalSortHint }`

# 2.Public Functions

- QAbstractItemModel(QObject *parent = nullptr)

- virtual ~QAbstractItemModel()

- virtual QModelIndex buddy(const QModelIndex &index) const

- virtual bool canDropMimeData(const QMimeData *data, Qt::DropAction action, int row, int 

  column, const QModelIndex &parent) const

- virtual bool canFetchMore(const QModelIndex &parent) const

- bool checkIndex(const QModelIndex &index, QAbstractItemModel::CheckIndexOptions options = CheckIndexOption::NoOption) const

- virtual int columnCount(const QModelIndex &parent = QModelIndex()) const = 0

- virtual QVariant data(const QModelIndex &index, int role = Qt::DisplayRole) const = 0

- virtual bool dropMimeData(const QMimeData *data, Qt::DropAction action, int row, int column, const QModelIndex &parent)

- virtual void fetchMore(const QModelIndex &parent)

- virtual Qt::ItemFlags flags(const QModelIndex &index) const

- virtual bool hasChildren(const QModelIndex &parent = QModelIndex()) const

- bool hasIndex(int row, int column, const QModelIndex &parent = QModelIndex()) const

- virtual QVariant headerData(int section, Qt::Orientation orientation, int role = Qt::DisplayRole) const

- virtual QModelIndex index(int row, int column, const QModelIndex &parent = QModelIndex()) const = 0

- bool insertColumn(int column, const QModelIndex &parent = QModelIndex())

- virtual bool insertColumns(int column, int count, const QModelIndex &parent = QModelIndex())

- bool insertRow(int row, const QModelIndex &parent = QModelIndex())

- virtual bool insertRows(int row, int count, const QModelIndex &parent = QModelIndex())

- virtual QMap<int, QVariant> itemData(const QModelIndex &index) const

- virtual QModelIndexList match(const QModelIndex &start, int role, const QVariant &value, int 

  hits = 1, Qt::MatchFlags flags = Qt::MatchFlags(Qt::MatchStartsWith|Qt::MatchWrap)) const

- virtual QMimeData *mimeData(const QModelIndexList &indexes) const

- virtual QStringList mimeTypes() const

- bool moveColumn(const QModelIndex &sourceParent, int sourceColumn, const QModelIndex &destinationParent, int destinationChild)

- virtual bool moveColumns(const QModelIndex &sourceParent, int sourceColumn, int count, const QModelIndex &destinationParent, int destinationChild)

- bool moveRow(const QModelIndex &sourceParent, int sourceRow, const QModelIndex &destinationParent, int destinationChild)

- virtual bool moveRows(const QModelIndex &sourceParent, int sourceRow, int count, const QModelIndex &destinationParent, int destinationChild)

- virtual QModelIndex parent(const QModelIndex &index) const = 0

- bool removeColumn(int column, const QModelIndex &parent = QModelIndex())

- virtual bool removeColumns(int column, int count, const QModelIndex &parent = QModelIndex())

- bool removeRow(int row, const QModelIndex &parent = QModelIndex())

- virtual bool removeRows(int row, int count, const QModelIndex &parent = QModelIndex())

- virtual QHash<int, QByteArray> roleNames() const

- virtual int rowCount(const QModelIndex &parent = QModelIndex()) const = 0

- virtual bool setData(const QModelIndex &index, const QVariant &value, int role = Qt::EditRole)

- virtual bool setHeaderData(int section, Qt::Orientation orientation, const QVariant &value, int role = Qt::EditRole)

- virtual bool setItemData(const QModelIndex &index, const QMap<int, QVariant> &roles)

- virtual QModelIndex sibling(int row, int column, const QModelIndex &index) const

- virtual void sort(int column, Qt::SortOrder order = Qt::AscendingOrder)

- virtual QSize span(const QModelIndex &index) const

- virtual Qt::DropActions supportedDragActions() const

- virtual Qt::DropActions supportedDropActions() const

# 3.Public Slots

- virtual void revert()
- virtual bool submit()

# 4.Signals

- void columnsAboutToBeInserted(const QModelIndex &parent, int first, int last)
- void columnsAboutToBeMoved(const QModelIndex &sourceParent, int sourceStart, int sourceEnd, const QModelIndex &destinationParent, int destinationColumn)
- void columnsAboutToBeRemoved(const QModelIndex &parent, int first, int last)
- void columnsInserted(const QModelIndex &parent, int first, int last)
- void columnsMoved(const QModelIndex &parent, int start, int end, const QModelIndex &destination, int column)
- void columnsRemoved(const QModelIndex &parent, int first, int last)
- void dataChanged(const QModelIndex &topLeft, const QModelIndex &bottomRight, const QVector<int> &roles = QVector<int>())
- void headerDataChanged(Qt::Orientation orientation, int first, int last)
- void layoutAboutToBeChanged(const QList<QPersistentModelIndex> &parents = 
- QList<QPersistentModelIndex>(), QAbstractItemModel::LayoutChangeHint hint = QAbstractItemModel::NoLayoutChangeHint)
- void layoutChanged(const QList<QPersistentModelIndex> &parents = QList<QPersistentModelIndex>(), QAbstractItemModel::LayoutChangeHint hint = QAbstractItemModel::NoLayoutChangeHint)
- void modelAboutToBeReset()
- void modelReset()
- void rowsAboutToBeInserted(const QModelIndex &parent, int start, int end)
- void rowsAboutToBeMoved(const QModelIndex &sourceParent, int sourceStart, int sourceEnd, const QModelIndex &destinationParent, int destinationRow)
- void rowsAboutToBeRemoved(const QModelIndex &parent, int first, int last)
- void rowsInserted(const QModelIndex &parent, int first, int last)
- void rowsMoved(const QModelIndex &parent, int start, int end, const QModelIndex &destination, int row)
- void rowsRemoved(const QModelIndex &parent, int first, int last)

# 4.Protected Functions

- void beginInsertColumns(const QModelIndex &parent, int first, int last)
- void beginInsertRows(const QModelIndex &parent, int first, int last)
- bool beginMoveColumns(const QModelIndex &sourceParent, int sourceFirst, int sourceLast, const QModelIndex &destinationParent, int destinationChild)
- bool beginMoveRows(const QModelIndex &sourceParent, int sourceFirst, int sourceLast, const QModelIndex &destinationParent, int destinationChild)
- void beginRemoveColumns(const QModelIndex &parent, int first, int last)
- void beginRemoveRows(const QModelIndex &parent, int first, int last)
- void beginResetModel()
- void changePersistentIndex(const QModelIndex &from, const QModelIndex &to)
- void changePersistentIndexList(const QModelIndexList &from, const QModelIndexList &to)
  QModelIndex createIndex(int row, int column, void *ptr = nullptr) const
- QModelIndex createIndex(int row, int column, quintptr id) const
- void endInsertColumns()
- void endInsertRows()
- void endMoveColumns()
- void endMoveRows()
- void endRemoveColumns()
- void endRemoveRows()
- void endResetModel()
- QModelIndexList persistentIndexList() const

# 5.Protected Slots

- void resetInternalData()

# 6.Detailed Description



# 四，QModelIndex

# 1.Public Functions

- `QModelIndex()`

  创建一个新的空模型索引。 这种类型的模型索引用于指示模型中的位置无效。

- `int column() const`

  返回此模型索引引用的列。

- `QVariant data(int role = Qt::DisplayRole) const`

  返回索引所引用项目的给定角色的数据。

- `Qt::ItemFlags flags() const`

  返回索引所引用项目的标志。

- `quintptr internalId() const`

  返回模型使用的quintptr，以将索引与内部数据结构相关联。

- `void *internalPointer() const`

  返回模型使用的void *指针，以将索引与内部数据结构相关联。

- `bool isValid() const`

  如果此模型索引有效，则返回true；否则，返回false。
  有效索引属于模型，并且具有非负的行号和列号。

- `const QAbstractItemModel *model() const`

  返回指向包含该索引所引用项目的模型的指针。
  返回指向模型的const指针，因为对模型的非const函数的调用可能会使模型索引无效并使应用程序崩溃。

- `QModelIndex parent() const`

  返回模型索引的父级，如果没有父级，则返回QModelIndex（）。

- `int row() const`

  返回此模型索引引用的行。

- `QModelIndex sibling(int row, int column) const`

  **返回行和列的同级。 如果此位置没有兄弟姐妹，则返回无效的QModelIndex。**

- `QModelIndex siblingAtColumn(int column) const`

  返回当前行的列的同级。 如果此位置没有兄弟姐妹，则返回无效的QModelIndex。

- `QModelIndex siblingAtRow(int row) const`

  返回当前列的行的同级。 如果此位置没有兄弟姐妹，则返回无效的QModelIndex。

- `bool operator!=(const QModelIndex &other) const`

  如果此模型索引与另一个模型索引不在同一个位置，则返回true；否则返回false。

- `bool operator<(const QModelIndex &other) const`

  如果此模型索引小于另一个模型索引，则返回true；否则返回false。
  小于计算对开发人员不是直接有用的-没有定义具有不同父级的索引进行比较的方式。 仅存在此运算符，以便该类可与QMap一起使用。

- `bool operator==(const QModelIndex &other) const`

  如果此模型索引与另一个模型索引位于同一位置，则返回true；否则返回false。
  与另一个模型索引进行比较时，将使用内部数据指针，行，列和模型值

# 2.Related Non-Members

- `typedef QModelIndexList`

  即QList <QModelIndex>

# 3.Detailed Description

此类用作**QAbstractItemModel**派生的项目模型的索引。**项目视图，委托（delegates）和选择模型使用索引在模型中定位项目**。

模型使用**QAbstractItemModel :: createIndex（）**函数创建新的QModelIndex对象。可以使用QModelIndex构造函数构造无效的模型索引。当引用模型中的顶级项目时，无效索引通常用作父索引。
模型索引引用模型中的项目，并包含指定它们在这些模型中的位置所需的所有信息。**每个索引位于给定的行和列中，并且可以具有父索引；使用row（），column（）和parent（）获得此信息**。模型中的每个顶级项都由没有父索引的模型索引表示-在这种情况下，parent（）将返回无效的模型索引，该索引等效于使用QModelIndex（）的零参数形式构造的索引。
若要获取引用模型中现有项目的模型索引，请调用**QAbstractItemModel :: index（）**，其中包含所需的行和列值以及父级的模型索引。**当引用模型中的顶级项目时，请提供QModelIndex（）作为父索引**。
model（）函数将索引引用的模型作为QAbstractItemModel返回。 child（）函数用于检查模型中索引下的项。 sibling（）函数允许您遍历模型中与索引相同级别的项目。
注意：应立即使用模型索引，然后将其丢弃。在调用更改模型结构或删除项目的模型函数后，不应依赖索引来保持有效。如果您需要随时间保持模型索引，请使用QPersistentModelIndex。