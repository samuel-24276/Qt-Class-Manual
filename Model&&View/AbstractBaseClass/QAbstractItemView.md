# QAbstractItemView

继承关系：`QAbstractItemView`->`QAbstractScrollArea`->`QFrame`->`QWidget`->`QObject and QPaintDevice`

继承者：

- QColumnView
- QHeaderView
- QListView
- QTableView
- QTreeView

## 1.Public Types

- `enum DragDropMode { NoDragDrop, DragOnly, DropOnly, DragDrop, InternalMove }`

  描述视图可以作用的各种拖放事件。 默认情况下，该视图不支持拖放（NoDragDrop）。

  | Constant                        | Value | Description                              |
  | ------------------------------- | ----- | ---------------------------------------- |
  | QAbstractItemView::NoDragDrop   | 0     | 不支持拖放。                             |
  | QAbstractItemView::DragOnly     | 1     | 该视图支持拖动自己的项目                 |
  | QAbstractItemView::DropOnly     | 2     | 视图接受放入项目                         |
  | QAbstractItemView::DragDrop     | 3     | 视图支持拖放                             |
  | QAbstractItemView::InternalMove | 4     | 视图仅从自身接受移动（而不是复制）操作。 |

  

- `enum EditTrigger { NoEditTriggers, CurrentChanged, DoubleClicked, SelectedClicked, EditKeyPressed, …, AllEditTriggers }`

  `flags EditTriggers`

  该枚举描述了将启动项目编辑的操作。

  | Constant                           | Value | Description                          |
  | ---------------------------------- | ----- | ------------------------------------ |
  | QAbstractItemView::NoEditTriggers  | 0     | 无法编辑                             |
  | QAbstractItemView::CurrentChanged  | 1     | 当前项目更改时，编辑就会开始。       |
  | QAbstractItemView::DoubleClicked   | 2     | 项目被双击时编辑开始                 |
  | QAbstractItemView::SelectedClicked | 4     | 单击一个被选中项目时开始编辑         |
  | QAbstractItemView::EditKeyPressed  | 8     | 在项目上按下平台编辑键后，编辑开始。 |
  | QAbstractItemView::AnyKeyPressed   | 16    | 当在项目上按任意键时，编辑开始。     |
  | QAbstractItemView::AllEditTriggers | 31    | 将开始所有上述操作的编辑。           |

  

- `enum ScrollHint { EnsureVisible, PositionAtTop, PositionAtBottom, PositionAtCenter }`

  | Constant                             | Value | Description                  |
  | ------------------------------------ | ----- | ---------------------------- |
  | **QAbstractItemView::EnsureVisible** | 0     | **滚动以确保该项目可见**     |
  | QAbstractItemView::PositionAtTop     | 1     | 滚动以将项目放置在视图的顶部 |
  | QAbstractItemView::PositionAtBottom  | 2     | 滚动以将项目放置在视图的底部 |
  | QAbstractItemView::PositionAtCenter  | 3     | 滚动以将项目放置在视图的中间 |

  

- `enum ScrollMode { ScrollPerItem, ScrollPerPixel }`

  述滚动条的行为。 将滚动模式设置为ScrollPerPixel时，除非使用setSingleStep（）进行了显式设置，否则单步大小将自动调整。 通过将单步大小设置为-1，可以恢复自动调整。

  | Constant                          | Value | Description                    |
  | --------------------------------- | ----- | ------------------------------ |
  | QAbstractItemView::ScrollPerItem  | 0     | 该视图将内容每次滚动一次。     |
  | QAbstractItemView::ScrollPerPixel | 1     | 该视图将内容每次滚动一个像素。 |

  

- `enum SelectionBehavior { SelectItems, SelectRows, SelectColumns }`

  | Constant                         | Value | Description        |
  | -------------------------------- | ----- | ------------------ |
  | QAbstractItemView::SelectItems   | 0     | 只选中当前项目     |
  | QAbstractItemView::SelectRows    | 1     | 选中当前项目所在行 |
  | QAbstractItemView::SelectColumns | 2     | 选中当前项目所在列 |

  

