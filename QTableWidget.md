# QTableWidget

> 继承关系：`QTableWidget`->`QTableView`->`QAbstractItemView`->`QAbstractScrollArea`->`QFrame`->`QWidget`

## 1.Properties

- columnCount : int				列数
- rowCount : int                      行数

 ## 2.Public Functions

- QTableWidget(int rows, int columns, QWidget *parent = nullptr)

- QTableWidget(QWidget *parent = nullptr)

- virtual ~QTableWidget()

- QWidget *cellWidget(int row, int column) const

  返回显示在给定行和列的单元格中的窗口部件。
  注意：该表拥有窗口部件的所有权。

- void closePersistentEditor(QTableWidgetItem *item)

  关闭项目的持久性编辑器。

- int column(const QTableWidgetItem *item) const

  返回窗口部件所在列数

- int columnCount() const

  返回表格总列数

- int currentColumn() const

  返回当前窗口的所在列数

- **void setColumnCount(int columns)**

  设置表格的总列数，只有设置好列数才会自动生成列名，自己命名列名可以通过setHorizontalHeaderLabels(const QStringList &labels)函数完成，前提是设置好了列数。

- QTableWidgetItem *currentItem() const

  返回当前窗口部件

- int row(const QTableWidgetItem *item) const

  返回item所在行数。

- int rowCount() const

  返回表格的总行数

- int currentRow() const

  返回当前窗口所在行数

- **void setRowCount(int rows)**

  设置表格的行数,只有设置好行数才会自动生成行名，自己命名行名可以通过setVerticalHeaderLabels(const QStringList &labels)函数完成，前提是设置好了行数。

- void editItem(QTableWidgetItem *item)

  如果项目可编辑，则开始对其进行编辑。

- QList<QTableWidgetItem *> findItems(const QString &text, Qt::MatchFlags flags) const

  使用给定的标志查找与文本匹配的项目。

- QTableWidgetItem *horizontalHeaderItem(int column) const

  如果已设置，则返回column，column的水平标题项目； 否则返回nullptr。

- bool isPersistentEditorOpen(QTableWidgetItem *item) const

  返回是否为项目item打开持久性编辑器。

- **QTableWidgetItem *item(int row, int column) const**

  返回给定行和列的项目（如果已设置）； 否则返回nullptr。

- QTableWidgetItem *itemAt(const QPoint &point) const

  返回指向给定点处的项的指针，或者如果表小部件中的项未覆盖该点，则返回nullptr。

- **QTableWidgetItem *itemAt(int ax, int ay) const**

  在表小部件的坐标系中返回与QPoint（ax，ay）等效的位置处的项目，或者如果表小部件中的项目未覆盖指定的点，则返回nullptr。

- const QTableWidgetItem *itemPrototype() const

  返回表使用的项目原型。

- void openPersistentEditor(QTableWidgetItem *item)

  打开给定项目的编辑器。 编辑后，编辑器保持打开状态。

- void removeCellWidget(int row, int column)

  删除在行和列指示的单元格上设置的部件。

- QList<QTableWidgetItem *> selectedItems() const

  返回所有选定项目的列表。
  此函数返回指向所选单元格内容的指针列表。 使用selectedIndexes（）函数检索包括空单元格在内的完整选择。

- QList<QTableWidgetSelectionRange> selectedRanges() const

  返回所有选定范围的列表。

- void setCellWidget(int row, int column, QWidget *widget)

  将给定的窗口小部件设置为在给定的行和列的单元格中显示，将窗口小部件的所有权传递给表。
  如果将单元小部件A替换为单元小部件B，则将删除单元小部件A。

- void setCurrentCell(int row, int column)

  设置当前的单元格所在行列

- void setCurrentCell(int row, int column, QItemSelectionModel::SelectionFlags command)

  使用给定command将当前单元格设置为位置（行，列）处的单元格。

- void setCurrentItem(QTableWidgetItem *item)

  将当前项目设置为item。
  除非选择模式为NoSelection，否则也将选择该项目。

- void setCurrentItem(QTableWidgetItem *item, QItemSelectionModel::SelectionFlags command)

  使用给定命令将当前项目设置为item。

- void setHorizontalHeaderItem(int column, QTableWidgetItem *item)

  将列的水平标题项目设置为item。 如有必要，可增加列数以适合该项目。 前一个标题项（如果有的话）被删除。

- **void setHorizontalHeaderLabels(const QStringList &labels)**

  **使用标签设置水平标题标签。**

- void setItem(int row, int column, QTableWidgetItem *item)

  将给定行和列的项目设置为item。
  该表获取项目的所有权。
  请注意，如果启用了排序（请参阅sortingEnabled），并且column是当前的排序列，则该行将移动到由item确定的排序位置。
  如果要设置特定行的多个项目（例如，通过循环调用setItem（）），则可能需要先关闭排序，然后再打开排序； 这将允许您对同一行中的所有项目使用相同的行参数（即setItem（）不会移动该行）

- void setItemPrototype(const QTableWidgetItem *item)

  将表的项目原型设置为指定的项目。
  当需要创建新表项时，表小部件将使用项原型克隆功能。 例如，当用户在空单元格中编辑时。 当您有QTableWidgetItem子类并且要确保QTableWidget创建子类的实例时，这很有用。
  该表获取原型的所有权。

- void setRangeSelected(const QTableWidgetSelectionRange &range, bool select)

  根据选择来选择或取消选择范围。

- void setVerticalHeaderItem(int row, QTableWidgetItem *item)

  将行的垂直标题项目设置为item。

- **void setVerticalHeaderLabels(const QStringList &labels)**

  **使用标签设置垂直标题标签。**

