# QAbstractItemModel

继承关系：`QAbstractItemModel`->`QObject`

继承者：

- QAbstractListModel——列表模型的抽象基类
- QAbstractProxyModel ——代理模型的抽象类
- QAbstractTableModel——表格模型的抽象基类
- QAbstractProxyModel
- QConcatenateTablesProxyModel
- QDirModel——文件和目录的存储模型
- QFileSystemModel
- QHelpContentModel
- QStandardItemModel

> 模型视图(InterView)框架的所有模型都基于抽象基类QAbstractItemModel，完成QStringList存储的QStringListModel类继承自QAbstractListModel类，而与数据库有关的QSqlQueryModel类继承自QAbstractTableModel类。

# 1.Public Types

- `enum class CheckIndexOption { NoOption, IndexIsValid, DoNotUseParent, ParentIsInvalid }`

  `flags CheckIndexOptions`

  该枚举可用于控制QAbstractItemModel :: checkIndex（）执行的检查。

  | Constant                                              | Value  | Description                                                  |
  | ----------------------------------------------------- | ------ | ------------------------------------------------------------ |
  | QAbstractItemModel::CheckIndexOption::NoOption        | 0x0000 | 没有指定检查选项。                                           |
  | QAbstractItemModel::CheckIndexOption::IndexIsValid    | 0x0001 | 传递给QAbstractItemModel :: checkIndex（）的模型索引被检查为有效的模型索引。 |
  | QAbstractItemModel::CheckIndexOption::DoNotUseParent  | 0x0002 | 不执行任何涉及传递给QAbstractItemModel :: checkIndex（）的索引父级使用的检查。 |
  | QAbstractItemModel::CheckIndexOption::ParentIsInvalid | 0x0003 | 传递给QAbstractItemModel :: checkIndex（）的模型索引的父级被检查为无效的模型索引。 如果同时指定了此选项和DoNotUseParent，则将忽略此选项。 |

  

- `enum LayoutChangeHint { NoLayoutChangeHint, VerticalSortHint, HorizontalSortHint }`

  该枚举描述了模型更改布局的方式。

  | Constant                               | Value | Description    |
  | -------------------------------------- | ----- | -------------- |
  | QAbstractItemModel::NoLayoutChangeHint | 0     | 没有提示可用。 |
  | QAbstractItemModel::VerticalSortHint   | 1     | 行正在排序。   |
  | QAbstractItemModel::HorizontalSortHint | 2     | 列正在排序。   |

  

# 2.Public Functions

- QAbstractItemModel(QObject *parent = nullptr)

- virtual ~QAbstractItemModel()

- virtual QModelIndex buddy(const QModelIndex &index) const

  **返回由index表示的*项目的伙伴的模型索引***。 当用户想要编辑项目时，视图将调用此函数以检查是否应改为编辑模型中的另一个项目。 然后，视图将使用伙伴项返回的模型索引构造一个委托。
  此功能的默认实现将每个项目都作为自己的伙伴。

- virtual bool canDropMimeData(const QMimeData *data, Qt::DropAction action, int row, int column, const QModelIndex &parent) const

  **如果模型可以接受数据删除，则返回true**。 此默认实现仅检查mimeTypes（）列表中的数据是否至少具有一种格式，以及动作是否在模型的supportedDropActions（）中。
  如果要测试是否可以通过操作将数据删除到行，列，父级，请在自定义模型中重新实现此功能。 如果您不需要该测试，则无需重新实现此功能。

- virtual bool canFetchMore(const QModelIndex &parent) const

  如果有更多数据可用于父项，则返回true；否则返回true。 否则返回false。
  默认实现始终返回false。
  如果canFetchMore（）返回true，则应调用fetchMore（）函数。 例如，这就是QAbstractItemView的行为。
  注意：可以通过元对象系统和QML调用此函数。 请参阅Q_INVOKABLE。

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

  让模型知道应该**丢弃缓存的信息**。 此功能通常用于行编辑。

- virtual bool submit()

  让模型知道它应该**将缓存的信息提交到永久存储**。 此功能通常用于行编辑。
  如果没有错误，则返回true；否则返回false。 否则返回false。

# 4.Signals