- `enum SelectionMode { SingleSelection, ContiguousSelection, ExtendedSelection, MultiSelection, NoSelection }`

  该枚举指示视图如何响应用户选择：

  | Constant                               | Value | Description                                                  |
  | -------------------------------------- | ----- | ------------------------------------------------------------ |
  | QAbstractItemView::SingleSelection     | 1     | 当用户选择一个项目时，任何已经选择的项目都将变为未选择状态。 用户可以在单击所选项目时通过按Ctrl键取消选择所选项目。 |
  | QAbstractItemView::ContiguousSelection | 4     | 当用户以常规方式选择一个项目时，将清除选择并选择新项目。 但是，如果用户在单击某个项目时按下Shift键，则根据单击项目的状态选择或取消选择当前项目和单击项目之间的所有项目。 |
  | QAbstractItemView::ExtendedSelection   | 3     | 当用户以常规方式选择一个项目时，将清除选择并选择新项目。 但是，如果用户在单击某个项目时按下Ctrl键，则被单击的项目将被切换，而其他所有项目则保持不变。 如果用户在单击某个项目时按下Shift键，则根据该单击项目的状态，选择或取消选择当前项目和单击项目之间的所有项目。 可以通过将鼠标拖动到多个项目上来选择多个项目。 |
  | QAbstractItemView::MultiSelection      | 2     | 当用户以通常的方式选择一个项目时，该项目的选择状态将被切换，而其他项目将被保留。 可以通过在它们上方拖动鼠标来切换多个项目。 |
  | QAbstractItemView::NoSelection         | 0     | 项目不可选中                                                 |

  

## 2.Properties

- **alternatingRowColors : bool**

  此属性保存是否使用交替颜色绘制背景
  如果此属性为true，则将使用QPalette :: Base和QPalette :: AlternateBase绘制项目背景。 否则将使用QPalette :: Base颜色绘制背景。
  默认情况下，此属性为false。

- **autoScroll : bool**

  此属性保存是否在拖动事件中启用了自动滚动
  如果将此属性设置为true（默认值），则当用户在窗口边缘的16个像素内拖动时，QAbstractItemView会自动滚动视图的内容。 如果当前项目更改，则视图将自动滚动以确保当前项目完全可见。
  仅当窗口接受放置时，此属性才起作用。 通过将此属性设置为false可以关闭自动滚动。

- autoScrollMargin : int

  触发自动滚动时，此属性保存区域的大小。
  此属性控制触发自动滚动的窗口边缘区域的大小。 默认值为16像素。

- defaultDropAction : Qt::DropAction

  此属性保存默认在QAbstractItemView :: drag（）中使用的放置动作。
  如果未设置该属性，则当受支持的动作支持CopyAction时，放置动作为CopyAction。

  `enum Qt::DropAction`
  `flags Qt::DropActions`

  | Constant             | Value  | Description                                                  |
  | -------------------- | ------ | ------------------------------------------------------------ |
  | Qt::CopyAction       | 0x1    | 将数据复制到目标                                             |
  | Qt::MoveAction       | 0x2    | 将数据从原位置移动到目标位置                                 |
  | Qt::LinkAction       | 0x4    | 创建一个从源到目标的链接。                                   |
  | Qt::ActionMask       | 0xff   | 无解释                                                       |
  | Qt::IgnoreAction     | 0x0    | 忽略操作（对数据不执行任何操作）。                           |
  | Qt::TargetMoveAction | 0x8002 | 在Windows上，当D＆D数据的所有权应由目标应用程序接管时，即源应用程序不应删除数据时，将使用此值。 在X11上，此值用于移动。 在Mac上不使用TargetMoveAction。 |

  

- dragDropMode : DragDropMode

  此属性保存视图将要执行的拖放事件

