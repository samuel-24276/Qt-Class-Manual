# QGridLayout

继承关系：`QGridLayout`->`QLayout`->`QObject` and `QLayoutItem`

## 1.Properties

- horizontalSpacing : int

  此属性保存并排放置的小部件之间的间距。

  如果未显式设置任何值，则布局的水平间距将从父布局或父窗口小部件的样式设置继承。

- verticalSpacing : int

  此属性保存彼此重叠放置的小部件之间的间距。

  如果未显式设置任何值，则布局的垂直间距将从父布局或父窗口小部件的样式设置继承。

## 2.Public Functions

QGridLayout ( QWidget * parent )

QGridLayout ()
~QGridLayout ()
void	addItem ( QLayoutItem * item, int row, int column, int rowSpan = 1, int columnSpan = 1, Qt::Alignment alignment = 0 )
void	addLayout ( QLayout * layout, int row, int column, Qt::Alignment alignment = 0 )
void	addLayout ( QLayout * layout, int row, int column, int rowSpan, int columnSpan, Qt::Alignment alignment = 0 )
void	addWidget ( QWidget * widget, int row, int column, Qt::Alignment alignment = 0 )
void	addWidget ( QWidget * widget, int fromRow, int fromColumn, int rowSpan, int columnSpan, Qt::Alignment alignment = 0 )
QRect	cellRect ( int row, int column ) const
int	columnCount () const
int	columnMinimumWidth ( int column ) const
int	columnStretch ( int column ) const
void	getItemPosition ( int index, int * row, int * column, int * rowSpan, int * columnSpan )
int	horizontalSpacing () const
QLayoutItem *	itemAtPosition ( int row, int column ) const
Qt::Corner	originCorner () const
int	rowCount () const
int	rowMinimumHeight ( int row ) const
int	rowStretch ( int row ) const
void	setColumnMinimumWidth ( int column, int minSize )
void	setColumnStretch ( int column, int stretch )
void	setHorizontalSpacing ( int spacing )
void	setOriginCorner ( Qt::Corner corner )
void	setRowMinimumHeight ( int row, int minSize )
void	setRowStretch ( int row, int stretch )
void	setSpacing ( int spacing )
void	setVerticalSpacing ( int spacing )
int	spacing () const
int	verticalSpacing () const

## 3.Reimplemented Public Functions

virtual int	count () const
virtual Qt::Orientations	expandingDirections () const
virtual bool	hasHeightForWidth () const
virtual int	heightForWidth ( int w ) const
virtual void	invalidate ()
virtual QLayoutItem *	itemAt ( int index ) const
virtual QSize	maximumSize () const
virtual int	minimumHeightForWidth ( int w ) const
virtual QSize	minimumSize () const
virtual void	setGeometry ( const QRect & rect )
virtual QSize	sizeHint () const
virtual QLayoutItem *	takeAt ( int index )

## 4.Reimplemented Protected Functions

`virtual void	addItem ( QLayoutItem * item )`

## 5.Detailed Description

QGridLayout类将小部件布置在网格中。

QGridLayout占用可用空间（通过其父布局或parentWidget（）），将其划分为行和列，然后将其管理的每个窗口小部件放入正确的单元格中。

列和行的行为相同；我们将讨论列，但行具有等效功能。

每列都有最小宽度和拉伸因子。最小宽度是使用setColumnMinimumWidth（）设置的最大宽度，以及该列中每个小部件的最小宽度。拉伸因子是使用setColumnStretch（）设置的，并确定列将超出其所需最小值的可用空间量。

通常，每个托管窗口小部件或布局都使用addWidget（）放入其自己的单元格中。小部件还可能使用addItem（）和addWidget（）的行和列跨度重载来占用多个单元格。如果这样做，QGridLayout将猜测如何在列/行上分配大小（基于拉伸因子）。

要从布局中删除小部件，请调用removeWidget（）。在小部件上调用QWidget :: hide（）也会有效地从布局中删除该小部件，直到调用QWidget :: show（）为止。

下图显示了带有五列三行网格的对话框的一部分（该网格显示为洋红色覆盖）：