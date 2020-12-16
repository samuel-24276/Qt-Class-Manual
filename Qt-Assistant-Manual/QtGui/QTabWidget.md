# QTabWidget

继承关系：`QTabWidget`->`QWidget`->` QObject` and `QPaintDevice`

## 1.Public Types

- enum	TabPosition { North, South, West, East }
- enum	TabShape { Rounded, Triangular }

## 2.Properties

- count : const int
- currentIndex : int
- documentMode : bool
- elideMode : Qt::TextElideMode
- iconSize : QSize
- movable : bool
- tabPosition : TabPosition
- tabShape : TabShape
- tabsClosable : bool
- usesScrollButtons : bool

## 3.Public Functions

QTabWidget ( QWidget * parent = 0 )
~QTabWidget ()
int	addTab ( QWidget * page, const QString & label )
int	addTab ( QWidget * page, const QIcon & icon, const QString & label )
void	clear ()
QWidget *	cornerWidget ( Qt::Corner corner = Qt::TopRightCorner ) const
int	count () const
int	currentIndex () const
QWidget *	currentWidget () const
bool	documentMode () const
Qt::TextElideMode	elideMode () const
QSize	iconSize () const
int	indexOf ( QWidget * w ) const
int	insertTab ( int index, QWidget * page, const QString & label )
int	insertTab ( int index, QWidget * page, const QIcon & icon, const QString & label )
bool	isMovable () const
bool	isTabEnabled ( int index ) const
void	removeTab ( int index )
void	setCornerWidget ( QWidget * widget, Qt::Corner corner = Qt::TopRightCorner )
void	setDocumentMode ( bool set )
void	setElideMode ( Qt::TextElideMode )
void	setIconSize ( const QSize & size )
void	setMovable ( bool movable )
void	setTabEnabled ( int index, bool enable )
void	setTabIcon ( int index, const QIcon & icon )
void	setTabPosition ( TabPosition )
void	setTabShape ( TabShape s )
void	setTabText ( int index, const QString & label )
void	setTabToolTip ( int index, const QString & tip )
void	setTabWhatsThis ( int index, const QString & text )
void	setTabsClosable ( bool closeable )
void	setUsesScrollButtons ( bool useButtons )
QIcon	tabIcon ( int index ) const
TabPosition	tabPosition () const
TabShape	tabShape () const
QString	tabText ( int index ) const
QString	tabToolTip ( int index ) const
QString	tabWhatsThis ( int index ) const
bool	tabsClosable () const
bool	usesScrollButtons () const
QWidget *	widget ( int index ) const

## 4.Reimplemented Public Functions

- virtual int	heightForWidth ( int width ) const
- virtual QSize	minimumSizeHint () const
- virtual QSize	sizeHint () const

## 5.Public Slots

- void	setCurrentIndex ( int index )
- void	setCurrentWidget ( QWidget * widget )

## 6.Signals

- void	currentChanged ( int index )
- void	tabCloseRequested ( int index )

## 7.Protected Functions

- void	initStyleOption ( QStyleOptionTabWidgetFrame * option ) const
- void	setTabBar ( QTabBar * tb )
- QTabBar *	tabBar () const
- virtual void	tabInserted ( int index )
- virtual void	tabRemoved ( int index )

## 8.Reimplemented Protected Functions

- virtual void	changeEvent ( QEvent * ev )
- virtual bool	event ( QEvent * ev )
- virtual void	keyPressEvent ( QKeyEvent * e )
- virtual void	paintEvent ( QPaintEvent * event )
- virtual void	resizeEvent ( QResizeEvent * e )
- virtual void	showEvent ( QShowEvent * )

## 9.Detailed Description

QTabWidget类提供了选项卡小部件堆栈。

选项卡小部件提供一个**选项卡栏(参见QTabBar)**和一个“页面区域”，用于显示与每个选项卡相关的页面。默认情况下，选项卡栏显示在页面区域的上方，但是可以使用不同的配置(参见TabPosition)。每个选项卡都与一个不同的小部件(称为页面)相关联。页面区域中只显示当前页面;所有其他页面被隐藏。用户可以通过单击标签或按下Alt+字母快捷键(如果有的话)来显示不同的页面。

使用QTabWidget的通常方法是执行以下操作:

- 创建一个QTabWidget。
- 为选项卡对话框中的每个页面创建QWidget，但不要为它们指定父窗口小部件。
- 将子部件插入到页面部件中，使用布局正常定位它们。
- 调用addTab()或insertTab()将页面小部件放入选项卡小部件中，为每个选项卡提供合适的标签和可选的键盘快捷方式。

tabs的位置由 tabPosition定义，其形状由tabShape定义。

当用户选择页面时，会发出currentChanged()信号。

当前页面索引可用作currentIndex()，它是带有currentWidget()的当前页面小部件。您可以使用widget()检索指向具有给定索引的页面小部件的指针，并可以使用indexOf()查找小部件的索引位置。使用setCurrentWidget()或setCurrentIndex()来显示特定的页面。

可以使用setTabText()或setTabIcon()更改选项卡的文本和图标。可以使用removeTab()删除选项卡及其关联页面。

每个选项卡在任何时候都可以启用或禁用(参见setTabEnabled())。如果选项卡是启用的，选项卡文本将正常绘制，用户可以选择该选项卡。如果禁用该选项卡，则该选项卡将以不同的方式绘制，用户将无法选择该选项卡。请注意，即使禁用了一个选项卡，页面仍然可以是可见的，例如，如果所有的选项卡都被禁用了。

选项卡小部件是拆分复杂对话框的好方法。另一种选择是使用QStackedWidget，您可以为它提供在页面之间导航的方法，例如QToolBar或QListWidget。

QTabWidget中的大多数功能是由QTabBar(顶部，提供选项卡)和QStackedWidget(大部分区域，组织各个页面)提供的。