- dragDropOverwriteMode : bool

  此属性保存视图的拖放行为
  **如果其值为true，则所选数据在删除时将覆盖现有项目数据，而移动数据将清除该项目**。 如果其值为false，则在删除数据时会将所选数据作为新项插入。 移动数据后，该项目也会被删除。
  **默认值为false**，如QListView和QTreeView子类中一样。 另一方面，在QTableView子类中，该属性已设置为true。
  注意：这并不是要防止项目被覆盖。 模型的flags（）实现应通过不返回Qt :: ItemIsDropEnabled来实现。

- dragEnabled : bool

  此属性保存视图是否支持拖动自己的项目

- editTriggers : EditTriggers

  此属性保存哪些操作将启动项目编辑
  此属性是由EditTrigger定义的标志的选择，并使用OR运算符进行组合。 如果在此属性中设置了执行的动作，则视图将仅启动项目的编辑。

- horizontalScrollMode : ScrollMode

  视图如何在水平方向上滚动其内容
  此属性控制视图如何水平滚动其内容。 滚动可以按像素或按项目进行。 其默认值来自通过QStyle :: SH_ItemView_ScrollMode样式提示的样式。

- iconSize : QSize

  此属性保存项目图标的大小
  在视图可见时设置此属性将导致重新布置项目。

- selectionBehavior : SelectionBehavior

  此属性保存视图使用的选择行为
  此属性保存选择是根据单个项目，行还是列进行的。

- selectionMode : SelectionMode

  此属性保存视图在哪种选择模式下运行
  此属性控制用户是否可以选择一个或多个项目，并且在多个项目选择中控制选择是否必须是连续范围的项目。

- **showDropIndicator : bool**

  **此属性保存在拖放项目时是否显示放置指示器。**

- tabKeyNavigation : bool

  此属性保存是否启用了带有tab和backtab的项目导航。

- textElideMode : Qt::TextElideMode

  此属性在省略文本中保留“ ...”的位置。
  所有项目视图的默认值为Qt :: ElideRight。

- verticalScrollMode : ScrollMode

  视图如何在垂直方向上滚动其内容
  此属性控制视图如何垂直滚动其内容。 滚动可以按像素或按项目进行。 其默认值来自通过QStyle :: SH_ItemView_ScrollMode样式提示的样式。

## 3.Public Functions

- QAbstractItemView(QWidget *parent = nullptr)

- virtual ~QAbstractItemView()

- `bool alternatingRowColors() const`

- `int autoScrollMargin() const`

- `void closePersistentEditor(const QModelIndex &index)`

  关闭给定索引处的项目的持久性编辑器。

- `QModelIndex currentIndex() const`

  返回项目所在的索引地址。

- `Qt::DropAction defaultDropAction() const`

  此属性保存默认在QAbstractItemView :: drag（）中使用的放置动作。
  如果未设置该属性，则当受支持的动作支持CopyAction时，放置动作为CopyAction。

- `QAbstractItemView::DragDropMode dragDropMode() const`

  此属性保存视图将要执行的拖放事件

- `bool dragDropOverwriteMode() const`

- `bool dragEnabled() const`

  此属性保存视图是否支持拖动自己的项目

- `QAbstractItemView::EditTriggers editTriggers() const`

- **`bool hasAutoScroll() const`**

  此属性保存是否在拖动事件中启用了自动滚动
  如果将此属性设置为true（默认值），则当用户在视口边缘的16个像素内拖动时，QAbstractItemView会自动滚动视图的内容。 如果当前项目更改，则视图将自动滚动以确保当前项目完全可见。
  仅当视图接受放置时，此属性才起作用。 通过将此属性设置为false可以关闭自动滚动。

- `QAbstractItemView::ScrollMode horizontalScrollMode() const`

- `QSize iconSize() const`

- **`virtual QModelIndex indexAt(const QPoint &point) const = 0`**

  **返回项目在视图坐标点的模型索引。**
  **在基类中，这是一个纯虚函数。**

- `QWidget * indexWidget(const QModelIndex &index) const`

  返回给定索引处项目的小部件。

- `bool isPersistentEditorOpen(const QModelIndex &index) const`

  返回是否为索引index处的项目打开了持久性编辑器。

