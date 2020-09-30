# QHeaderView 

继承关系：`QHeaderView `->`QAbstractItemView`->`QAbstractScrollArea`->`QFrame`->`QWidget`

## 1.Public Types

`enum ResizeMode { Interactive, Fixed, Stretch, ResizeToContents, Custom }`

| Constant                      | Value | Description                                                  |
| ----------------------------- | ----- | ------------------------------------------------------------ |
| QHeaderView::Interactive      | 0     | 用户可以调整部分的大小。 也可以使用resizeSection（）以编程方式调整该部分的大小。 段大小默认为defaultSectionSize。 |
| QHeaderView::Fixed            | 2     | 用户无法调整该部分的大小。 只能使用resizeSection（）以编程方式调整该部分的大小。 段大小默认为defaultSectionSize。 |
| QHeaderView::Stretch          | 1     | QHeaderView将自动调整该部分的大小以填充可用空间。 大小不能由用户或以编程方式更改。 |
| QHeaderView::ResizeToContents | 3     | QHeaderView将基于整个列或行的内容自动将节的大小调整为最佳大小。 大小不能由用户或以编程方式更改。 |

QHeaderView::Custom已经过时弃用了。

## 2.Properties

- cascadingSectionResizes : bool

  此属性保存是否在用户调整大小的部分达到最小大小后是否将交互式调整大小级联到以下部分
  此属性仅影响将交互作为其调整大小模式的部分。
  默认值为false。

- defaultAlignment : Qt::Alignment

  此属性保存每个标题部分中文本的默认对齐方式

- defaultSectionSize : int

  在调整大小之前，此属性保存标题部分的默认大小。
  **此属性仅影响将“交互”或“固定”作为其调整大小模式的部分**。
  默认情况下，此属性的值取决于样式。 因此，当样式更改时，此属性将从中更新。 调用setDefaultSectionSize（）将停止更新，调用resetDefaultSectionSize（）将恢复默认行为。

- firstSectionMovable : bool

  此属性保存用户是否可以移动第一列
  此属性控制用户是否可以移动第一列。 在QTreeView中，第一列保留树结构，因此即使在setSectionsMovable（true）之后，默认情况下也是不可移动的。
  通过调用此方法，可以使它再次可移动，例如在没有树形结构的平面列表的情况下。 在这种情况下，建议也调用QTreeView :: setRootIsDecorated（false）。
  除非也调用setSectionsMovable（true），否则将其设置为true无效。

- highlightSections : bool

  此属性保存包含所选项目的节是否突出显示
  默认情况下，此属性为false。

- maximumSectionSize : int

  此属性保存标题部分的最大大小。
  最大部分大小是允许的最大部分大小。 此属性的默认值为1048575，这也是节的最大可能大小。 将最大值设置为-1会将值重置为最大部分大小。
  除拉伸外，此属性在所有调整大小模式下均受重视

- minimumSectionSize : int

  此属性保存标题部分的最小大小。
  最小部分大小是允许的最小部分大小。 如果最小节大小设置为-1，则QHeaderView将使用全局支杆或字体度量大小的最大值。
  所有调整大小模式均支持此属性。

- showSortIndicator : bool

  此属性保存是否显示排序指示器
  默认情况下，此属性为false。

- stretchLastSection : bool

  此属性保存标题中最后一个可见部分是否占用所有可用空间
  默认值为false。
  注意：QTreeView提供的水平标题已配置为true，以确保该视图不会浪费为其标题分配的任何空间。 如果将此值设置为true，则此属性将覆盖在标题的最后一节中设置的调整大小模式。

## 3.Public Functions

