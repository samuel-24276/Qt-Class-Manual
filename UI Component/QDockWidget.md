# QDockWidget

继承关系：`QDockWidget`->`QWidget`->`QObject` and `QPaintDevice`

## 1.Public Types

- enum DockWidgetFeature { DockWidgetClosable, DockWidgetMovable, DockWidgetFloatable, DockWidgetVerticalTitleBar, AllDockWidgetFeatures, NoDockWidgetFeatures }

- flags DockWidgetFeatures

  | Constant                                | Value                                                        | Description                                                  |
  | --------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | QDockWidget::DockWidgetClosable         | 0x01                                                         | 停靠小部件可以关闭。 在某些系统上，dock小部件在浮动时始终具有关闭按钮（例如，在MacOS 10.5上）。 |
  | QDockWidget::DockWidgetMovable          | 0x02                                                         | 用户可以在扩展坞之间移动扩展坞小部件。                       |
  | QDockWidget::DockWidgetFloatable        | 0x04                                                         | 停靠小部件可以与主窗口分离，并作为独立窗口浮动。             |
  | QDockWidget::DockWidgetVerticalTitleBar | 0x08                                                         | 停靠小部件在其左侧显示垂直标题栏。 这可用于增加QMainWindow中的垂直空间。 |
  | QDockWidget::AllDockWidgetFeatures      | DockWidgetClosable \| DockWidgetMovable \| DockWidgetFloatable | （不建议使用）可以关闭，移动和浮动Dock小部件。 由于将来的发行版中可能会添加新功能，因此，如果使用此标志，则停靠小部件的外观和行为可能会更改。 请改为指定各个标志。 |
  | QDockWidget::NoDockWidgetFeatures       | 0x00                                                         | 停靠小部件无法关闭，移动或浮动。                             |

  DockWidgetFeatures类型是QFlags <DockWidgetFeature>的typedef。 它存储DockWidgetFeature值的或组合。

## 2.Properties

- allowedAreas : Qt::DockWidgetAreas

  areas where the dock widget may be placed

  The default is **`Qt::AllDockWidgetAreas`**.

  `enum Qt::DockWidgetArea`
  `flags Qt::DockWidgetAreas`

  停靠窗口的枚举类型主要有以下几种：

  | Constant                    | Value               |
  | --------------------------- | ------------------- |
  | `Qt::LeftDockWidgetArea`    | 0x1                 |
  | ` Qt::RightDockWidgetArea`  | 0x2                 |
  | `Qt::TopDockWidgetArea`     | 0x4                 |
  | ` Qt::BottomDockWidgetArea` | 0x8                 |
  | `Qt::AllDockWidgetAreas`    | DockWidgetArea_Mask |
  | ` Qt::NoDockWidgetArea`     | 0                   |

  DockWidgetAreas类型是QFlags <DockWidgetArea>的typedef。 它存储DockWidgetArea值的OR组合。

  `AllDockWidgetAreas`和`NoDockWidgetArea`在实际运用中算是无效参数。

- features : DockWidgetFeatures

  此属性保存停靠小部件是否可移动，可关闭和可浮动
  默认情况下，此属性设置为DockWidgetClosable，DockWidgetMovable和DockWidgetFloatable的组合。

- floating : bool

  此属性保存停靠小部件是否浮动
  浮动坞窗口小部件作为独立窗口显示在其父QMainWindow的“顶部”，而不是停靠在QMainWindow中。
  默认情况下，此属性为true。
  当此属性更改时，将发出topLevelChanged（）信号。

- windowTitle : QString 

  此属性保存停靠小部件标题（标题）
  默认情况下，此属性包含一个空字符串。

## 3.Public Functions

- QDockWidget(QWidget *parent = nullptr, Qt::WindowFlags flags = Qt::WindowFlags())

- QDockWidget(const QString &title, QWidget *parent = nullptr, Qt::WindowFlags flags = Qt::WindowFlags())

- virtual ~QDockWidget()

- Qt::DockWidgetAreas allowedAreas() const

- QDockWidget::DockWidgetFeatures features() const

- bool isAreaAllowed(Qt::DockWidgetArea area) const

  如果可以将该停靠小部件放置在给定区域中，则返回true；否则返回false。

- bool isFloating() const

  返回停靠小部件的浮动状态，浮动返回true，停靠返回false。

- void setAllowedAreas(Qt::DockWidgetAreas areas)

  设置停靠小部件停靠的位置。

- void setFeatures(QDockWidget::DockWidgetFeatures features)

  设置停靠小部件的特性：浮动、移动、关闭。

- void setFloating(bool floating)

  设置停靠小部件的浮动状态。