- **`QAbstractItemDelegate * itemDelegate() const`**

  返回此视图和模型使用的项目委托。 这是使用setItemDelegate（）设置的一组，或者是默认的一组。

- `QAbstractItemDelegate* itemDelegate(const QModelIndex &index) const`

  返回此视图和模型为给定索引使用的项目委托。

- `QAbstractItemDelegate* itemDelegateForColumn(int column) const`

  返回此视图和模型为给定列使用的项目委托。 您可以调用itemDelegate（）以获得指向给定索引的当前委托的指针。

- `QAbstractItemDelegate *itemDelegateForRow(int row) const`

  返回此视图和模型为给定行使用的项目委托。 您可以调用itemDelegate（）以获得指向给定索引的当前委托的指针。

- `virtual void keyboardSearch(const QString &search)`

  移至并选择与字符串搜索最匹配的项目。 如果未找到任何项目，则不会发生任何事情。
  在默认实现中，如果搜索为空，或者自上次搜索以来的时间间隔超过QApplication :: keyboardInputInterval（），将重置搜索。

- `QAbstractItemModel *model() const`

  返回此视图显示的模型。

- `void openPersistentEditor(const QModelIndex &index)`

  在给定索引的项目上打开持久性编辑器。 如果不存在任何编辑器，则委托将创建一个新的编辑器。

- `void resetHorizontalScrollMode()`

  重置视图在水平方向上滚动内容的方式

- `void resetVerticalScrollMode()`

  重置视图在垂直方向上滚动内容的方式

- **`QModelIndex rootIndex() const`**

  **返回模型根项的模型索引。 根项目是视图顶级项目的父项目。 根可能无效。**

- `virtual void scrollTo(const QModelIndex &index, QAbstractItemView::ScrollHint hint = EnsureVisible) = 0`

  如有必要，滚动视图以确保索引处的项目可见。 视图将尝试根据给定的提示定位项目。
  在基类中，这是一个纯虚函数。

- `QAbstractItemView::SelectionBehavior selectionBehavior() const`

- `QAbstractItemView::SelectionMode selectionMode() const`

- `QItemSelectionModel *selectionModel() const`

  返回当前选中的模型

- **`void setAlternatingRowColors(bool enable)`**

  设置是否使用交替颜色绘制背景
  如果参数为true，则将使用QPalette :: Base和QPalette :: AlternateBase绘制项目背景。 否则将使用QPalette :: Base颜色绘制背景。

- **`void setAutoScroll(bool enable)`**

  设置是否在拖动事件中启用了自动滚动
  如果参数为true（默认值），则当用户在视口边缘的16个像素内拖动时，QAbstractItemView会自动滚动视图的内容。 如果当前项目更改，则视图将自动滚动以确保当前项目完全可见。

- `void setAutoScrollMargin(int margin)`

- `void setDefaultDropAction(Qt::DropAction dropAction)`

- `void setDragDropMode(QAbstractItemView::DragDropMode behavior)`

- `void setDragDropOverwriteMode(bool overwrite)`

- `void setDragEnabled(bool enable)`

- `void setDropIndicatorShown(bool enable)`

- `void setEditTriggers(QAbstractItemView::EditTriggers triggers)`

- `void setHorizontalScrollMode(QAbstractItemView::ScrollMode mode)`

- `void setIconSize(const QSize &size)`

- `void setIndexWidget(const QModelIndex &index, QWidget *widget)`

- **`void setItemDelegate(QAbstractItemDelegate *delegate)`**

  设置该视图的项目委托及其要委托的模型。 如果要完全控制项目的编辑和显示，这将很有用。
  任何现有的委托将被移除(removed)，但不会被删除(deleted)。 QAbstractItemView不获取委托的所有权。
  **警告：您不应在视图之间共享委托的相同实例**。 这样做可能会导致错误或不直观的编辑行为，因为连接到给定委托的每个视图都可能会收到closeEditor（）信号，并尝试访问，修改或关闭已经关闭的编辑器。

