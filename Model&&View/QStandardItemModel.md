# QStandardItemModel

## 1.Properties

- sortRole : int 

  此属性保留项目角色，该角色用于在对项目进行排序时查询模型的数据
  默认值为Qt :: DisplayRole。

  | Qt Role            | Value | QML Role Name                                           |
  | ------------------ | ----- | ------------------------------------------------------- |
  | Qt::DisplayRole    | 0     | 要以文本形式呈现的关键数据。 （QString）                |
  | Qt::DecorationRole | 1     | 以图标形式呈现为装饰的数据。 （QColor，QIcon或QPixmap） |
  | Qt::EditRole       | 2     | 数据格式适合在编辑器中进行编辑。 （QString）            |
  | Qt::ToolTipRole    | 3     | 数据显示在项目的工具提示中。 （QString）                |
  | Qt::StatusTipRole  | 4     | 状态栏中显示的数据。 （QString）                        |
  | Qt::WhatsThisRole  | 5     | 在“这是什么？”模式下为该项目显示的数据。 （QString）    |
  | Qt::SizeHintRole   | 13    | 将提供给视图的项目的大小提示。 （QSize）                |

## 2.Public Functions

- QStandardItemModel(int rows, int columns, QObject *parent = nullptr)

  构造一个新的项模型，该模型最初具有行，行和列，并且具有给定的父项。

- QStandardItemModel(QObject *parent = nullptr)

- virtual ~QStandardItemModel()

- **`void appendColumn(const QList<QStandardItem *> &items)`**

  追加包含项目的列。 如有必要，将行数增加到项目大小。

- **`void appendRow(const QList<QStandardItem *> &items)`**

  追加包含项目的行。 如有必要，将列数增加到项目大小。

- **`void appendRow(QStandardItem *item)`**

  当构建仅具有一列的列表或树时，此功能提供了一种方便的方法来附加单个新项目。

- **`void clear()`**

  从模型中删除所有项目（包括标题项目），链接行和列数设置为零。

- **`bool clearItemData(const QModelIndex &index)`**

  删除存储在给定索引的所有角色中的数据。 如果索引有效且数据已清除，则返回true，否则返回false。

- QList<QStandardItem *> findItems(const QString &text, Qt::MatchFlags flags = Qt::MatchExactly, int column = 0) const

  在**给定列**中使用给定标志返回与给定文本匹配的项目列表。

- **`QStandardItem *horizontalHeaderItem(int column) const`**

  如果已设置，则返回列的水平标题项目； 否则返回nullptr。

- **`QModelIndex indexFromItem(const QStandardItem *item) const`**

  **返回与给定项目关联的QModelIndex**。不常用
  当您要执行需要该项的QModelIndex的操作时，请使用此函数，例如QAbstractItemView :: scrollTo（）。 **为了方便起见，提供了QStandardItem :: index（）； 它等效于调用此函数**。

- void insertColumn(int column, const QList<QStandardItem *> &items)

  在包含项目的列中插入一列。 如有必要，将行数增加到项目大小。

- bool insertColumn(int column, const QModelIndex &parent = QModelIndex())

  在指定的父项的子项中的给定列之前插入一列。 如果插入了该列，则返回true；否则，返回false。

- void insertRow(int row, const QList<QStandardItem *> &items)

  在包含项目的行中插入一行。 如有必要，将列数增加到项目大小。

- void insertRow(int row, QStandardItem *item)

  在包含item的行中插入一行。
  当构建仅具有一列的列表或树时，此功能提供了一种方便的方法来附加单个新项目。

- bool insertRow(int row, const QModelIndex &parent = QModelIndex())

  在指定的父项的子项中的给定行之前插入一行。 如果插入行，则返回true；否则，返回false。

- QStandardItem *invisibleRootItem() const

  返回模型的不可见根项。
  不可见的根项通过QStandardItem API提供对模型顶级项的访问，从而使得可以编写可以统一方式处理顶级项及其子项的函数； 例如，涉及树模型的递归函数。
  **注意：从此函数检索的QStandardItem对象上调用index（）无效**。

- **`QStandardItem *item(int row, int column = 0) const`**

  返回给定行和列的项目（如果已设置）； 否则返回nullptr。

- QStandardItem *itemFromIndex(const QModelIndex &index) const

  返回指向与给定索引关联的QStandardItem的指针。
  *通常，从视图处理基于QModelIndex的信号（例如QAbstractItemView :: activated（））时，调用此函数是第一步。 在您的插槽中，以信号携带的QModelIndex作为参数调用itemFromIndex（），以获得指向相应QStandardItem的指针*。
  请注意，此函数将懒惰地为索引创建一个项（使用itemPrototype（）），如果该索引处尚无项，则在父项的子表中进行设置。
  如果index是无效索引，则此函数返回nullptr。

- const QStandardItem *itemPrototype() const

  返回模型使用的项目原型。 当需要按需构造新项目时（例如，当视图或项目委托调用setData（）时），该模型会将项目原型用作项目工厂。

- void setColumnCount(int columns)

  将此模型中的列数设置为columns。 如果该值小于columnCount（），则废弃不需要的列中的数据。

- void setRowCount(int rows)

- void setHorizontalHeaderItem(int column, QStandardItem *item)

  将列的水平标题项目设置为item。 模型获取项目的所有权。 如有必要，可增加列数以适合该项目。 前一个标题项（如果有的话）被删除。

- **`void setHorizontalHeaderLabels(const QStringList &labels)`**

  使用标签设置水平标题标签。 如有必要，将列数增加到标签的大小。

- void setVerticalHeaderItem(int row, QStandardItem *item)

