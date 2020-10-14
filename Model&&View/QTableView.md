# QTableView

继承关系：`QTableView`->`QAbstractItemView`->`QAbstractScrollArea`->`QFrame`->`QWidget`

## 1.Properties

- cornerButtonEnabled : bool

  此属性保存是否启用左上角的按钮
  如果此属性为true，则启用表视图左上角的按钮。 单击此按钮将选择表视图中的所有单元格。默认情况下，此属性为true。

- gridStyle : Qt::PenStyle

  此属性保存用于绘制网格的笔样式。

- showGrid : bool

  此属性保存是否显示网格
  如果此属性为true，则为表格绘制一个网格； 如果该属性为false，则不绘制网格。 默认值是true。

- sortingEnabled : bool

  此属性保存是否启用排序
  如果此属性为true，则为表启用排序。 如果此属性为false，则不启用排序。 默认值为false。
  注意：使用setSortingEnabled（）将属性设置为true会立即触发对具有当前排序部分和顺序的sortByColumn（）的调用。

- wordWrap : bool

  此属性包含项文本换词策略。
  如果此属性为true，则在断字时将项目文本包装在必要的位置； 否则，它根本不会被包装。 默认情况下，此属性为true。
  请注意，即使启用了自动换行，该单元也不会扩展为适合所有文本。 将根据当前的textElideMode插入省略号。

## 2.Public Functions

- QTableView(QWidget *parent = nullptr)

- virtual ~QTableView()

- void clearSpans()

  删除表视图中的所有行和列跨度。

- int columnAt(int x) const

  返回以内容坐标表示的给定x坐标x所在的列。
  注意：如果给定的坐标无效（无列），此函数将返回-1。

- int columnSpan(int row, int column) const

  返回表格元素在（行，列）处的列跨度。 预设为1

- int columnViewportPosition(int column) const

  返回给定列的内容坐标中的x坐标。

- int columnWidth(int column) const

  返回给定列的宽度。

- **Qt::PenStyle gridStyle() const**

  此属性保存用于绘制网格的笔样式。

  | Constant           | Value | Description                                                  |
  | ------------------ | ----- | ------------------------------------------------------------ |
  | Qt::NoPen          | 0     | 完全没有线。 例如，QPainter :: drawRect（）填充但不绘制任何边界线。 |
  | Qt::SolidLine      | 1     | 一条简单的线。                                               |
  | Qt::DashLine       | 2     | 虚线隔开几个像素。                                           |
  | Qt::DotLine        | 3     | 点分开几个像素。                                             |
  | Qt::DashDotLine    | 4     | 交替的点和破折号。                                           |
  | Qt::DashDotDotLine | 5     | 一个破折号，两个点，一个破折号，两个点。                     |
  | Qt::CustomDashLine | 6     | 使用QPainterPathStroker :: setDashPattern（）定义的自定义模式 |

  

- QHeaderView *horizontalHeader() const

  返回表格视图的水平标题。

- QHeaderView *verticalHeader() const

  返回表格视图的垂直标题。

- **void setHorizontalHeader(QHeaderView *header)**

  **将用于水平标题的窗口小部件设置为header。**

- **void setVerticalHeader(QHeaderView *header)**

  **将用于垂直标题的窗口小部件设置为header。**

- bool isColumnHidden(int column) const

  如果给定的列是隐藏的，则返回true； 否则返回false。

- void setColumnHidden(int column, bool hide)

  如果hide为true，则给定的列将被隐藏；否则为false，将显示。

- void setColumnWidth(int column, int width)

  将给定列的宽度设置为width。

- int rowAt(int y) const

  返回内容坐标中给定y坐标y所在的行。
  注意：如果给定的坐标无效（无行），则此函数返回-1。

- int rowHeight(int row) const

  返回给定行的高度。

- int rowSpan(int row, int column) const

  返回表格元素在（行，列）处的行跨度。 预设值为1。

- int rowViewportPosition(int row) const

  返回给定行的内容坐标中的y坐标。

- bool isRowHidden(int row) const

  如果给定的行的，则返回true； 否则返回false。