- `void setItemDelegateForColumn(int column, QAbstractItemDelegate *delegate)`

  设置此视图和模型为给定列使用的给定项目委托。 列上的所有项目都将由委托绘制和管理，而不是使用默认委托（即itemDelegate（））。
  列的所有现有列委托将被移除(removed)，但不会被删除(deleted)。 QAbstractItemView不获取委托的所有权。
  **注意**：如果已将委托分配给行和列，则行委托将具有优先权并管理相交的单元格索引。
  **警告**：您不应在视图之间共享委托的相同实例。 这样做可能会导致错误或不直观的编辑行为，因为连接到给定委托的每个视图都可能会收到closeEditor（）信号，并尝试访问，修改或关闭已经关闭的编辑器。

- `void setItemDelegateForRow(int row, QAbstractItemDelegate *delegate)`

  设置此视图和模型为给定行使用的给定项目委托。 行上的所有项目都将由委托绘制和管理，而不是使用默认委托（即itemDelegate（））。
  该行的任何现有行委托将被移除(removed)，但不会被删除(deleted)。 QAbstractItemView不获取委托的所有权。
  注意：如果已将委托分配给行和列，则行委托（即此委托）将具有优先权并管理相交的单元格索引。
  警告：您不应在视图之间共享委托的相同实例。 这样做可能会导致错误或不直观的编辑行为，因为连接到给定委托的每个视图都可能会收到closeEditor（）信号，并尝试访问，修改或关闭已经关闭的编辑器。

- `virtual void setModel(QAbstractItemModel *model)`

  设置要显示的视图的模型。
  此函数将创建并设置一个新的选择模型，用setSelectionModel（）替换以前设置的任何模型。 但是，旧的选择模型不会被删除，因为它可能在多个视图之间共享。 如果不再需要旧的选择模型，我们建议您删除它。 这是通过以下代码完成的：

  ```c++
  QItemSelectionModel *m = view->selectionModel();
  view->setModel(new model);
  delete m;
  ```

  如果旧模型 和 旧选择模型都没有父对象，或者它们的父对象是寿命很长的对象，则最好调用它们的**deleteLater（）**函数以显式删除它们。
  **除非视图是模型的父对象，否则视图不会获得模型的所有权，因为该模型可能在许多不同的视图之间共享**。

- `void setSelectionBehavior(QAbstractItemView::SelectionBehavior behavior)`

- `void setSelectionMode(QAbstractItemView::SelectionMode mode)`

- `virtual void setSelectionModel(QItemSelectionModel *selectionModel)`

- `void setTabKeyNavigation(bool enable)`

  设置是否启用了带有tab和backtab的项目导航。

- `void setTextElideMode(Qt::TextElideMode mode)`

- `void setVerticalScrollMode(QAbstractItemView::ScrollMode mode)`

  设置视图在垂直方向上的滚动策略

- `bool showDropIndicator() const`

  设置在拖放项目时是否显示放置指示器。

- **`virtual int sizeHintForColumn(int column) const`**

  返回指定列的宽度大小提示；如果没有模型，则返回-1。
  在具有水平标题的视图中使用此函数可根据给定列的内容查找标题部分的大小提示。

- **`QSize sizeHintForIndex(const QModelIndex &index) const`**

  返回具有指定索引的项目的大小提示，或者为无效索引返回无效的大小。

- **`virtual int sizeHintForRow(int row) const`**

  返回指定行的高度大小提示；如果没有模型，则返回-1。
  返回的高度是使用给定行的项目的大小提示来计算的，即返回的值是项目之间的最大高度。 请注意，要控制行的高度，必须重新实现QAbstractItemDelegate :: sizeHint（）函数。
  在具有垂直标题的视图中使用此函数可根据给定行的内容查找标题部分的大小提示。

- `bool tabKeyNavigation() const`

- `Qt::TextElideMode textElideMode() const`

- `QAbstractItemView::ScrollMode verticalScrollMode() const`

- `virtual QRect visualRect(const QModelIndex &index) const = 0`

  返回该项目在索引处占据的视口上的矩形。
  如果您的项目显示在多个区域中，则visualRect应该返回包含索引的主要区域，而不是索引可能包含，触摸或引起绘图的整个区域。
  在基类中，这是一个纯虚函数。