- void setVerticalHeaderLabels(const QStringList &labels)

- void setItem(int row, int column, QStandardItem *item)

  将给定行和列的项目设置为item。 模型获取项目的所有权。 如有必要，增加行数和列数以适合该项目。 **给定位置上的上一项（如果有的话）被删除**。

- void setItem(int row, QStandardItem *item)

- void setItemPrototype(const QStandardItem *item)

  将模型的项目原型设置为指定的项目。 该模型拥有原型的所有权。
  依靠QStandardItem :: clone（）函数，项目原型充当QStandardItem工厂。 要提供自己的原型，请子类QStandardItem，重新实现QStandardItem :: clone（）并将该原型设置为自定义类的实例。 每当QStandardItemModel需要按需创建项目时（例如，当视图或项目委托调用setData（）时），新项目将是自定义类的实例。

- void setItemRoleNames(const QHash<int, QByteArray> &roleNames)

  将项目角色名称设置为roleNames。

- void setSortRole(int role)

  设置项目角色，该角色用于在对项目进行排序时查询模型的数据。

- int sortRole() const

- QList<QStandardItem *> takeColumn(int column)

  **在不删除列项目的情况下删除给定的列**，并返回指向已删除项目的指针列表。 该模型**释放项目的所有权**。 对于列中尚未设置的项目，列表中的相应指针将为nullptr。

- QStandardItem *takeHorizontalHeaderItem(int column)

  **从标题中删除列的水平标题项目而不将其删除**，并返回指向该项目的指针。 **模型释放项目的所有权**。

- QStandardItem *takeItem(int row, int column = 0)

  **删除（行，列）处的项目而不删除它。 模型释放项目的所有权**。

- QList<QStandardItem *> takeRow(int row)

- QStandardItem *takeVerticalHeaderItem(int row)

- QStandardItem *verticalHeaderItem(int row) const

## 3.Reimplemented Public Functions

- virtual int columnCount(const QModelIndex &parent = QModelIndex()) const override

- virtual QVariant data(const QModelIndex &index, int role = Qt::DisplayRole) const override

- virtual bool dropMimeData(const QMimeData *data, Qt::DropAction action, int row, int column, const QModelIndex &parent) override

- virtual Qt::ItemFlags flags(const QModelIndex &index) const override

- virtual bool hasChildren(const QModelIndex &parent = QModelIndex()) const override

- virtual QVariant headerData(int section, Qt::Orientation orientation, int role = Qt::DisplayRole) const override

- virtual QModelIndex index(int row, int column, const QModelIndex &parent = QModelIndex()) const override

- virtual bool insertColumns(int column, int count, const QModelIndex &parent = QModelIndex()) override

- virtual bool insertRows(int row, int count, const QModelIndex &parent = QModelIndex()) override

- virtual QMap<int, QVariant> itemData(const QModelIndex &index) const override

- virtual QMimeData *mimeData(const QModelIndexList &indexes) const override

- virtual QStringList mimeTypes() const override

- virtual QModelIndex parent(const QModelIndex &child) const override

- virtual bool removeColumns(int column, int count, const QModelIndex &parent = QModelIndex()) override

- virtual bool removeRows(int row, int count, const QModelIndex &parent = QModelIndex()) override

- virtual int rowCount(const QModelIndex &parent = QModelIndex()) const override

- virtual bool setData(const QModelIndex &index, const QVariant &value, int role = Qt::EditRole) override

- virtual bool setHeaderData(int section, Qt::Orientation orientation, const QVariant &value, int role = Qt::EditRole) override

- virtual bool setItemData(const QModelIndex &index, const QMap<int, QVariant> &roles) override

- **`virtual QModelIndex sibling(int row, int column, const QModelIndex &idx) const override`**

  返回索引处项目的行和列的同级；如果该位置没有同级，则返回无效的QModelIndex。
  sibling（）只是一个便捷函数，它找到项目的父项，并使用它来检索指定行和列中子项的索引。

- virtual void sort(int column, Qt::SortOrder order = Qt::AscendingOrder) override

- virtual Qt::DropActions supportedDropActions() const override

## 4.Signals

- void itemChanged(QStandardItem *item)

  只要项目的数据发生更改，就会发出此信号。

## 5.Detailed Description

QStandardItemModel可**用作标准Qt数据类型的存储库**。它是模型/视图类之一，并且是Qt模型/视图框架的一部分。
QStandardItemModel提供了一种经典的基于项目的方法来处理模型。 **QStandardItemModel中的项目由QStandardItem提供**。
QStandardItemModel实现QAbstractItemModel接口，这意味着该模型可用于在支持该接口的任何视图（例如QListView，QTableView和QTreeView以及您自己的自定义视图）中提供数据。为了提高性能和灵活性，您可能希望子类化QAbstractItemModel来提供对不同种类的数据存储库的支持。例如，QDirModel提供了到基础文件系统的模型接口。
当您需要列表或树时，通常创建一个空的QStandardItemModel并使用**appendRow（）**将项目添加到模型中，并使用item（）访问项目。如果您的模型代表一个表，则通常将表的尺寸传递给QStandardItemModel构造函数，然后使用setItem（）将项目定位到表中。您还可以使用setRowCount（）和setColumnCount（）更改模型的尺寸。要插入项目，请使用insertRow（）或insertColumn（），要删除项目，请使用removeRow（）或removeColumn（）。
您可以**使用setHorizontalHeaderLabels（）和setVerticalHeaderLabels（）设置模型的标题标签**。
您可以使用**findItems（）搜索模型中的项目**，然后通过调用**sort（）对模型进行排序**。
调用clear（）从模型中删除所有项目。