# QTabBar

继承关系：`QTabBar`->`QWidget`->` QObject` and `QPaintDevice`

## 1.Public Types

- enum	ButtonPosition { LeftSide, RightSide }

  该枚举类型列出了小部件在选项卡上的位置。

  | Constant           | Value | Description   |
  | ------------------ | ----- | ------------- |
  | QTabBar::LeftSide  | 0     | 放在tab页左边 |
  | QTabBar::RightSide | 1     | 放在tab页右边 |

- enum	SelectionBehavior { SelectLeftTab, SelectRightTab, SelectPreviousTab }

  枚举类型列出了**移除标签时QTabBar的行为**，被移除的标签也是当前标签。

  | Constant                   | Value | Description                      |
  | -------------------------- | ----- | -------------------------------- |
  | QTabBar::SelectLeftTab     | 0     | 选择要删除的选项卡左边的选项卡。 |
  | QTabBar::SelectRightTab    | 1     | 选择要删除的选项卡右边的选项卡。 |
  | QTabBar::SelectPreviousTab | 2     | 选择之前选择的选项卡。           |

- enum	Shape { RoundedNorth, RoundedSouth, RoundedWest, RoundedEast, ..., TriangularEast }

  枚举类型列出了QTabBar支持的内置形状。把这些当作提示，因为有些样式可能不会呈现某些形状。然而，位置应该受到尊重。

  | Constant                 | Value | Description                                     |
  | ------------------------ | ----- | ----------------------------------------------- |
  | QTabBar::RoundedNorth    | 0     | 页面上方正常的圆角外观                          |
  | QTabBar::RoundedSouth    | 1     | 页面下方正常的圆角外观                          |
  | QTabBar::RoundedWest     | 2     | 页面左侧正常的圆角外观                          |
  | QTabBar::RoundedEast     | 3     | 页面右侧正常的圆角外观                          |
  | QTabBar::TriangularNorth | 4     | 页面上方的三角形标签。                          |
  | QTabBar::TriangularSouth | 5     | 例如，与Excel电子表格中使用的类似的三角形选项卡 |
  | QTabBar::TriangularWest  | 6     | 页面左侧的三角形选项卡。                        |
  | QTabBar::TriangularEast  | 7     | 页面右侧的三角形选项卡。                        |

  

## 2.Properties

- count : const int

- currentIndex : int

- documentMode : bool

  无论选项卡栏是否以适合于主窗口的模式呈现，此属性均保持。

  此属性被用作样式的提示，以不同的方式绘制选项卡，然后它们通常在选项卡小部件中显示。在Mac OS X上，这个选项卡看起来与Safari或Leopard的Terminal.app中的选项卡类似。

- drawBase : bool

  这个属性定义了标签栏是否应该绘制它的Base。

  如果为真，那么QTabBar将绘制一个与overlab样式相关的基底。否则，只绘制选项卡。

- elideMode : Qt::TextElideMode

  此属性用于保存如何省略选项卡栏中的文本。

  此属性控制在没有足够空间显示给定选项卡栏大小的项时如何省略项。

  默认情况下，该值依赖于样式。

- expanding : bool

- iconSize : QSize

- movable : bool

- selectionBehaviorOnRemove : SelectionBehavior

- shape : Shape

- tabsClosable : bool

- usesScrollButtons : bool

  当选项卡栏有许多选项卡时，该属性用于确定选项卡栏是否应该使用按钮来滚动选项卡。

  当一个标签栏中有太多的标签时，标签栏可以选择扩大它的大小，或者添加按钮，让你滚动浏览标签。

  默认情况下，该值依赖于样式。

## 3.Public Functions

- QTabBar ( QWidget * parent = 0 )
- ~QTabBar ()
  int	addTab ( const QString & text )
  int	addTab ( const QIcon & icon, const QString & text )
  int	count () const
  int	currentIndex () const
  bool	documentMode () const
  bool	drawBase () const
  Qt::TextElideMode	elideMode () const
  bool	expanding () const
  QSize	iconSize () const
  int	insertTab ( int index, const QString & text )
  int	insertTab ( int index, const QIcon & icon, const QString & text )
  bool	isMovable () const
  bool	isTabEnabled ( int index ) const
  void	moveTab ( int from, int to )
  void	removeTab ( int index )
  SelectionBehavior	selectionBehaviorOnRemove () const
  void	setDocumentMode ( bool set )
  void	setDrawBase ( bool drawTheBase )
  void	setElideMode ( Qt::TextElideMode )
  void	setExpanding ( bool enabled )
  void	setIconSize ( const QSize & size )
  void	setMovable ( bool movable )
  void	setSelectionBehaviorOnRemove ( SelectionBehavior behavior )
  void	setShape ( Shape shape )
  void	setTabButton ( int index, ButtonPosition position, QWidget * widget )
  void	setTabData ( int index, const QVariant & data )
  void	setTabEnabled ( int index, bool enabled )
  void	setTabIcon ( int index, const QIcon & icon )
  void	setTabText ( int index, const QString & text )
  void	setTabTextColor ( int index, const QColor & color )
  void	setTabToolTip ( int index, const QString & tip )
  void	setTabWhatsThis ( int index, const QString & text )
  void	setTabsClosable ( bool closable )
  void	setUsesScrollButtons ( bool useButtons )
  Shape	shape () const
  int	tabAt ( const QPoint & position ) const
  QWidget *	tabButton ( int index, ButtonPosition position ) const
  QVariant	tabData ( int index ) const
  QIcon	tabIcon ( int index ) const
  QRect	tabRect ( int index ) const
  QString	tabText ( int index ) const
  QColor	tabTextColor ( int index ) const
  QString	tabToolTip ( int index ) const
  QString	tabWhatsThis ( int index ) const
  bool	tabsClosable () const
  bool	usesScrollButtons () const