## 4.Reimplemented Public Functions

`virtual QVariant inputMethodQuery(Qt::InputMethodQuery query) const override`

## 5.Public Slots

- `void clearSelection()`

  取消选择所有选定的项目。 当前索引不会更改。

- `void edit(const QModelIndex &index)`

  如果可编辑，则开始编辑与给定索引相对应的项目。
  请注意，此功能不会更改当前索引。 由于当前索引定义了要编辑的下一个和上一个项目，因此用户可能会发现键盘导航无法正常工作。 **为了提供一致的导航行为，请在此函数之前使用相同的模型索引调用setCurrentIndex（）**。

- `virtual void reset()`

  重置视图的内部状态。
  **警告**：此功能将重置打开的编辑器，滚动条位置，选择等。将**不提交现有更改**。 如果您想在重置视图时保存更改，则可以重新实现此函数，提交更改，然后调用超类的实现。

- `void scrollToBottom()`

  将视图滚动到底部。

- `void scrollToTop()`

  将视图滚动到顶部。

- `virtual void selectAll()`

  选择视图中的所有项目。 选择时，此功能将使用在视图上设置的选择行为。

- **void setCurrentIndex(const QModelIndex &index)**

  将当前项目设置为索引处的项目。
  除非当前选择模式为NoSelection，否则也将选择该项目。 请注意，此功能还会更新用户执行的任何新选择的起始位置。
  要将一个项目设置为当前项目而不选择它，请调用
  `selectionModel（）-> setCurrentIndex（index，QItemSelectionModel :: NoUpdate）;`

- `virtual void setRootIndex(const QModelIndex &index)`

  将根项目设置为给定索引处的项目。

- `void update(const QModelIndex &index)`

  更新给定索引占用的区域。

## 6.Signals

- `void activated(const QModelIndex &index)`

  用户激活索引指定的项目时，将发出此信号。 如何激活物品取决于平台。 例如，通过双击或双击该项目，或在该项目为当前状态时按Return或Enter键。

- `void clicked(const QModelIndex &index)`

  左键单击鼠标时发出此信号。 鼠标单击的项目由索引指定。 仅在索引有效时才发出信号。

- `void doubleClicked(const QModelIndex &index)`

  双击鼠标按钮时，将发出此信号。 鼠标双击的项目由索引指定。 仅在索引有效时才发出信号。

- `void entered(const QModelIndex &index)`

  当鼠标光标进入由index指定的项目时，将发出此信号。 **要启用此功能，需要启用鼠标跟踪**。

- `void iconSizeChanged(const QSize &size)`

  

- `void pressed(const QModelIndex &index)`

  按下鼠标按钮时会发出此信号。 鼠标指定的项目由索引指定。 仅在索引有效时才发出信号。
  使用QGuiApplication :: mouseButtons（）函数获取鼠标按钮的状态。

- `void viewportEntered()`

  当鼠标光标进入视图时，将发出此信号。 **要启用此功能，需要启用鼠标跟踪**。

## 7.Protected Types

- `enum CursorAction { MoveUp, MoveDown, MoveLeft, MoveRight, MoveHome, …, MovePrevious }`

  该枚举描述了在项目之间导航的不同方法

  | Constant                        | Value | Description                  |
  | ------------------------------- | ----- | ---------------------------- |
  | QAbstractItemView::MoveUp       | 0     | 移至当前项目上方的项目。     |
  | QAbstractItemView::MoveDown     | 1     | 移至当前项目下方的项目。     |
  | QAbstractItemView::MoveLeft     | 2     | 移至当前项目左边的项目。     |
  | QAbstractItemView::MoveRight    | 3     | 移至当前项目右边的项目。     |
  | QAbstractItemView::MoveHome     | 4     | 移至左上角的项目。           |
  | QAbstractItemView::MoveEnd      | 5     | 移至右下角的项目。           |
  | QAbstractItemView::MovePageUp   | 6     | 在当前项目上方向上移动一页。 |
  | QAbstractItemView::MovePageDown | 7     | 在当前项目下移一页。         |
  | QAbstractItemView::MoveNext     | 8     | 移至当前项目之后的项目。     |
  | QAbstractItemView::MovePrevious | 9     | 移至当前项目之前的项目。     |

  

