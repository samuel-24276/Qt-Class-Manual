# QListView

继承关系：`QListView`->`QAbstractItemView`->`QAbstractScrollArea`->`QFrame`->`QWidget`

继承者：

- QHelpIndexWidget
- QListWidget
- QUndoView

## 1.Public Types

- enum	Flow { LeftToRight, TopToBottom }

  | Constant               | Value | Description                |
  | ---------------------- | ----- | -------------------------- |
  | QListView::LeftToRight | 0     | 项目在视图中从左到右排列。 |
  | QListView::TopToBottom | 1     | 项目在视图中从上到下排列。 |

- enum	LayoutMode { SinglePass, Batched }

  | Constant              | Value | Description              |
  | --------------------- | ----- | ------------------------ |
  | QListView::SinglePass | 0     | 所有的项目都被同时列出。 |
  | QListView::Batched    | 1     | 这些项目是按批次摆放的。 |

- enum	Movement { Static, Free, Snap }

  | Constant          | Value | Description                                        |
  | ----------------- | ----- | -------------------------------------------------- |
  | QListView::Static | 0     | 用户不能移动项目。                                 |
  | QListView::Free   | 1     | 用户可以自由移动项目。                             |
  | QListView::Snap   | 2     | 当移动时，项目捕捉到指定的网格;看到setGridSize()。 |

- enum	ResizeMode { Fixed, Adjust }

  | Constant          | Value | Description                                |
  | ----------------- | ----- | ------------------------------------------ |
  | QListView::Fixed  | 0     | 只有在视图第一次显示时才会显示这些项。     |
  | QListView::Adjust | 1     | 每当视图调整大小时，这些项都将被显示出来。 |

- enum	ViewMode { ListMode, IconMode }

  | Constant            | Value | Description                                      |
  | ------------------- | ----- | ------------------------------------------------ |
  | QListView::ListMode | 0     | 项目摆放采用自上而下的流动方式，体积小，静态运动 |
  | QListView::IconMode | 1     | 物品采用从左到右流线摆放，尺寸大，移动自由       |

## 2.Properties

- batchSize : int

  如果将layoutMode设置为批处理，此属性保存每个批处理中布局的项数。

  默认值是100。

- flow : Flow

  此属性保存项目布局应该流向的方向。

  如果此属性为LeftToRight，则项目将从左到右布局。如果isWrapping属性为true，布局将在它到达可见区域的右侧时自动换行。如果此属性为top - tobottom，则项目将从可见区域的顶部展开，在到达底部时进行自动换行。

  *在视图可见时设置此属性将导致条目再次被布局*。

  默认情况下，该属性被设置为TopToBottom。

- gridSize : QSize

  此属性保存布局网格的大小。

  此属性是项被布置的网格的大小。默认值是空大小，这意味着没有网格，布局没有在网格中完成。将此属性设置为非空大小将在网格布局中切换。(当网格布局生效时，spacing属性将被忽略。)

  *在视图可见时设置此属性将导致条目再次被布局*。

- isWrapping : bool

  此属性用于判断是否应该换行条目布局。

  此属性用于在可见区域没有更多空间时布局是否应该换行。布局包装的位置取决于流属性。

  *在视图可见时设置此属性将导致条目再次被布局*。

  默认情况下，该属性为false。

- layoutMode : LayoutMode

  此属性**决定项的布局是立即发生还是延迟发生**。

  此属性保存项的布局模式。当模式为SinglePass(默认值)时，所有项目都被一次性列出。当对模式进行批处理时，在处理事件时，项目以批处理大小的项目进行布局。这使得即时查看可视项目并与之交互成为可能，而其他项目正在被布局。

- modelColumn : int

  此属性保存模型中可见的列。

  默认情况下，该属性包含0，表示将显示模型中的第一列。

