# QItemSelectionModel

继承关系：`QItemSelectionModel`->`QObject`

一个用于跟踪视图组件的单元格选择状态的类，当在QTableView选择某个单元格，或多个单元格时，通过QItemSelectionModel可以获得选中的单元格的模型索引，为单元格的选择操作提供方便。

## 1.Public Types

- enum SelectionFlag { NoUpdate, Clear, Select, Deselect, Toggle, …, ClearAndSelect }

  flags SelectionFlags

  该枚举描述了选择模型的更新方式。

  | Constant                                  | Value             | Description                                          |
  | ----------------------------------------- | ----------------- | ---------------------------------------------------- |
  | QItemSelectionModel::NoUpdate             | 0x0000            | 没有选择。                                           |
  | QItemSelectionModel::Clear                | 0x0001            | 完整的选择将被清除。                                 |
  | QItemSelectionModel::Select               | 0x0002            | 将选择所有指定的索引。                               |
  | QItemSelectionModel::Deselect             | 0x0004            | 所有指定的索引将被取消选择。                         |
  | **`QItemSelectionModel::Toggle`**         | 0x0008            | **所有指定的索引将根据其当前状态被选择或取消选择**。 |
  | **`QItemSelectionModel::Current`**        | 0x0010            | **当前选择将被更新**。                               |
  | QItemSelectionModel::Rows                 | 0x0020            | 所有索引将扩展为跨行。                               |
  | QItemSelectionModel::Columns              | 0x0040            | 所有索引将扩展为列。                                 |
  | **`QItemSelectionModel::SelectCurrent`**  | Select \| Current | Select和Current的组合，为方便起见                    |
  | **`QItemSelectionModel::ToggleCurrent`**  | Toggle \| Current | Toggle和Current的组合，为方便起见                    |
  | **`QItemSelectionModel::ClearAndSelect`** | Clear \| Current  | Clear和Current的组合，为方便起见                     |

  

## 2.Properties

- selectedIndexes : const QModelIndexList 

## 3.Public Functions

- QItemSelectionModel(QAbstractItemModel *model, QObject *parent)

- QItemSelectionModel(QAbstractItemModel *model = nullptr)

- virtual ~QItemSelectionModel()

- `bool columnIntersectsSelection(int column, const QModelIndex &parent = QModelIndex()) const`

  如果在具有给定父项的列中选择了任何项，则返回true。
  注意：从Qt 5.15开始，parent的默认参数是一个空的模型索引。

- QModelIndex currentIndex() const

  返回当前项目的模型项目索引，如果没有当前项目，则返回无效索引。

- bool hasSelection() const

  如果选择模型包含任何选择范围，则返回true； 否则返回false。

- bool isColumnSelected(int column, const QModelIndex &parent = QModelIndex()) const

  如果在具有给定父项的列中选择了所有项，则返回true。
  请注意，此函数通常比在同一列中的所有项目上调用isSelected（）更快，并且忽略了不可选择的项目。
  注意：从Qt 5.15开始，parent的默认参数是一个空的模型索引。
  注意：可以通过元对象系统和QML调用此函数。 请参阅Q_INVOKABLE。

- bool isRowSelected(int row, const QModelIndex &parent = QModelIndex()) const

- bool isSelected(const QModelIndex &index) const

  如果选择了给定的模型项索引，则返回true。
  注意：可以通过元对象系统和QML调用此函数。 请参阅Q_INVOKABLE。

- const QAbstractItemModel *model() const

  返回选择模型所操作的项目模型。

- QAbstractItemModel *model()

  返回选择模型所操作的项目模型。

- bool rowIntersectsSelection(int row, const QModelIndex &parent = QModelIndex()) const

  如果在具有给定父项的行中选择了任何项，则返回true。
  注意：从Qt 5.15开始，parent的默认参数是一个空的模型索引。
  注意：可以通过元对象系统和QML调用此函数。 请参阅Q_INVOKABLE。

- QModelIndexList selectedColumns(int row = 0) const

  返回给定行中所有行均被选中的列的索引。
  注意：可以通过元对象系统和QML调用此函数。 请参阅Q_INVOKABLE。

- QModelIndexList selectedIndexes() const

  返回所有选定模型项索引的列表。 该列表不包含重复项，也不进行排序。
  注意：属性selectedIndexes的Getter函数。

- QModelIndexList selectedRows(int column = 0) const

- const QItemSelection selection() const

  返回存储在选择模型中的选择范围。

- void setModel(QAbstractItemModel *model)

  设置要建模的模型。 将发出modelChanged（）信号。

## 4.Public Slots

- virtual void clear()

  清除选择模型。 发出selectionChanged（）和currentChanged（）。

- virtual void clearCurrentIndex()

  清除当前索引。 发出currentChanged（）。

- void clearSelection()

  清除选择模型中的选择。 发出selectionChanged（）。

- **virtual void reset()**

  **清除选择模型。 不发出任何信号**。

- virtual void select(const QItemSelection &selection, 

  QItemSelectionModel::SelectionFlags command)

  使用指定的命令选择项目选择，并发出selectionChanged（）。

- virtual void select(const QModelIndex &index, QItemSelectionModel::SelectionFlags command)

  使用指定的命令选择模型项索引，并发出selectionChanged（）。

- virtual void setCurrentIndex(const QModelIndex &index, QItemSelectionModel::SelectionFlags command)

  将模型项索引设置为当前项，并发出currentChanged（）。 当前项目用于键盘导航和焦点指示。 它独立于任何选定项目，尽管选定项目也可以是当前项目。
  根据指定的命令，索引也可以成为当前选择的一部分。

## 5.Signals

- void currentChanged(const QModelIndex &current, const QModelIndex &previous)

- void currentColumnChanged(const QModelIndex &current, const QModelIndex &previous)

- void currentRowChanged(const QModelIndex &current, const QModelIndex &previous)

- **`void modelChanged(QAbstractItemModel *model)`**

  使用setModel（）成功设置模型后，将发出此信号。

- void selectionChanged(const QItemSelection &selected, const QItemSelection &deselected)

## 6.Protected Functions

- void emitSelectionChanged(const QItemSelection &newSelection, const QItemSelection &oldSelection)

## 7.Detailed Description

QItemSelectionModel可以在一个视图或同一模型的多个视图中跟踪选定的项目。它还在视图中跟踪当前选定的项目。
QItemSelectionModel类是Model / View类之一，并且是Qt模型/视图框架的一部分。
所选项目使用范围存储。每当您要修改选定的项目时，请使用select（）并提供QItemSelection或QModelIndex和QItemSelectionModel :: SelectionFlag。
QItemSelectionModel采用两层方法进行选择管理，既处理已提交的选定项目，又处理当前选择中的项目。当前选择的项目是当前交互式选择的一部分（例如，使用橡皮筋选择或键盘移位选择）。
要更新当前选择的项目，请使用QItemSelectionModel :: Current和其他任何SelectionFlags的按位或。如果省略QItemSelectionModel :: Current命令，将创建一个新的当前选择，并将先前的选择添加到整个选择中。所有功能都在两层上运行。例如，selecteditems（）将从两层返回项目。
注意：从5.5开始，model，hasSelection和currentIndex是元对象属性。