- `enum DropIndicatorPosition { OnItem, AboveItem, BelowItem, OnViewport }`

  该枚举指示放置指示器相对于当前鼠标位置处的索引的位置：

  | Constant                      | Value | Description                                                  |
  | ----------------------------- | ----- | ------------------------------------------------------------ |
  | QAbstractItemView::OnItem     | 0     | 该项目将被放置在索引上。                                     |
  | QAbstractItemView::AboveItem  | 1     | 该项目将被放置在索引上方。                                   |
  | QAbstractItemView::BelowItem  | 2     | 该项目将被放置在索引下方。                                   |
  | QAbstractItemView::OnViewport | 3     | 该项目将被放到没有任何项目的视图区域。 每个视图处理放置到视图上的项目的方式取决于所使用的基础模型的行为。 |

  

- `enum State { NoState, DraggingState, DragSelectingState, EditingState, ExpandingState, …, AnimatingState }`

  描述视图可以处于的不同状态。通常只有重新实现自己的视图时，这才是有趣的。

  | Constant                              | Value | Description                      |
  | ------------------------------------- | ----- | -------------------------------- |
  | QAbstractItemView::NoState            | 0     | 默认状态                         |
  | QAbstractItemView::DraggingState      | 1     | 用户正在拖动项目。               |
  | QAbstractItemView::DragSelectingState | 2     | 用户正在选择项目。               |
  | QAbstractItemView::EditingState       | 3     | 用户正在小部件编辑器中编辑项目。 |
  | QAbstractItemView::ExpandingState     | 4     | 用户正在打开项目的分支。         |
  | QAbstractItemView::CollapsingState    | 5     | 用户正在关闭项目的分支。         |
  | QAbstractItemView::AnimatingState     | 6     | 项目视图正在执行动画。           |

  

## 8.Protected Functions

- `QPoint dirtyRegionOffset() const`
- `QAbstractItemView::DropIndicatorPosition dropIndicatorPosition() const`
- `virtual bool edit(const QModelIndex &index, QAbstractItemView::EditTrigger trigger, QEvent *event)`
- `void executeDelayedItemsLayout()`
- `virtual int horizontalOffset() const = 0`
- `virtual bool isIndexHidden(const QModelIndex &index) const = 0`
- `virtual QModelIndex moveCursor(QAbstractItemView::CursorAction cursorAction, Qt::KeyboardModifiers modifiers) = 0`
- `void scheduleDelayedItemsLayout()`
- `void scrollDirtyRegion(int dx, int dy)`
- `virtual QModelIndexList selectedIndexes() const`
- `virtual QItemSelectionModel::SelectionFlags selectionCommand(const QModelIndex &index, const QEvent *event = nullptr) const`
- `void setDirtyRegion(const QRegion &region)`
- `virtual void setSelection(const QRect &rect, QItemSelectionModel::SelectionFlags flags) = 0`
- `void setState(QAbstractItemView::State state)`
- `virtual void startDrag(Qt::DropActions supportedActions)`
- `QAbstractItemView::State state() const`
- `virtual int verticalOffset() const = 0`
- `virtual QStyleOptionViewItem viewOptions() const`
- `virtual QRegion visualRegionForSelection(const QItemSelection &selection) const = 0`

## 9.Reimplemented Protected Functions