- void columnsAboutToBeInserted(const QModelIndex &parent, int first, int last)

  **在将列插入模型之前就发出此信号**。 新项目将位于给定父项目下的首尾之间。
  注意：连接到该信号的组件使用它来适应模型尺寸的变化。 它只能由QAbstractItemModel实现发出，而不能在子类代码中显式发出。
  注意：**这是一个私有信号。 它可以用于信号连接，但不能由用户发射**。

- void columnsInserted(const QModelIndex &parent, int first, int last)

  **在将列插入模型后，将发出此信号**。 新项目是给定父项目下的第一个到最后一个（包括）之间的项目。
  注意：连接到该信号的组件使用它来适应模型尺寸的变化。 它只能由QAbstractItemModel实现发出，而不能在子类代码中显式发出。

  注意：**这是一个私有信号。 它可以用于信号连接，但不能由用户发射**。

- void columnsAboutToBeMoved(const QModelIndex &sourceParent, int sourceStart, int sourceEnd, const QModelIndex &destinationParent, int destinationColumn)

  **信号在模型中移动列之前发出**。 将要移动的项目是在给定sourceParent项目下在sourceStart和sourceEnd之间（包括首尾）的项目。 从列destinationColumn开始，它们将被移到destinationParent。
  注意：连接到该信号的组件使用它来适应模型尺寸的变化。 它只能由QAbstractItemModel实现发出，而不能在子类代码中显式发出。
  注意：**这是一个私有信号。 它可以用于信号连接，但不能由用户发射**。

- void columnsMoved(const QModelIndex &parent, int start, int end, const QModelIndex &destination, int column)

  **列在模型中移动后，将发出此信号**。 给定父项下包含“开始”和“结束”之间的项已从列开始移动到目标。
  注意：连接到该信号的组件使用它来适应模型尺寸的变化。 它只能由QAbstractItemModel实现发出，而不能在子类代码中显式发出。

  注意：**这是一个私有信号。 它可以用于信号连接，但不能由用户发射**。

- void columnsAboutToBeRemoved(const QModelIndex &parent, int first, int last)

  **在从模型中删除列之前，将发出此信号**。 要删除的项目是给定父项目下的第一个到最后一个（含）之间的项目。
  注意：连接到该信号的组件使用它来适应模型尺寸的变化。 它只能由QAbstractItemModel实现发出，而不能在子类代码中显式发出。

  注意：**这是一个私有信号。 它可以用于信号连接，但不能由用户发射**。

- void columnsRemoved(const QModelIndex &parent, int first, int last)

  **从模型中删除列后，将发出此信号**。 删除的项目是给定父项目下的第一个到最后一个（含）之间的项目。
  注意：连接到该信号的组件使用它来适应模型尺寸的变化。 它只能由QAbstractItemModel实现发出，而不能在子类代码中显式发出。

  注意：**这是一个私有信号。 它可以用于信号连接，但不能由用户发射**。

- void rowsAboutToBeInserted(const QModelIndex &parent, int start, int end)

  

- void rowsAboutToBeMoved(const QModelIndex &sourceParent, int sourceStart, int sourceEnd, const QModelIndex &destinationParent, int destinationRow)

  

- void rowsAboutToBeRemoved(const QModelIndex &parent, int first, int last)

  

- void rowsInserted(const QModelIndex &parent, int first, int last)

  

- void rowsMoved(const QModelIndex &parent, int start, int end, const QModelIndex &destination, int row)

  

- void rowsRemoved(const QModelIndex &parent, int first, int last)

  

- void dataChanged(const QModelIndex &topLeft, const QModelIndex &bottomRight, const QVector<int> &roles = QVector<int>())

  **只要现有项目中的数据发生更改，就会发出此信号**。
  如果项目是同一父项，则受影响的项目是在topLeft和bottomRight（含）之间的项目。 如果项目没有相同的父项，则行为是不确定的。
  **重新实现setData（）函数时，必须显式发出此信号**。
  可选角色参数可用于指定实际上已修改了哪些数据角色。 Roles参数中的向量为空，表示应将所有角色视为已修改。 角色参数中元素的顺序没有任何关联。