- movement : Movement

  此属性用于**表示项目是否可以自由移动、是否被锁定到网格或根本不能移动**。

  此属性决定用户如何在视图中移动项目。静态意味着项目不能在用户中移动。自由意味着用户可以将项目拖放到视图中的任何位置。*Snap意味着用户可以拖放项目，但只能拖放到gridSize属性所指定的网格中的位置*。

  在视图可见时设置此属性将导致条目再次被布局。

  默认情况下，此属性设置为Static。

- resizeMode : ResizeMode

  此属性用于在视图调整大小时是否再次显示项。

  如果该属性被调整，当视图调整大小时，项目将再次显示。如果该值是固定的，那么当视图调整大小时，这些项将不会显示出来。

  默认情况下，此属性被设置为Fixed。

- selectionRectVisible : bool

  如果选择矩形应该是可见的，则此属性保留。

  如果此属性为真，则选择矩形可见;否则它将被隐藏。

  注意:只有在选择模式处于可以选择多个项目的模式下，选择矩形才会可见;也就是说，如果选择模式是QAbstractItemView::SingleSelection，它将不会绘制一个选择矩形。

  默认情况下，该属性为false。

- spacing : int

  此属性保存布局中项目周围的空间。

  此属性是布局中围绕一个项目填充的空白空间的大小。

  在视图可见时设置此属性将导致条目再次被布局。

  默认情况下，这个属性包含0的值。

- uniformItemSizes : bool

  此属性用于判断listview中的所有项是否具有相同的大小。

  只有在保证视图中的所有项具有相同的大小时，才应该将此属性设置为true。这使视图能够为性能目的进行一些优化。

  默认情况下，该属性为false。

- viewMode : ViewMode

  该属性保存QListView的查看模式。

  此属性将更改其他未设置的属性，以符合设置视图模式。已经设置的特定于qlistview的属性不会被更改，除非调用了clearPropertyFlags()。

  设置视图模式将根据选定的移动启用或禁用拖放。对于ListMode，默认的移动是静态的(禁用拖放);对于IconMode，默认的移动是自由的(启用了拖放)。

- wordWrap : bool

  此属性保存项文本单词包装策略。

  如果该属性为true，则在需要换行的地方对条目文本进行换行;否则它根本不会被包装。默认情况下，此属性为false。

  请注意，即使启用了换行，单元格也不会展开为文本腾出空间。根据视图的textElideMode，它将为不能显示的文本打印省略号。

## 3.Public Functions

- QListView ( QWidget * parent = 0 )

- ~QListView ()

- void	clearPropertyFlags ()

  清除QListView特定的属性标志。

  从QAbstractItemView继承的属性不包含在属性标志中。具体来说，当调用setMovement()或setViewMode()时，dragEnabled和acceptsdrop由QListView计算。

- bool	isRowHidden ( int row ) const

  如果行被隐藏，返回true;否则返回false。

- void	setBatchSize ( int batchSize )

- void	setFlow ( Flow flow )

- void	setGridSize ( const QSize & size )

- void	setLayoutMode ( LayoutMode mode )

- void	setModelColumn ( int column )

- void	setMovement ( Movement movement )

- void	setResizeMode ( ResizeMode mode )

- void	setRowHidden ( int row, bool hide )

- void	setSelectionRectVisible ( bool show )

- void	setSpacing ( int space )

- void	setUniformItemSizes ( bool enable )

- void	setViewMode ( ViewMode mode )

- void	setWordWrap ( bool on )

- void	setWrapping ( bool enable )

- int	batchSize () const

- Flow	flow () const

- QSize	gridSize () const

- bool	isSelectionRectVisible () const

- bool	isWrapping () const

- LayoutMode	layoutMode () const

- int	modelColumn () const

- Movement	movement () const

- ResizeMode	resizeMode () const

- int	spacing () const

- bool	uniformItemSizes () const

- ViewMode	viewMode () const

- bool	wordWrap () const

## 4.Reimplemented Public Functions

- virtual QModelIndex	indexAt ( const QPoint & p ) const
- virtual void	scrollTo ( const QModelIndex & index, ScrollHint hint = EnsureVisible )
- virtual QRect	visualRect ( const QModelIndex & index ) const

