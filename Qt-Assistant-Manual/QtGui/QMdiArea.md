# QMdiArea

> 继承关系：QMdiArea->QAbstractScrollArea->QFrame->QWidget

## 1.Public Types

- `enum AreaOption { DontMaximizeSubWindowOnActivation }`

  `flags AreaOptions`

  该枚举描述了用于自定义QMdiArea行为的选项，值为`QMdiArea::DontMaximizeSubWindowOnActivation`

- `enum ViewMode { SubWindowView, TabbedView }`

  该枚举描述了该区域的查看模式； 即子窗口的显示方式。

  值为：

  - `QMdiArea::SubWindowView`

    显示带有窗口框架的子窗口（默认)

  - `QMdiArea::TabbedView`

    在选项卡栏中显示带有选项卡的子窗口。

- `enum WindowOrder { CreationOrder, StackingOrder, ActivationHistoryOrder }`

  - `QMdiArea::CreationOrder`

    窗口按其创建顺序返回。

  - `QMdiArea::StackingOrder`

    窗口按其堆叠顺序返回，最上面的窗口在列表的最后。

  - `QMdiArea::ActivationHistoryOrder`

    窗口将按照它们被激活的顺序返回。

## 2.Properties

- `activationOrder : WindowOrder`

  此属性保存子窗口列表的排序条件
  此属性为subWindowList（）返回的子窗口列表指定排序条件。 默认情况下，这是窗口创建顺序。

- `background : QBrush`

  此属性保存工作区的背景画笔
  此属性为工作区本身设置背景画笔。 默认情况下，它是灰色，但可以是任何画笔（例如颜色，渐变或像素图）。

- `documentMode : bool`

  此属性保存是否在选项卡式视图模式下将选项卡栏设置为文档模式。
  默认情况下禁用文档模式。

- `tabPosition : QTabWidget::TabPosition`

  此属性保存选项卡式视图模式下选项卡的位置。
  QTabWidget :: TabPosition枚举描述了此属性的可能值：North、South、West、East四种位置

- `tabShape : QTabWidget::TabShape`

  此枚举类型定义选项卡的形状：

  - `QTabWidget::Rounded`这些选项卡以圆形外观绘制。 这是默认形状。
  - `QTabWidget::Triangular`这些选项卡以三角形外观绘制。

- `tabsClosable : bool`

  此属性保存选项卡栏是否应在选项卡式视图模式下在每个选项卡上放置关闭按钮。
  **默认情况下，标签无法关闭**。

- `tabsMovable : bool`

  此属性保存用户是否可以在选项卡式视图模式下在选项卡区域内移动选项卡。
  **选项卡默认情况下不可移动**。

- `viewMode : ViewMode`

  此属性保存子窗口在QMdiArea中的显示方式。
  **默认情况下，SubWindowView用于显示子窗口**。

## 3.Public Functions

- `QMdiSubWindow *activeSubWindow() const`

  返回指向**当前活动子窗口**的指针。 如果当前没有窗口处于活动状态，则返回nullptr。
  就窗口状态(`Qt::WindowState`)而言，子窗口被视为顶级窗口，即，**如果MDI区域之外的窗口小部件为活动窗口，则没有子窗口将处于活动状态**。 请注意，如果MDI区域所在的窗口中的小部件获得焦点，则该窗口将被激活。

  窗口状态有以下几种：

  - `Qt::WindowNoState`

    窗口未设置状态（处于正常状态）。

  - `Qt::WindowMinimized`

    窗口被最小化（即图标化）。

  - `Qt::WindowMaximized`

    窗口将最大化，并在其周围具有框架。

  - `Qt::WindowFullScreen`

    窗口充满整个屏幕，周围没有任何框架。

  - `Qt::WindowActive`

    该窗口是活动窗口，即它具有键盘焦点。

- `QList<QMdiSubWindow *> subWindowList(QMdiArea::WindowOrder order = CreationOrder) const`

  返回MDI区域中所有子窗口的列表。`enum QMdiArea::WindowOrder`窗口顺序有以下几种：

  - `QMdiArea::CreationOrder`

    将窗口按插入到工作区中的顺序排序，这是默认设置。

  - `QMdiArea::StackingOrder`

    窗口将按其堆叠顺序列出，最上面的窗口是列表中的最后一项。

  - `QMdiArea::ActivationHistoryOrder`

    根据窗口的近期激活历史记录列出窗口。

## 4.Reimplemented Public Functions

## 5.Public Slots

## 6.Signals

`void subWindowActivated(QMdiSubWindow *window)`

窗口激活后，QMdiArea发出此信号。 **当window为nullptr时，QMdiArea刚刚停用了其最后一个活动窗口，并且工作空间上没有活动窗口**。

## 7.Reimplemented Protected Functions

## 8.Protected Slots

## 9.Detailed Description

- 