- void sortItems(int column, Qt::SortOrder order = Qt::AscendingOrder)

  根据列和顺序对表小部件中的所有行进行排序。

- QTableWidgetItem *takeHorizontalHeaderItem(int column)

  从标题中删除列的水平标题项，而不删除它。

- QTableWidgetItem *takeItem(int row, int column)

  从表中删除行和列中的项目而不删除它。

- QTableWidgetItem *takeVerticalHeaderItem(int row)

  从标题中删除行中的垂直标题项，而不删除它。

- QTableWidgetItem *verticalHeaderItem(int row) const

  返回行的垂直标题项。

- int visualColumn(int logicalColumn) const

  返回给定逻辑列的可视列。

- QRect visualItemRect(const QTableWidgetItem *item) const

  返回item处该项目所占据的视口上的矩形。

- int visualRow(int logicalRow) const

  返回给定逻辑行的可视行。

## 3.Public Slots

- void clear()

  删除视图中的所有项目。 这还将删除所有选择和标题。 如果您不想删除标题，请使用QTableWidget :: clearContents（）。 表格尺寸保持不变。

- void clearContents()

  从视图中删除标题中没有的所有项目。 这也将删除所有选择。 表格尺寸保持不变。

- void insertColumn(int column)

  将一个空列插入表中的列。

- void insertRow(int row)

  将空行插入表格中的行。

- void removeColumn(int column)

  从表中删除column列及其所有项目。

- void removeRow(int row)

  从表中删除row行及其所有项目。

- **void scrollToItem**(const QTableWidgetItem *item, QAbstractItemView::ScrollHint hint EnsureVisible)

  如有必要，**滚动视图以确保该项目可见**。 提示参数可以更精确地指定操作后该项目应位于的位置。

## 4.Signals

- void cellActivated(int row, int column)

  当行和列指定的单元格已激活时，将发出此信号

- void cellChanged(int row, int column)

  只要行和列指定的单元格中的项目数据发生更改，就会发出此信号。

- void cellClicked(int row, int column)

  每当单击表格中的单元格时，都会发出此信号。 指定的行和列是单击的单元格。

- void cellDoubleClicked(int row, int column)

  每当双击表格中的一个单元格时，就会发出此信号。 指定的行和列是双击的单元格。

- void cellEntered(int row, int column)

  当鼠标光标进入单元格时，将发出此信号。 该单元格由行和列指定。
  仅当打开mouseTracking或在移入项目时按下鼠标按钮时，才发出此信号。

- void cellPressed(int row, int column)

  只要按下表格中的某个单元格，就会发出此信号。 指定的行和列是被按下的单元格。

- void currentCellChanged(int currentRow, int currentColumn, int previousRow, int previousColumn)

  每当当前单元格更改时，都会发出此信号。 previousRow和previousColumn指定的单元格是以前具有焦点的单元格，currentRow和currentColumn指定的单元格是新的当前单元格。

- void currentItemChanged(QTableWidgetItem *current, QTableWidgetItem *previous)

  当前项目更改时，将发出此信号。 上一个项目是先前具有焦点的项目，当前是新的当前项目。

- void itemActivated(QTableWidgetItem *item)

  当指定的项目被激活时，该信号被发射

- void itemChanged(QTableWidgetItem *item)

  每当项目数据更改时，都会发出此信号。

- void itemClicked(QTableWidgetItem *item)

  每当单击表中的项目时，都会发出此信号。 指定的项目是单击的项目。

- void itemDoubleClicked(QTableWidgetItem *item)

  每当双击表中的一个项目时，都会发出此信号。 指定的项目是被双击的项目。

- void itemEntered(QTableWidgetItem *item)

  当鼠标光标进入一个项目时，该信号被发射。 该项目是输入的项目。
  仅当打开mouseTracking或在移入项目时按下鼠标按钮时，才发出此信号。

- void itemPressed(QTableWidgetItem *item)

  每当按下表格中的项目时，就会发出此信号。 指定的项目是被按下的项目。

- void itemSelectionChanged()

  选择更改时，将发出此信号。

## 5.Protected Functions

- virtual bool dropMimeData(int row, int column, const QMimeData *data, Qt::DropAction action)

  处理在给定的行和列中以给定操作结束的拖放操作提供的数据。 如果模型可以处理数据和操作，则返回true； 否则返回false。

- QModelIndex indexFromItem(const QTableWidgetItem *item) const

  返回与给定项目关联的QModelIndex。

- QTableWidgetItem *itemFromIndex(const QModelIndex &index) const

  返回指向与给定索引关联的QTableWidgetItem的指针。

- QList<QTableWidgetItem *> items(const QMimeData *data) const

  返回指向数据对象中包含的项目的指针的列表。 如果对象不是由QTreeWidget在同一过程中创建的，则列表为空。

- virtual QMimeData *mimeData(const QList<QTableWidgetItem *> items) const

  返回一个对象，其中包含指定项目的序列化描述。 用于描述项目的格式是从mimeTypes（）函数获得的。
  如果项目列表为空，则返回nullptr而不是序列化的空列表。

- virtual QStringList mimeTypes() const

  返回可用于描述tablewidget项列表的MIME类型的列表。

- virtual Qt::DropActions supportedDropActions() const

  返回此视图支持的放置动作。

## 6.Reimplemented Protected Functions

- virtual void dropEvent(QDropEvent *event) override

  重新实现：QAbstractItemView :: dropEvent（QDropEvent * event）。

- virtual bool event(QEvent *e) override

  重新实现：: QAbstractItemView::event(QEvent *event).