- QHeaderView(Qt::Orientation orientation, QWidget *parent = nullptr)
- virtual ~QHeaderView()
- bool cascadingSectionResizes() const
- int count() const
- Qt::Alignment defaultAlignment() const
- int defaultSectionSize() const
- int hiddenSectionCount() const
- void hideSection(int logicalIndex)
- bool highlightSections() const
- bool isFirstSectionMovable() const
- bool isSectionHidden(int logicalIndex) const
- bool isSortIndicatorShown() const
- int length() const
- int logicalIndex(int visualIndex) const
- int logicalIndexAt(int position) const
- int logicalIndexAt(int x, int y) const
- int logicalIndexAt(const QPoint &pos) const
- int maximumSectionSize() const
- int minimumSectionSize() const
- void moveSection(int from, int to)
- int offset() const
- Qt::Orientation orientation() const
- void resetDefaultSectionSize()
- int resizeContentsPrecision() const
- void resizeSection(int logicalIndex, int size)
- void resizeSections(QHeaderView::ResizeMode mode)
- bool restoreState(const QByteArray &state)
- QByteArray saveState() const
- int sectionPosition(int logicalIndex) const
- QHeaderView::ResizeMode sectionResizeMode(int logicalIndex) const
- int sectionSize(int logicalIndex) const
- int sectionSizeHint(int logicalIndex) const
- int sectionViewportPosition(int logicalIndex) const
- bool sectionsClickable() const
- bool sectionsHidden() const
- bool sectionsMovable() const
- bool sectionsMoved() const
- void setCascadingSectionResizes(bool enable)
- void setDefaultAlignment(Qt::Alignment alignment)
- void setDefaultSectionSize(int size)
- void setFirstSectionMovable(bool movable)
- void setHighlightSections(bool highlight)
- void setMaximumSectionSize(int size)
- void setMinimumSectionSize(int size)
- void setResizeContentsPrecision(int precision)
- void setSectionHidden(int logicalIndex, bool hide)
- void setSectionResizeMode(QHeaderView::ResizeMode mode)
- void setSectionResizeMode(int logicalIndex, QHeaderView::ResizeMode mode)
- void setSectionsClickable(bool clickable)
- void setSectionsMovable(bool movable)
- void setSortIndicator(int logicalIndex, Qt::SortOrder order)
- void setSortIndicatorShown(bool show)
- void setStretchLastSection(bool stretch)
- void showSection(int logicalIndex)
- Qt::SortOrder sortIndicatorOrder() const
- int sortIndicatorSection() const
- bool stretchLastSection() const
- int stretchSectionCount() const
- void swapSections(int first, int second)
- int visualIndex(int logicalIndex) const
- int visualIndexAt(int position) const

## 4.Reimplemented Public Functions

- virtual void reset() override
- virtual void setModel(QAbstractItemModel *model) override
- virtual void setVisible(bool v) override
- virtual QSize sizeHint() const override

## 5.Public Slots

- void headerDataChanged(Qt::Orientation orientation, int logicalFirst, int logicalLast)
- void setOffset(int offset)
- void setOffsetToLastSection()
- void setOffsetToSectionPosition(int visualSectionNumber)

## 6.Signals

- void geometriesChanged()
- void sectionClicked(int logicalIndex)
- void sectionCountChanged(int oldCount, int newCount)
- void sectionDoubleClicked(int logicalIndex)
- void sectionEntered(int logicalIndex)
- void sectionHandleDoubleClicked(int logicalIndex)
- void sectionMoved(int logicalIndex, int oldVisualIndex, int newVisualIndex)
- void sectionPressed(int logicalIndex)
- void sectionResized(int logicalIndex, int oldSize, int newSize)
- void sortIndicatorChanged(int logicalIndex, Qt::SortOrder order)

## 7.Protected Functions

- void initStyleOption(QStyleOptionHeader *option) const
- virtual void paintSection(QPainter *painter, const QRect &rect, int logicalIndex) const
- virtual QSize sectionSizeFromContents(int logicalIndex) const

## 8.Reimplemented Protected Functions

- virtual void currentChanged(const QModelIndex &current, const QModelIndex &old) override
- virtual bool event(QEvent *e) override
- virtual int horizontalOffset() const override
- virtual void mouseDoubleClickEvent(QMouseEvent *e) override
- virtual void mouseMoveEvent(QMouseEvent *e) override
- virtual void mousePressEvent(QMouseEvent *e) override
- virtual void mouseReleaseEvent(QMouseEvent *e) override
- virtual void paintEvent(QPaintEvent *e) override
- virtual void setSelection(const QRect &rect, QItemSelectionModel::SelectionFlags flags) override
- virtual int verticalOffset() const override
- virtual bool viewportEvent(QEvent *e) override

## 9.Protected Slots

- void resizeSections()
- void sectionsAboutToBeRemoved(const QModelIndex &parent, int logicalFirst, int logicalLast)
- void sectionsInserted(const QModelIndex &parent, int logicalFirst, int logicalLast)