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

 

# QTreeWidgetItem

- **enum Qt::ItemDataRole**

模型中的每个项目都有一组与之关联的数据元素，每个数据元素都有其自己的角色。 视图使用角色来向模型指示其需要哪种数据类型。 定制模型应返回这些类型的数据。
通用角色（和关联的类型）是：

| Constant           | Value | Description                                                  |
| ------------------ | ----- | ------------------------------------------------------------ |
| Qt::DisplayRole    | 0     | 要以文本形式呈现的关键数据。 （QString）                     |
| Qt::DecorationRole | 1     | 以图标形式呈现为装饰的数据。 （QColor，QIcon或QPixmap）      |
| Qt::EditRole       | 2     | 数据格式适合在编辑器中进行编辑。 （QString）                 |
| Qt::ToolTipRole    | 3     | 数据显示在项目的工具提示中。 （QString）                     |
| Qt::StatusTipRole  | 4     | 状态栏中显示的数据。 （QString）                             |
| Qt::WhatsThisRole  | 5     | The data displayed for the item in "What's This?" mode. (QString) |
| Qt::SizeHintRole   | 13    | 将提供给视图的项目的大小提示。 （QSize）                     |

描述外观和元数据（具有关联类型）的角色：

| Constant                 | Value          | Description                                                  |
| ------------------------ | -------------- | ------------------------------------------------------------ |
| Qt::FontRole             | 6              | 用于使用默认委托(delegate)渲染的项目的字体。 （QFont）       |
| Qt::TextAlignmentRole    | 7              | 使用默认委托(delegate)渲染的项目的文本对齐方式。 （Qt :: Alignment） |
| Qt::BackgroundRole       | 8              | 用于使用默认委托渲染的项目的背景画笔。 （QBrush）            |
| Qt::BackgroundColorRole  | BackgroundRole | 该角色已过时。 改用BackgroundRole                            |
| Qt::ForegroundRole       | 9              | 用于使用默认委托渲染的项目的前景色画笔（通常为文本颜色）。 （QBrush） |
| Qt::TextColorRole        | ForegroundRole | 该角色已过时。 请改用ForegroundRole。                        |
| Qt::CheckStateRole       | 10             | 该角色用于获取项目的检查状态。 （Qt :: CheckState）          |
| Qt::InitialSortOrderRole | 14             | 该角色用于获取标题视图节的初始排序顺序。 （Qt :: SortOrder）。 这个角色是在Qt 4.8中引入的。 |

辅助功能角色（具有关联的类型）：

| Constant                      | Value | Description                                                  |
| ----------------------------- | ----- | ------------------------------------------------------------ |
| Qt::AccessibleTextRole        | 11    | 辅助功能扩展和插件（例如屏幕阅读器）使用的文本。 （QString） |
| Qt::AccessibleDescriptionRole | 12    | 出于可访问性目的而对项目的描述。 （QString）                 |

用户角色：

| Constant     | Value  | Description                              |
| ------------ | ------ | ---------------------------------------- |
| Qt::UserRole | 0x0100 | 可以用于特定于应用程序目的的第一个角色。 |

对于用户角色，由开发人员决定使用哪种类型，并确保组件在访问和设置数据时使用正确的类型。

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

- **virtual void setData(int column, int role, const QVariant &value)**

  将项目的列和角色的值设置为给定值。
  该角色描述由值指定的数据类型，并由Qt :: ItemDataRole枚举定义。
  注意：默认实现将Qt :: EditRole和Qt :: DisplayRole视为引用相同的数据。

- **virtual QVariant data(int column, int role) const**

  返回项目的列和角色的值。返回的值可以再调用value<数据类型>()函数来获取存储的自定义数据。

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

#  3.Protected Functions

- void emitDataChanged()

# 4.Related Non-Members

- QDataStream &operator<<(QDataStream &out, const QTreeWidgetItem &item)
- QDataStream &operator>>(QDataStream &in, QTreeWidgetItem &item)

# 5.Detailed Description

树小部件项目用于保存树小部件的信息行。行通常包含几列数据，**每列数据可以包含一个文本标签和一个图标**。
QTreeWidgetItem类是一个便利类，它代替了Qt 3中的QListViewItem类。它提供了一个与QTreeWidget类一起使用的项目。
通常使用父项构造项目，该父项可以是QTreeWidget（用于顶级项目）或QTreeWidgetItem（用于树中较低级别的项目）。例如，以下代码构造一个顶级项目来表示世界城市，并为奥斯陆添加一个条目作为子项：

```c++
QTreeWidgetItem *cities = new QTreeWidgetItem(treeWidget);
cities->setText(0, tr("Cities"));
QTreeWidgetItem *osloItem = new QTreeWidgetItem(cities);
osloItem->setText(0, tr("Oslo"));
osloItem->setText(1, tr("Yes"));
```

可以通过指定在构建项目时遵循的项目来按特定顺序添加项目：

```c++
QTreeWidgetItem *planets = new QTreeWidgetItem(treeWidget, cities);
planets->setText(0, tr("Planets"));
```

一个项目中的每一列都可以有自己的背景画笔，可以通过setBackground（）函数进行设置。当前的背景画笔可以通过background（）找到。每列的文本标签可以使用其自己的字体和笔刷呈现。这些由setFont（）和setForeground（）函数指定，并由font（）和frontant（）读取。
顶层项目与树的较低层项目之间的主要区别在于，顶层项目没有parent（）。此信息可用于区分项目之间的区别，并且有助于了解何时从树中插入和删除项目。可以使用takeChild（）删除项目的子项，并使用insertChild（）函数将其插入子项列表中的给定索引。
默认情况下，项目是启用(enabled)，可选(selectable)，可检查的(checkable)，并且可以作为拖放操作的来源。可以通过使用适当的值调用setFlags（）来更改每个项目的标志。可以使用setCheckState（）函数检查和取消检查可检查项。相应的checkState（）函数指示当前是否检查了该项。

- 子类化**Subclassing**
  当将QTreeWidgetItem子类化以提供自定义项目时，可以为其定义新类型，以便将它们与标准项目区分开。 需要此功能的子类的构造函数需要使用等于或大于UserType的新类型值来调用基类构造函数。