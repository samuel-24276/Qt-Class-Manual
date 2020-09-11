# QAbstractItemModel

继承关系：`QAbstractItemModel`->`QObject`

继承者：

- QAbstractListModel
- QAbstractProxyModel 
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



# QModelIndex

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