## 5.Signals

- void	indexesMoved ( const QModelIndexList & indexes )

  当视图中移动指定的索引时，将发出此信号。

## 6.Protected Functions

- QRect	rectForIndex ( const QModelIndex & index ) const
- void	setPositionForIndex ( const QPoint & position, const QModelIndex & index )

## 7.Reimplemented Protected Functions

- virtual void	currentChanged ( const QModelIndex & current, const QModelIndex & previous )
- virtual void	dataChanged ( const QModelIndex & topLeft, const QModelIndex & bottomRight )
- virtual void	dragLeaveEvent ( QDragLeaveEvent * e )
- virtual void	dragMoveEvent ( QDragMoveEvent * e )
- virtual void	dropEvent ( QDropEvent * e )
- virtual bool	event ( QEvent * e )
- virtual int	horizontalOffset () const
- virtual bool	isIndexHidden ( const QModelIndex & index ) const
- virtual void	mouseMoveEvent ( QMouseEvent * e )
- virtual void	mouseReleaseEvent ( QMouseEvent * e )
- virtual QModelIndex	moveCursor ( CursorAction cursorAction, Qt::KeyboardModifiers modifiers )
- virtual void	paintEvent ( QPaintEvent * e )
- virtual void	resizeEvent ( QResizeEvent * e )
- virtual void	rowsAboutToBeRemoved ( const QModelIndex & parent, int start, int end )
- virtual void	rowsInserted ( const QModelIndex & parent, int start, int end )
- virtual QModelIndexList	selectedIndexes () const
- virtual void	selectionChanged ( const QItemSelection & selected, const QItemSelection & deselected )
- virtual void	setSelection ( const QRect & rect, QItemSelectionModel::SelectionFlags command )
- virtual void	startDrag ( Qt::DropActions supportedActions )
- virtual void	timerEvent ( QTimerEvent * e )
- virtual void	updateGeometries ()
- virtual int	verticalOffset () const
- virtual QStyleOptionViewItem	viewOptions () const
- virtual QRegion	visualRegionForSelection ( const QItemSelection & selection ) const

## 8.Detailed Description

QListView类为模型提供了一个列表或图标视图。

QListView显示存储在模型中的项，可以作为一个简单的非分层列表，也可以作为一组图标。这个类**用于提供列表和图标视图**，这些视图以前是由QListBox和QIconView类提供的，但是使用了Qt模型/视图体系结构提供的更灵活的方法。

QListView类是一个模型/视图类，是Qt模型/视图框架的一部分。

此视图不显示水平或垂直标题;要显示带有水平标题的项目列表，请使用QTreeView。

QListView实现了QAbstractItemView类定义的接口，以允许它显示由QAbstractItemModel类派生的模型提供的数据。

列表视图中的项目可以使用两种视图模式中的一种来显示:在列表模式中，项目以简单列表的形式显示;在IconMode中，列表视图采用图标视图的形式，其中的项目用图标显示，就像文件管理器中的文件一样。默认情况下，列表视图处于列表模式。要更改视图模式，可以使用setViewMode()函数，要确定当前的视图模式，可以使用viewMode()函数。

这些视图中的项按照列表视图的flow()指定的方向进行布局。根据视图的movement()状态，这些项可以固定在适当的位置，或者允许移动。

如果模型中的项目不能完全按照流的方向布局，它们可以被包装在视图部件的边界上;这取决于isWrapping()。当项目由图标视图表示时，此属性非常有用。

resizeMode()和layoutMode()控制如何以及何时布置项目。项目根据它们的间距()来分隔，并且可以存在于gridSize()指定的概念网格大小中。可以根据项目的图标大小()将其呈现为大图标或小图标。

### Improving Performance

为了在显示大量条目时提高视图的性能，可以给视图提供它正在处理的数据的提示。对于想要显示大小相同的项的视图，可以采用的一种方法是将uniformItemSizes属性设置为true。