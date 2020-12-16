# QTabWidget

继承关系：`QTabWidget`->`QWidget`

## 1.Public Types

- enum TabPosition { North, South, West, East }

  此枚举类型定义QTabWidget在何处绘制选项卡行：

  | Constant          | Value | Description                |
  | ----------------- | ----- | -------------------------- |
  | QTabWidget::North | 0     | 这些选项卡绘制在页面上方。 |
  | QTabWidget::South | 1     | 这些选项卡绘制在页面下方。 |
  | QTabWidget::West  | 2     | 这些选项卡绘制在页面左边。 |
  | QTabWidget::East  | 3     | 这些选项卡绘制在页面右边。 |

  

- enum TabShape { Rounded, Triangular }

  此枚举类型定义选项卡的形状：

  | Constant               | Value | Description                               |
  | ---------------------- | ----- | ----------------------------------------- |
  | QTabWidget::Rounded    | 0     | 这些选项卡以圆形外观绘制。 这是默认形状。 |
  | QTabWidget::Triangular | 1     | 这些选项卡以三角形外观绘制。              |

  

## 2.Properties

- count : const int

  此属性保存选项卡栏中的选项卡数
  默认情况下，此属性的值为0。

- currentIndex : int

  此属性保存当前选项卡页面的索引位置。

  如果没有当前小部件，则当前索引为-1。

  默认情况下，此属性包含值-1，因为在窗口小部件中最初没有选项卡。

- **documentMode : bool**

  此属性保存选项卡小部件是否以适合文档页面的模式呈现。 这与macOS上的文档模式相同。

  设置此属性后，不会呈现选项卡小部件框架。 此模式对于显示文档类型页面很有用，

  该页面涵盖了大多数选项卡小部件区域。

- elideMode : Qt::TextElideMode

  如何在标签栏中隐藏文本

  此属性控制在没有足够的空间来显示给定标签栏大小的情况下如何删除项目。

  默认情况下，该值取决于样式。

- iconSize : QSize

  此属性保存选项卡栏中图标的大小

  默认值取决于样式。 这是图标的最大大小。 如果图标较小，则不会按比例放大。

- **movable : bool**

  此属性保存用户是否可以在标签栏区域内移动标签。
  默认情况下，此属性为false。

- tabBarAutoHide : bool

  如果为true，则选项卡栏包含少于2个选项卡时将自动隐藏。

  默认情况下，此属性为false。

- tabPosition : TabPosition

  此属性保存此选项卡小部件中选项卡的位置。

  TabPosition枚举描述了此属性的可能值。

  默认情况下，此属性设置为North。

- tabShape : TabShape

  此属性保存此选项卡小部件中选项卡的形状。

  此属性的可能值为QTabWidget :: Rounded（默认）或QTabWidget :: Triangular。

- **tabsClosable : bool**

  此属性保存是否将关闭按钮自动添加到每个选项卡。

- usesScrollButtons : bool

  此属性保存选项卡栏包含多个选项卡时是否应使用按钮滚动选项卡。

  当选项卡栏上的选项卡太多时，选项卡栏可以选择扩大其大小，也可以选择添加按钮来滚动选项卡。

  默认情况下，该值取决于样式。

## 3.Public Functions

- QTabWidget(QWidget *parent = nullptr)
- virtual ~QTabWidget()
- int addTab(QWidget *page, const QString &label)
- int addTab(QWidget *page, const QIcon &icon, const QString &label)
- void clear()
- QWidget *cornerWidget(Qt::Corner corner = Qt::TopRightCorner) const
- int count() const
- int currentIndex() const
- QWidget *currentWidget() const
- bool documentMode() const
- Qt::TextElideMode elideMode() const
- QSize iconSize() const
- int indexOf(QWidget *w) const
- int insertTab(int index, QWidget *page, const QString &label)
- int insertTab(int index, QWidget *page, const QIcon &icon, const QString &label)
- bool isMovable() const
- bool isTabEnabled(int index) const
- bool isTabVisible(int index) const
- void removeTab(int index)
- void setCornerWidget(QWidget *widget, Qt::Corner corner = Qt::TopRightCorner)
- void setDocumentMode(bool set)
- void setElideMode(Qt::TextElideMode mode)
- void setIconSize(const QSize &size)
- void setMovable(bool movable)
- void setTabBarAutoHide(bool enabled)
- void setTabEnabled(int index, bool enable)
- void setTabIcon(int index, const QIcon &icon)
- void setTabPosition(QTabWidget::TabPosition position)
- void setTabShape(QTabWidget::TabShape s)
- void setTabText(int index, const QString &label)
- void setTabToolTip(int index, const QString &tip)
- void setTabVisible(int index, bool visible)
- void setTabWhatsThis(int index, const QString &text)
- void setTabsClosable(bool closeable)
- void setUsesScrollButtons(bool useButtons)
- QTabBar *tabBar() const
- bool tabBarAutoHide() const
- QIcon tabIcon(int index) const
- QTabWidget::TabPosition tabPosition() const
- QTabWidget::TabShape tabShape() const
- QString tabText(int index) const
- QString tabToolTip(int index) const
- QString tabWhatsThis(int index) const
- bool tabsClosable() const
- bool usesScrollButtons() const
- QWidget *widget(int index) const