- void headerDataChanged(Qt::Orientation orientation, int first, int last)

  **每当头改变时，该信号被发射**。 方向指示水平或垂直标题是否已更改。 标题中从头到尾的部分需要更新。
  **重新实现setHeaderData（）函数时，必须显式发出此信号**。
  如果要更改列数或行数，则不需要发出此信号，而可以使用begin / end函数（有关详细信息，请参见QAbstractItemModel类描述中的子类化部分）。

- void layoutAboutToBeChanged(const QList<QPersistentModelIndex> &parents = QList<QPersistentModelIndex>(), QAbstractItemModel::LayoutChangeHint hint = QAbstractItemModel::NoLayoutChangeHint)

  **信号在模型布局更改之前发出**。 连接到该信号的组件使用它来适应模型布局的变化。
  **子类在发出layoutAboutToBeChanged（）之后应更新所有持久性模型索引**。
  可选的parents参数用于给出有关模型布局的哪些部分正在更改的更具体的通知。 空列表表示更改了整个模型的布局。 父级列表中元素的顺序并不重要。 可选的hint参数用于提示模型重新布局时发生的情况。

- void layoutChanged(const QList<QPersistentModelIndex> &parents = QList<QPersistentModelIndex>(), QAbstractItemModel::LayoutChangeHint hint = QAbstractItemModel::NoLayoutChangeHint)

  **只要模型暴露的项目的*布局*发生变化，就会发出此信号**。 例如，对模型进行排序时。 当视图接收到该信号时，它应更新项目的布局以反映此更改。
  *子类化QAbstractItemModel或QAbstractProxyModel时，请确保在更改项目顺序或更改要公开给视图的数据的结构之前发出layoutAboutToBeChanged（），并在更改布局后发出layoutChanged（）*。
  可选的parents参数用于给出有关模型布局的哪些部分正在更改的更具体的通知。 空列表表示更改了整个模型的布局。 父级列表中元素的顺序并不重要。 可选的hint参数用于提示模型重新布局时发生的情况。
  子类应在发出layoutChanged（）之前更新所有持久性模型索引。 换句话说，当结构改变时：

  - emit layoutAboutToBeChanged()
  - 记住将改变的QModelIndex
  - 更新您的内部数据
  - 调用changePersistentIndex()
  - emit layoutChanged()

- void modelAboutToBeReset()

  **在模型的内部状态（例如持久性模型索引）无效之前，调用beginResetModel（）会发出此信号**。

  注意：**这是一个私有信号。 它可以用于信号连接，但不能由用户发射**。

- void modelReset()

  **在模型的内部状态（例如持久性模型索引）无效之后，调用endResetModel（）时将发出此信号**。
  请注意，如果重置了模型，则应认为先前从模型中检索到的所有信息均无效。 这包括但不限于rowCount（）和columnCount（），flags（），通过data（）检索的数据和roleNames（）。
  注意：**这是一个私人信号。 它可以用于信号连接，但不能由用户发射**。

# 5.Protected Functions

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

# 6.Protected Slots

- void resetInternalData()

# 7.Detailed Description

`QAbstractItemModel`类定义了项目模型必须使用的标准接口，才能与模型/视图体系结构中的其他组件进行互操作。 **它不应该直接实例化。 相反，您应该将其子类化以创建新模型**。
`QAbstractItemModel`类是Model / View类之一，并且是Qt模型/视图框架的一部分。 它可以用作QML中**项目视图元素**或Qt Widgets模块中项目视图类的**基础数据模型**。
如果您需要一个用于项目视图的模型，例如QML的`List View`元素或C ++小部件`QListView`或`QTableView`，则应考虑继承QAbstractListModel或QAbstractTableModel而不是此类。
**基础数据模型作为表的层次结构公开给视图和委托。 如果不使用层次结构，则模型是一个简单的行和列表。 *每个项目都有一个由QModelIndex指定的唯一索引***。

