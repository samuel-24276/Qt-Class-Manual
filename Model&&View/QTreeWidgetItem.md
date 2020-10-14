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