- **void setTitleBarWidget(QWidget *widget)**

  **将任意窗口小部件设置为停靠窗口小部件的标题栏**。 如果小部件为nullptr，则将移除但不会删除先前在停靠小部件上设置的所有自定义标题栏小部件，而是使用默认标题栏。

  如果设置了标题栏小部件，则QDockWidget浮动时将不使用本机窗口装饰。

  以下是实现自定义标题栏的一些技巧：

  - 标题栏小部件未明确处理的鼠标事件必须通过调用QMouseEvent :: ignore（）来忽略。 然后，这些事件传播到QDockWidget父级，该父级以常规方式处理它们，拖动标题栏时移动，双击则停靠和取消停放，等等。

  - 在QDockWidget上设置DockWidgetVerticalTitleBar时，标题栏小部件将相应地重新放置。 在resizeEvent（）中，标题栏应检查其应采用的方向：

    

    ```c++
    QDockWidget *dockWidget = qobject_cast<QDockWidget*>(parentWidget());
     if (dockWidget->features() & QDockWidget::DockWidgetVerticalTitleBar) {
         // I need to be vertical
     } else {
         // I need to be horizontal
     }
    ```

  - **标题栏小部件必须具有有效的QWidget :: sizeHint（）和QWidget :: minimumSizeHint（）。 这些功能应考虑标题栏的当前方向**。

  - 无法从停靠小部件中删除标题栏。 但是，通过将默认构造的QWidget设置为标题栏小部件，可以实现类似的效果。

  使用上面显示的qobject_cast（），标题栏小部件可以完全访问其父QDockWidget。 因此，它可以响应于用户动作而执行诸如对接和隐藏的操作。

- **void setWidget(QWidget *widget)**

  将停靠小部件的小部件设置为widget。

  如果添加widget时可以看到停靠小部件，则必须显式显示（）。

  注意，**在调用此函数之前，必须添加小部件的布局。 如果没有，则小部件将不可见**。

- QWidget *titleBarWidget() const

  返回在QDockWidget上设置的自定义标题栏小部件，如果未设置自定义标题栏，则返回nullptr。

- QAction *toggleViewAction() const

  返回可以添加到菜单和工具栏的可检查操作，以便用户可以显示或关闭此Dock小部件。

  操作的文本设置为停靠小部件的窗口标题。

  注意：该操作不能用于以编程方式显示或隐藏停靠小部件。 为此使用可见属性。

- QWidget *widget() const

  返回停靠小部件的小部件。 如果尚未设置小部件，则此函数返回零。

## 4.Signals

- void allowedAreasChanged(Qt::DockWidgetAreas allowedAreas)

  当allowedAreas属性更改时，将发出此信号。 allowedAreas参数给出属性的新值。

  注意：属性allowedAreas的通知程序信号。

- void dockLocationChanged(Qt::DockWidgetArea area)

  当停靠小部件移至另一个停靠区或移至其当前停靠区中的其他位置时，将发出此信号。 当以编程方式移动停靠小部件或用户将其拖到新位置时，会发生这种情况。

- void featuresChanged(QDockWidget::DockWidgetFeatures features)

  当features属性更改时，将发出此信号。 features参数提供属性的新值。

  注意：属性功能的通知程序信号。

- void topLevelChanged(bool topLevel)

  当浮动属性改变时，该信号被发射。 如果停靠小部件现在处于浮动状态，则topLevel参数为true；否则为false。 

- void visibilityChanged(bool visible)

  当停靠小部件可见（或不可见）时，将发出此信号。 当窗口小部件被隐藏或显示时，以及将其停靠在选项卡式停靠区域中且其选项卡变为选中或未选中状态时，都会发生这种情况。

## 5.Protected Functions

- void initStyleOption(QStyleOptionDockWidget *option) const

  使用此QDockWidget中的值初始化选项。 当子类需要QStyleOptionDockWidget，但又不想自己填写所有信息时，此方法很有用。

## 6.Reimplemented Protected Functions

- virtual void changeEvent(QEvent *event) override
- virtual void closeEvent(QCloseEvent *event) override
- virtual bool event(QEvent *event) override
- virtual void paintEvent(QPaintEvent *event) override

## 7.Detailed Description

QDockWidget提供了停靠小部件的概念，也称为工具选项板或实用程序窗口。 停靠窗口是放置在QMainWindow中中央窗口小部件周围的停靠窗口小部件区域中的辅助窗口。

停靠窗口可以在其当前区域内移动，移至新区域并由最终用户浮动（例如，取消停靠）。 QDockWidget API允许程序员限制Dock小部件的移动，浮动和关闭功能以及可以放置它们的区域。

### Appearance

**QDockWidget由标题栏和内容区域组成**。 标题栏显示停靠小部件窗口标题，浮动按钮和关闭按钮。 根据QDockWidget的状态，浮动和关闭按钮可能被禁用或根本不显示。

标题栏和按钮的外观取决于所使用的样式。

**QDockWidget充当其子窗口小部件的包装，该子窗口小部件由setWidget（）设置**。 自定义大小提示，最小和最大大小以及大小策略应在子窗口小部件中实现。 QDockWidget将尊重它们，调整其自身的约束以包括框架和标题。 **不应在QDockWidget本身上设置大小限制，因为它们会根据是否停靠而改变； 停靠的QDockWidget没有框架和较小的标题栏**。