- void setRowHeight(int row, int height)

  将给定行的高度设置为height。

- void setRowHidden(int row, bool hide)

  如果hide为true，则给定的行将被隐藏；否则为false，将显示。

- bool isCornerButtonEnabled() const

  返回左上角的全选按钮是否启用，若启用返回true，否则返回false。

- bool isSortingEnabled() const

- void setCornerButtonEnabled(bool enable)

- void setGridStyle(Qt::PenStyle style)

- void setSortingEnabled(bool enable)

- void setSpan(int row, int column, int rowSpanCount, int columnSpanCount)

- void setWordWrap(bool on)

- bool showGrid() const

  此属性保存是否显示网格
  如果此属性为true，则为表格绘制一个网格； 如果该属性为false，则不绘制网格。 默认值是true。

- bool wordWrap() const

  此属性包含项文本换词策略
  如果此属性为true，则在断字时将项目文本包装在必要的位置； 否则，它根本不会被包裹。 默认情况下，此属性为true。
  请注意，即使启用了自动换行，该单元也不会扩展为适合所有文本。 省略号将根据当前的textElideMode插入。

## 3.Reimplemented Public Functions

- virtual QModelIndex indexAt(const QPoint &pos) const override

  返回与表项相对应的模型项在内容坐标中位置pos的索引位置。

- virtual void setModel(QAbstractItemModel *model) override

- virtual void setRootIndex(const QModelIndex &index) override

- virtual void setSelectionModel(QItemSelectionModel *selectionModel) override

## 4.Public Slots

- void hideColumn(int column)

  隐藏给定的列。

- void hideRow(int row)

- void resizeColumnToContents(int column)

  根据用于呈现列中每个项目的委托的大小提示来调整给定列的大小。
  注意：仅可见列将被调整大小。 重新实现sizeHintForColumn（）也可以调整隐藏列的大小。

- void resizeColumnsToContents()

  根据用于呈现列中每个项目的委托的大小提示来调整所有列的大小。

- void resizeRowToContents(int row)

- void resizeRowsToContents()

- void selectColumn(int column)

  如果当前的**SelectionMode**和**SelectionBehavior**（可在QAbstractItemView找到）允许选择列，则在表视图中选择给定的列。

- void selectRow(int row)

- void setShowGrid(bool show)

- void showColumn(int column)

  展示给定列。

- void showRow(int row)

- void sortByColumn(int column, Qt::SortOrder order)

  按给定列和顺序中的值对模型进行排序。
  列可能为-1，在这种情况下，将不会显示排序指示符，并且模型将返回其自然的未排序顺序。 请注意，并非所有型号都支持此功能，在这种情况下甚至可能崩溃。

## 5.Reimplemented Protected Functions

- virtual void currentChanged(const QModelIndex &current, const QModelIndex &previous) override
- virtual int horizontalOffset() const override
- virtual bool isIndexHidden(const QModelIndex &index) const override
- virtual QModelIndex moveCursor(QAbstractItemView::CursorAction cursorAction, Qt::KeyboardModifiers modifiers) override
- virtual void paintEvent(QPaintEvent *event) override
- virtual QModelIndexList selectedIndexes() const override
- virtual void selectionChanged(const QItemSelection &selected, const QItemSelection &deselected) override
- virtual void setSelection(const QRect &rect, QItemSelectionModel::SelectionFlags flags) override
- virtual int sizeHintForColumn(int column) const override
- virtual int sizeHintForRow(int row) const override
- virtual void timerEvent(QTimerEvent *event) override
- virtual void updateGeometries() override
- virtual int verticalOffset() const override
- virtual QStyleOptionViewItem viewOptions() const override
- virtual QSize viewportSizeHint() const override

## 6.Protected Slots

- void columnCountChanged(int oldCount, int newCount)
- void columnMoved(int column, int oldIndex, int newIndex)
- void columnResized(int column, int oldWidth, int newWidth)
- void rowCountChanged(int oldCount, int newCount)
- void rowMoved(int row, int oldIndex, int newIndex)
- void rowResized(int row, int oldHeight, int newHeight)