可以通过模型访问的每个数据项都有一个关联的模型索引。您可以使用index（）函数获得此模型索引。每个索引都可以具有sibling（）索引；子项具有parent（）索引。
每个项目都有许多与之关联的数据元素，可以通过为模型的data（）函数指定一个角色（请参阅Qt :: ItemDataRole）来检索它们。可以使用itemData（）函数同时获取所有可用角色的数据。
使用特定的`Qt :: ItemDataRole`设置每个角色的数据。可以使用s`etData（）`单独设置各个角色的数据，也可以使用`setItemData（）`设置所有角色的数据。
可以使用flags（）查询项目（请参阅Qt :: ItemFlag），以查看是否可以通过其他方式选择，拖动或操纵它们。
如果项目具有子对象，则`hasChildren（）`对于相应的索引返回true。
该模型在层次结构的每个级别都有一个rowCount（）和columnCount（）。可以使用insertRows（），insertColumns（），removeRows（）和removeColumns（）插入和删除行和列。
模型发出信号以指示变化。例如，只要模型可用的数据项发生更改，就会发出dataChanged（）。对模型提供的标头的更改将导致发出headerDataChanged（）。如果基础数据的结构发生了变化，则模型可以发出layoutChanged（）来向任何附加的视图指示它们应该重新显示所显示的任何项目，并考虑到新的结构。
可以使用match（）函数在模型中搜索可用的项目以查找特定数据。
要对模型进行排序，可以使用sort（）。

## Subclassing子类化

注意：“模型子类别参考”中提供了一些子类别模型的一般准则。
**子类化QAbstractItemModel时，至少必须实现index（），parent（），rowCount（），columnCount（）和data（）**。这些功能在所有只读模型中使用，并构成可编辑模型的基础。
您也可以重新实现hasChildren（），以为rowCount（）的实现成本很高的模型提供特殊的行为。这使得模型可以限制视图请求的数据量，并且可以用作实现模型数据的惰性填充的一种方式。
**要在模型中启用编辑，还必须实现setData（）和重新实现flags（）以确保返回ItemIsEditable**。您还可以重新实现headerData（）和setHeaderData（）来控制呈现模型标头的方式。
**当分别重新实现setData（）和setHeaderData（）函数时，必须显式发出dataChanged（）和headerDataChanged（）信号**。
定制模型需要创建模型索引以供其他组件使用。为此，请使用适当的行号和列号以及相应的标识符调用createIndex（），并将其作为指针或整数值。这些值的组合对于每个项目都必须是唯一的。定制模型通常在其他重新实现的函数中使用这些唯一标识符，以检索项目数据并访问有关该项目的父项和子项的信息。有关唯一标识符的更多信息，请参见简单树模型示例。
不必支持`Qt :: ItemDataRole`中定义的每个角色。根据模型中包含的数据类型，可能只有实现data（）函数以返回一些更常见角色的有效信息才有用。大多数模型至少为`Qt :: DisplayRole`提供项目数据的文本表示，行为良好的模型也应为`Qt :: ToolTipRole`和`Qt :: WhatsThisRole`提供有效的信息。支持这些角色可使模型与标准Qt视图一起使用。但是，对于某些处理高度专业化数据的模型，仅为用户定义的角色提供数据可能是合适的。
提供可调整大小的数据结构接口的模型可以提供insertRows（），removeRows（），insertColumns（）和removeColumns（）的实现。在实现这些功能时，重要的是要在模型发生之前和之后将有关模型尺寸的更改通知所有连接的视图：
insertRows（）实现必须在将新行插入数据结构之前先调用beginInsertRows（），然后立即调用endInsertRows（）。
insertColumns（）实现必须在将新列插入数据结构之前先调用beginInsertColumns（），然后立即调用endInsertColumns（）。
在将行从数据结构中删除之前，removeRows（）实现必须调用beginRemoveRows（），然后立即调用endRemoveRows（）。
在将列从数据结构中删除之前，removeColumns（）实现必须调用beginRemoveColumns（），然后立即调用endRemoveColumns（）。
**这些函数发出的专用信号使连接的组件有机会在任何数据变得不可用之前采取措施**。使用这些开始和结束功能对插入和删除操作进行封装也使模型能够正确管理持久性模型索引。如果希望正确处理选择，则必须确保调用这些函数。如果您插入或删除带有子项的项目，则无需为子项调用这些函数。换句话说，父项将照顾其子项。
**要创建增量填充的模型，可以重新实现fetchMore（）和canFetchMore（）**。如果重新实现fetchMore（）将行添加到模型，则必须调用beginInsertRows（）和endInsertRows（）。