## 4.Reimplemented Public Functions

- virtual bool hasHeightForWidth() const override
- virtual int heightForWidth(int width) const override
- virtual QSize minimumSizeHint() const override
- virtual QSize sizeHint() const override

## 5.Public Slots

- `void setCurrentIndex(int index)`

- `void setCurrentWidget(QWidget *widget)`

  使widget成为当前小部件。 使用的窗口小部件必须是此选项卡窗口小部件中的页面。

要实现按下不同按钮显示不同QTabWidget页面的功能，可以编写按钮的clicked()槽函数，在槽函数内利用`setCurrentIndex()`来设置QTabWidget显示的页面。

要实现QTabWidget页面切换，`QRadioButton`按钮随页面切换选中不同按钮的功能，可以编写当前QTabWidget的currentChanged()信号的槽函数，在里面通过传入的当前页面索引，设置不同的选中按钮。

## 6.Signals

- `void currentChanged(int index)`

  当前页面索引index更改时，将发出此信号。 该参数是新的当前页面索引位置，如果没有新的位置，则返回-1（例如，如果QTabWidget中没有窗口小部件）

- `void tabBarClicked(int index)`

- `void tabBarDoubleClicked(int index)`

- `void tabCloseRequested(int index)`

## 7.Protected Functions

- void initStyleOption(QStyleOptionTabWidgetFrame *option) const
- void setTabBar(QTabBar *tb)
- virtual void tabInserted(int index)
- virtual void tabRemoved(int index)

## 8.Reimplemented Protected Functions

- virtual void changeEvent(QEvent *ev) override
- virtual bool event(QEvent *ev) override
- virtual void keyPressEvent(QKeyEvent *e) override
- virtual void paintEvent(QPaintEvent *event) override
- virtual void resizeEvent(QResizeEvent *e) override
- virtual void showEvent(QShowEvent *) override

## 9.Detailed Description

选项卡小部件提供了一个选项卡栏（请参阅QTabBar）和一个“页面区域”，该区域用于显示与每个选项卡相关的页面。 默认情况下，选项卡栏显示在页面区域上方，但是可以使用不同的配置（请参见TabPosition）。 每个选项卡都与一个不同的小部件（称为页面）相关联。 页面区域中仅显示当前页面。 其他所有页面均被隐藏。 用户可以通过单击其选项卡或按Alt +字母快捷键（如果有的话）来显示其他页面。

使用QTabWidget的正常方法是执行以下操作：

- 创建一个QTabWidget。
- 在选项卡对话框中为每个页面创建一个QWidget，但不要为其指定父窗口小部件。
- 将子窗口小部件插入页面窗口小部件，使用布局将它们正常放置。
- 调用addTab（）或insertTab（）将页面小部件放入选项卡小部件中，为每个选项卡提供合适的标签以及可选的键盘快捷键。

选项卡的位置由tabPosition定义，其形状由tabShape定义。

用户选择页面时，将发出currentChanged（）信号。

当前页面索引可以作为currentIndex（）使用，currentPage（）是当前页面小部件。您可以使用widget（）检索具有给定索引的页面小部件的指针，并可以使用indexOf（）查找小部件的索引位置。使用setCurrentWidget（）或setCurrentIndex（）显示特定页面。
您可以使用setTabText（）或setTabIcon（）更改选项卡的文本和图标。可以使用removeTab（）删除选项卡及其相关页面。

每个选项卡在任何给定时间都是启用或禁用的（请参阅setTabEnabled（））。如果启用了选项卡，则将正常绘制选项卡文本，并且用户可以选择该选项卡。如果禁用该选项卡，则该选项卡将以其他方式绘制，并且用户无法选择该选项卡。请注意，即使某个选项卡被禁用，该页面仍然可见，例如，如果所有选项卡都被禁用。

**选项卡小部件可能是拆分复杂对话框的一种很好的方法。一种替代方法是使用QStackedWidget**，为此您提供了一些在页面之间导航的方法，例如QToolBar或QListWidget。

QTabWidget中的大多数功能由QTabBar（在顶部，提供选项卡）和QStackedWidget（在大部分区域，用于组织各个页面）中提供。