- `virtual void dragEnterEvent(QDragEnterEvent *event) override`
- `virtual void dragLeaveEvent(QDragLeaveEvent *event) override`
- `virtual void dragMoveEvent(QDragMoveEvent *event) override`
- `virtual void dropEvent(QDropEvent *event) override`
- `virtual bool event(QEvent *event) override`
- `virtual bool eventFilter(QObject *object, QEvent *event) override`
- `virtual void focusInEvent(QFocusEvent *event) override`
- `virtual bool focusNextPrevChild(bool next) override`
- `virtual void focusOutEvent(QFocusEvent *event) override`
- `virtual void inputMethodEvent(QInputMethodEvent *event) override`
- `virtual void keyPressEvent(QKeyEvent *event) override`
- `virtual void mouseDoubleClickEvent(QMouseEvent *event) override`
- `virtual void mouseMoveEvent(QMouseEvent *event) override`
- `virtual void mousePressEvent(QMouseEvent *event) override`
- `virtual void mouseReleaseEvent(QMouseEvent *event) override`
- `virtual void resizeEvent(QResizeEvent *event) override`
- `virtual void timerEvent(QTimerEvent *event) override`
- `virtual bool viewportEvent(QEvent *event) override`
- `virtual QSize viewportSizeHint() const override`

## 10.Protected Slots

- `virtual void closeEditor(QWidget *editor, QAbstractItemDelegate::EndEditHint hint)`

  关闭给定的编辑器，然后释放它。 **提示用于指定视图应如何响应编辑操作的结束**。 例如，提示可能指示应打开视图中的下一项进行编辑。

- `virtual void commitData(QWidget *editor)`

  将编辑器中的数据提交给模型。

- `virtual void currentChanged(const QModelIndex &current, const QModelIndex &previous)`

  当新项目成为当前项目时，将调用此插槽。 上一个当前项目由上一个索引指定，新项目由当前索引指定。

- `virtual void dataChanged(const QModelIndex &topLeft, const QModelIndex &bottomRight, const QVector<int> &roles = QVector<int>())`

  当具有给定角色的项目在模型中更改时，将调用此插槽。 更改的项目是从topLeft到bottomRight（含）的项目。 如果只更改一项，则topLeft == bottomRight。
  更改的角色可以是一个空容器（意味着所有内容都已更改），也可以是一个带有角色子集已更改的非空容器。
  注意：在Qt提供的视图中，dataChanged（）不支持Qt :: ToolTipRole。

- `virtual void editorDestroyed(QObject *editor)`

  给定的编辑器已销毁时，将调用此函数。

- `virtual void rowsAboutToBeRemoved(const QModelIndex &parent, int start, int end)`

  **当要删除行时，将调用此插槽。 删除的行是给定父项下从头到尾的所有行**。

- `virtual void rowsInserted(const QModelIndex &parent, int start, int end)`

  **插入行时将调用此插槽。 新行是给定父项下从头到尾的所有行。 基类实现在模型上调用fetchMore（）以检查更多数据**。

- `virtual void selectionChanged(const QItemSelection &selected, const QItemSelection &deselected)`

  更改选择时将调用此插槽。 通过取消选择指定先前的选择（可能为空），通过选择指定新的选择。

- `virtual void updateGeometries()`

  更新视图的子小部件的几何（位置）。

## 11.Detailed Description

QAbstractItemView类是使用QAbstractItemModel的每个标准视图的基类。 **QAbstractItemView是一个抽象类，本身无法实例化**。 它提供了一个标准接口，可通过信号和插槽机制与模型进行互操作，从而使子类能够随着模型的更改而保持最新。此类为键盘和鼠标导航，视图滚动，项目编辑和选择提供标准支持。 **键盘导航实现了以下功能：**

| Keys              | Functionality                                       |
| ----------------- | --------------------------------------------------- |
| Arrow keys方向键  | 更改并选择当前项目。                                |
| Ctrl+Arrow keys   | 更改当前项目，但不选择它。                          |
| Shift+Arrow keys  | 更改并选择当前项目。 **未取消选择先前选择的项目。** |
| Ctr+Space         | 切换当前项目的选择。                                |
| Tab/Backtab       | 将当前项目更改为下一个/上一个项目。                 |
| Home/End          | 选择模型中的第一项/最后一项。                       |
| Page up/Page down | 按视图中可见行的数量上下滚动显示的行。              |
| Ctrl+A            | 选择模型中的所有项目。                              |

