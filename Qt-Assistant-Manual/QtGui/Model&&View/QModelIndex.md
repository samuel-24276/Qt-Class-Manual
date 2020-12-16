# QModelIndex

# 1.Public Functions

- `QModelIndex()`

  创建一个新的空模型索引。 这种类型的模型索引用于指示模型中的位置无效。

- `int column() const`

  返回此模型索引引用的列。

- `int row() const`

  返回此模型索引引用的行。****

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

