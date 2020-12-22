# Qt Style Sheets Reference

Qt样式表支持各种属性，伪状态和子控件，从而可以自定义小部件的外观。

> QSS设置边框border属性是**上右下左**，设置布局的四周Margin即setContentMargins()是**左上右下**。

## 1.List of Stylable Widgets部件支持样式

下表列出了可以使用样式表自定义的Qt小部件：

| Widget              | How to Style                                                 |
| ------------------- | ------------------------------------------------------------ |
| QLabel              | 支持box model。 **不支持：hover伪状态**。<br/>从4.3开始，在QLabel上设置样式表会自动将QFrame :: frameStyle属性设置为QFrame :: StyledPanel。<br/>有关示例（请参见自定义QFrame）（QLabel源自QFrame）。 |
| QPushButton         | 支持box model。 **支持：default，：flat，：checked伪状态**。<br/>对于带有菜单的QPushButton，菜单指示器使用:: menu-indicator子控件设置样式。 可以使用：open和：closed伪状态来自定义可检查按钮的外观。<br/>警告：如果仅在QPushButton上设置背景色，则除非将border属性设置为某个值，否则背景可能不会出现。 这是因为，默认情况下，QPushButton绘制一个原生边框，该边框与背景颜色完全重叠。 例如，<br/>  `QPushButton { background-color: red; border: none; }`<br/>有关示例，请参见自定义QPushButton。 |
| QRadioButton        | 支持box model。 可以使用:: indicator子控件设置检查指示器的样式。 默认情况下，指示器放置在窗口小部件的“内容”矩形的左上角。<br/>间隔属性指定检查指示符和文本之间的间隔。<br/>有关示例，请参见自定义QRadioButton。 |
| QCheckBox           | 支持box model。 可以使用**:: indicator子控件**设置检查指示器的样式。 默认情况下，指示器放置在窗口小部件的“内容”矩形的左上角。<br/>interval属性指定检查指示符和文本之间的间距。<br/>有关示例，请参见自定义QCheckBox。 |
| QLineEdit           | 支持box model。<br/>所选项目的颜色和背景分别使用selection-color和selection-background-color设置样式。<br/>可以使用lineedit-password-character属性设置密码字符的样式。<br/>有关示例，请参见自定义QLineEdit。 |
| QTextEdit           | 支持box model。<br/>所选文本的颜色和背景分别使用selection-color和selection-background-color设置样式。<br/>请参阅QAbsractScrollArea以设置可滚动背景的样式。 |
| QToolButton         | 支持box model。<br/>如果QToolButton带有菜单，则::menu-indicator可用于设置指示器样式。 默认情况下，菜单指示器位于窗口小部件的填充矩形的右下角。<br/>如果QToolButton处于QToolButton :: MenuButtonPopup模式，则:: menu-button子控件用于绘制菜单按钮。 :: menu-arrow子控件用于在菜单按钮内部绘制菜单箭头。 默认情况下，它位于菜单按钮子控件的“内容”矩形的中心。<br/>当QToolButton显示箭头时，将使用:: up-arrow，:: down-arrow，:: left-arrow和:: right-arrow子控件。<br/>警告：如果仅在QToolButton上设置背景色，则除非将border属性设置为某个值，否则背景不会显示。 这是因为，默认情况下，QToolButton绘制一个原生边框，该边框与背景颜色完全重叠。 例如， |
| QMenu               | 支持box model。<br/>单个项目使用:: item子控件设置样式。 除了通常支持的伪状态外，item子控件还支持：selected，：default，：exclusive和非独占伪状态。<br/>可检查菜单项的指示器使用:: indicator子控件设置样式。<br/>分隔符使用:: separator子控件设置样式。<br/>对于带有子菜单的项目，箭头标记使用right-arrow和left-arrow设置样式。<br/>滚动器使用:: scroller设置样式。<br/>撕下使用:: tearoff设置样式。<br/>有关示例，请参见自定义QMenu。 |
| QComboBox           | 组合框周围的框架可以使用box model设置样式。 可以使用:: drop-down子控件设置**下拉按钮**的样式。 默认情况下，下拉按钮位于小部件的填充矩形的右上角。 可以使用:: down-arrow子控件设置**下拉按钮内的箭头标记**的样式。 默认情况下，箭头位于下拉子控件的内容矩形的中心。<br/>有关示例，请参见自定义QComboBox。 |
| QMessageBox         | messagebox-text-interaction-flags属性可用于更改与消息框中的文本的交互 |
| QToolBox            | 支持box model。<br/>可以使用:: tab子控件设置各个选项卡的样式。 选项卡支持：only-one，：first，：last，：middle，：previous-selected，：next-selected，：selected伪状态。 |
| QToolTip            | 支持盒子模型。 opacity属性控制工具提示的不透明度。<br/>有关示例，请参见自定义QFrame（QToolTip是QFrame）。 |
| QMenuBar            | 支持box model。 间隔属性指定菜单项之间的间隔。 单个项目使用:: item子控件设置样式。<br/>警告：在Qt / Mac上运行时，菜单栏通常嵌入到系统范围的菜单栏中。 在这种情况下，样式表将无效。<br/>有关示例，请参见自定义QMenuBar。 |
| QProgressBar        | 支持box model。 可以使用**:: chunk子控件设置进度条的样式**。 该块将显示在窗口小部件的“内容”矩形上。<br/>如果进度条显示文本，请使用text-align属性定位文本。<br/>不确定进度条具有：indeterminate伪状态集。<br/>有关示例，请参见自定义QProgressBar。 |
| QScrollBar          | 支持box model。小部件的内容矩形被视为滑块在其上移动的凹槽。 QScrollBar的范围（即宽度或高度取决于方向）分别使用width或height属性设置。要确定方向，请使用：horizontal和：vertical伪状态。<br/>可以使用:: handle子控件设置滑块的样式。设置最小宽度或最小高度会根据方向为滑块提供尺寸限制。<br/>:: add-line子控件可用于设置按钮样式以添加行。默认情况下，添加行子控件位于小部件的“边框”矩形的右上角。取决于方向：:: right-arrow或:: down-arrow。默认情况下，箭头位于add-line子控件的“内容”矩形的中心。<br/>:: sub-line子控件可用于设置按钮样式以减去一行。默认情况下，子行子控件位于小部件的“边框”矩形的右下角。取决于方向：:: left-arrow或:: up-arrow。默认情况下，箭头放置在sub-line子控件的“内容”矩形的中心。<br/>:: sub-page子控件可用于设置减去页面的滑块区域的样式。 :: add-page子控件可用于设置添加页面的滑块区域的样式。<br/>有关示例，请参见自定义QScrollBar。 |
| QStatusBar          | 仅支持background属性。 单个项目的框架可以使用:: item子控件设置样式。<br/>有关示例，请参见自定义QStatusBar。 |
| QTabBar             | 单个选项卡可以使用:: tab子控件设置样式。 使用:: close-button关闭按钮选项卡支持：only-one，：first，：last，：middle，：previous--selected，：next-selected和：selected伪状态。<br/>：top，：left，：right，：bottom伪状态取决于选项卡的方向。<br/>所选状态的重叠选项卡是使用负边距或绝对位置方案创建的。<br/>QTabBar的撕裂指示器使用:: tear子控件设置样式。<br/>**QTabBar为其滚动条使用了两个QToolButtons，可以使用QTabBar QToolButton选择器设置样式**。 要指定滚动按钮的宽度，请使用:: scroller子控件。<br/>QTabBar中选项卡的对齐方式是使用alignment属性设置样式的。<br/>**警告**：要更改QTabWidget在QTabWidget中的位置，请使用标签栏子控件（并设置subcontrol-position）。<br/>有关示例，请参见自定义QTabBar。 |
| QToolBar            | 支持box model。<br/>：top，：left，：right，：bottom伪状态取决于工具栏所在的区域。<br/>：first，：last，：middle，：only一个伪状态指示工具栏在线组中的位置（请参见QStyleOptionToolBar :: positionWithinLine）。<br/>QToolBar的分隔符使用:: separator子控件设置样式。<br/>使用:: handle子控件设置手柄（用于移动工具栏）的样式。<br/>有关示例，请参见自定义QToolBar。 |
| QMainWindow         | 支持分隔符的样式<br/>使用QDockWidget时，QMainWindow中的分隔符使用:: separator子控件设置样式。<br/>有关示例，请参见自定义QMainWindow。 |
| QDialog             | 仅支持background，background-clip和background-origin属性。<br/>警告：确保为自定义窗口小部件定义了Q_OBJECT宏。 |
| QDialogButtonBox    | 可以使用button-layout属性更改按钮的布局。                    |
|                     |                                                              |
|                     |                                                              |
| QFrame              | 支持box model。<br/>从4.3开始，在QLabel上设置样式表会自动将QFrame :: frameStyle属性设置为QFrame :: StyledPanel。<br/>有关示例，请参见自定义QFrame。 |
| QGroupBox           | 支持box model。 标题可以使用:: title子控件设置样式。 默认情况下，标题的位置取决于QGroupBox :: textAlignment。<br/>对于可检查的QGroupBox，标题包括检查指示符。 指示器使用:: indicator子控件设置样式。 间距属性可用于控制文本和指示符之间的间距。<br/>有关示例，请参见自定义QGroupBox。 |
| QAbstractScrollArea | 支持box model。<br/>QAbstractScrollArea的所有派生版本，包括QTextEdit和QAbstractItemView（所有项目视图类），都**支持使用背景附件进行可滚动的背景**。 将背景附件设置为固定可提供不随视口（viewport）滚动的背景图像。 将背景附件设置为滚动，则在滚动条移动时滚动背景图像。<br/>有关示例，请参见自定义QAbstractScrollArea。 |
| QSizeGrip           | 支持宽度，高度和图像属性。<br/>有关示例，请参见自定义QSizeGrip。 |
| QSlider             | 支持box model。 对于水平Slider，必须提供min-width和height属性。 对于垂直Slider，必须提供min-height和width属性。<br/>滑块的凹槽使用:: groove设置样式。 默认情况下，凹槽位于窗口小部件的“内容”矩形中。 滑块的拇指使用:: handle子控件设置样式。 子控件在凹槽子控件的“内容”矩形中移动。<br/>有关示例，请参见自定义QSlider。 |
| QTabWidget          | 选项卡小部件的框架使用:: pane子控件设置样式。 左和右角分别使用:: left-corner和:: right-corner设置样式。 使用:: tab-bar子控件可以控制选项卡栏的位置。<br/>默认情况下，子控件在QWindowsStyle中具有QTabWidget的位置。 要将QTabBar放在中心，请设置选项卡栏子控件的子控件位置。<br/>：top，：left，：right，：bottom伪状态取决于选项卡的方向。<br/>有关示例，请参见自定义QTabWidget。 |
| QTableWidget        | See QTableView.                                              |
| QDockWidget         | 支持**停靠时标题栏和标题栏按钮的样式**。<br/>可以使用border属性设置停靠窗口小部件边框的样式。 :: title子控件可用于自定义标题栏。 关闭和浮动按钮分别相对于:: title子控件使用:: close-button和:: float-button定位。<br/>当标题栏为垂直时，将设置：vertical伪类。 另外，根据QDockWidget :: DockWidgetFeature，设置：closesable，：floatable和：movable伪状态。<br/>**注意**：使用QMainWindow :: separator设置调整大小手柄的样式。<br/>警告：取消QDockWidget时，样式表无效，因为Qt退出时Qt使用本机顶级窗口。<br/>有关示例，请参见自定义QDockWidget。 |
| QTreeWidget         | See QTreeView.                                               |
| QWidget             | 仅支持background，background-clip和background-origin属性。<br/>如果您是QWidget的子类，则需要为您的自定义QWidget提供paintEvent，如下所示：<br/>  void CustomWidget :: paintEvent（QPaintEvent *）<br/>  {<br/>      QStyleOption opt;<br/>      opt.init（this）;<br/>      QPainter p（this）;<br/>      style（）-> drawPrimitive（QStyle :: PE_Widget，＆opt，＆p，this）;<br/>  }<br/>如果未设置样式表，则以上代码为空操作。<br/>警告：确保为自定义窗口小部件定义了Q_OBJECT宏。 |
| QTreeView           | 支持box model。 启用交替行颜色后，可以使用alternate-background-color属性设置交替颜色的样式。<br/>所选项目的颜色和背景分别使用selection-color和selection-background-color设置样式。<br/>选择行为由show-decoration-selected属性控制。<br/>可以使用:: branch子控件设置树形视图的分支的样式。 :: branch子控件支持：open，：closed，：has-sibling和：has-children伪状态。<br/>使用:: item子控件可以对QTreeView中的项目进行更精细的控制。<br/>请参阅QAbsractScrollArea以设置可滚动背景的样式。<br/>有关对分支进行样式设置的示例，请参见自定义QTreeView。 |
| QColumnView         | 可以使用image属性设置**握柄**的样式。 可以使用:: left-arrow子控件和:: right-arrow子控件设置**箭头指示器**的样式。 |
| QHeaderView         | 支持box model。 标题视图的各节使用:: section子控件设置样式。 子控件部分支持：middle，：first，：last，：only-one，：next-selected，：previous-selected，：selected和：checked**伪状态**。<br/>可以使用:: up-arrow和:: down-arrow子控件设置排序指示器中的样式。<br/>有关示例，请参见自定义QHeaderView。 |
| QListView           | 支持box model。 启用交替行颜色后，可以使用alternate-background-color属性设置交替颜色的样式。<br/>所选项目的颜色和背景分别使用**selection-color**和**selection-background-color**设置样式。<br/>选择行为由show-decoration-selected属性控制。<br/>使用:: item子控件可以对QListView中的项目进行更精细的控制。<br/>请参阅QAbsractScrollArea以设置可滚动背景的样式。<br/>有关示例，请参见自定义QListView。 |
| QDoubleSpinBox      | See QSpinBox.                                                |
| QDateEdit           | See QSpinBox.                                                |
| QTimeEdit           | See QSpinBox.                                                |
| QDateTimeEdit       | See QSpinBox.                                                |
| QSpinBox            | QSpinBox的框架可以使用box model设置样式。<br/>可以使用:: up-button和:: up-arrow子控件设置向上按钮和箭头的样式。 默认情况下，向上按钮位于小部件的“填充”矩形的右上角。 如果没有明确的尺寸，则它占据其参考矩形高度的一半。 向上箭头放置在向上按钮的“内容”矩形的中心。<br/>可以使用:: down-button和:: down-arrow子控件设置向下按钮和箭头的样式。 默认情况下，向下按钮位于小部件的“填充”矩形的右下角。 如果没有明确的尺寸，则它占据其参考矩形高度的一半。 底部箭头位于底部按钮的“内容”矩形的中心。<br/>有关示例，请参见自定义QSpinBox。 |

## 2.List of Properties样式表属性列表

下表列出了Qt样式表支持的所有属性。 可以为属性指定哪些值取决于属性的类型。 除非另有说明，否则以下属性适用于所有小部件。 **标有星号*的属性特定于Qt**，并且在CSS2或CSS3中没有等效项。

| Property                                        | Type                                                | Description                                                  |
| ----------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| alternate-background-color                      | Brush                                               | QAbstractItemView子类中使用的*备用背景色*。<br/>如果未设置此属性，则默认值是为调色板的AlternateBase角色设置的任何值。<br/>例：<br/>QTreeView {<br/>     alternate-background-color: blue;<br/>     background: yellow;<br/> } |
| background                                      | Background                                          | 设置背景的简写形式。 等效于指定背景颜色，背景图像，背景重复和/或背景位置。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QDialog，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit，QToolTip和纯QWidgets支持此属性。<br/>例：<br/>QTextEdit { background: yellow }<br/>通常，需要设置类似于Qt :: BrushStyle中的样式的填充模式。 您可以对Qt :: SolidPattern，Qt :: RadialGradientPattern，Qt :: LinearGradientPattern和Qt :: ConicalGradientPattern使用background-color属性。 通过创建包含图案的背景图像，可以轻松实现其他图案。<br/>例：<br/>QLabel {<br/>     background-image: url(dense6pattern.png);<br/>     background-repeat: repeat-xy;<br/> } |
| background-color                                | Brush                                               | The background color used for the widget.<br/>Examples:<br/>QLabel { background-color: yellow }<br/> QLineEdit { background-color: rgb(255, 0, 0) } |
| background-image                                | Url                                                 | 小部件使用的背景图像。 **图像的半透明部分使背景色发光**。<br/>例：<br/>QFrame { background-image: url(:/images/hydro.png) } |
| background-repeat                               | Repeat                                              | 是否重复背景图像以及如何重复背景图像以填充背景矩形。<br/>如果未指定此属性，则在两个方向（重复）上重复背景图像。<br/>例：<br/>QFrame {<br/>     background: white url(:/images/ring.png);<br/>     background-repeat: repeat-y;<br/>     background-position: left;<br/> } |
| background-position                             | Alignment                                           | 背景图像在背景原点矩形内的对齐方式。<br/>如果未指定此属性，则对齐方式位于左上方。<br/>例：<br/>QFrame {<br/>     background: url(:/images/footer.png);<br/>     background-position: bottom left;<br/> } |
| background-attachment                           | Attachment                                          | 确定QAbstractScrollArea中的背景图像是相对于视口滚动还是固定的。 默认情况下，背景图像与视口一起滚动。<br/>例：<br/>QTextEdit {<br/>     background-image: url("leaves.png");<br/>     background-attachment: fixed;<br/> } |
| background-clip                                 | Origin                                              | **小部件的矩形**，在其中绘制背景。<br/>此属性指定将背景色和背景图像剪切到的矩形。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QDialog，QFrame，QGroupBox，QLabel，QPushButton，QRadioButton，QSplitter，QTextEdit，QToolTip和纯QWidgets支持此属性。<br/>**如果未指定此属性，则默认为border**。<br/>例：<br/>QFrame {<br/>     background-image: url(:/images/header.png);<br/>     background-position: top left;<br/>     background-origin: content;<br/>     background-clip: padding;<br/> } |
| background-origin                               | Origin                                              | **小部件的背景矩形**，与background-position和background-image结合使用。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QDialog，QFrame，QGroupBox，QLabel，QPushButton，QRadioButton，QSplitter，QTextEdit，QToolTip和纯QWidgets支持此属性。<br/>**如果未指定此属性，则默认值为padding**。<br/>例：<br/>QFrame {<br/>     background-image: url(:/images/header.png);<br/>     background-position: top left;<br/>     background-origin: content;<br/> } |
| border                                          | Border                                              | 用于设置小部件边框的简写符号。 等效于指定边框颜色，边框样式和/或边框宽度。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit，QToolTip和纯QWidgets支持此属性。<br/>例：<br/>QLineEdit { border: 1px solid white } |
| border-top                                      | Border                                              | 设置小部件顶部边框的简写形式。 等效于指定border-top-color，border-top-style和/或border-top-width。 |
| border-right                                    | Border                                              | 设置小部件右侧边框的简写形式。 等效于指定border-top-color，border-top-style和/或border-top-width。 |
| border-bottom                                   | Border                                              | 设置小部件底部边框的简写形式。 等效于指定border-top-color，border-top-style和/或border-top-width。 |
| border-left                                     | Border                                              | 设置小部件左侧边框的简写形式。 等效于指定border-top-color，border-top-style和/或border-top-width。 |
| border-color                                    | Box Colors                                          | 所有边框边缘的颜色。 等效于指定border-top-color，border-right-color，border-bottom-color和border-left-color。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit，QToolTip和纯QWidgets支持此属性。<br/>如果未指定此属性，则默认为颜色（即小部件的前景色）。<br/>例：<br/>QLineEdit {<br/>     border-width: 1px;<br/>     border-style: solid;<br/>     border-color: white;<br/> } |
| border-top-color                                | Brush                                               | 边框顶部边缘的颜色。                                         |
| border-right-color                              | Brush                                               | 边框右侧边缘的颜色。                                         |
| border-bottom-color                             | Brush                                               | 边框底部边缘的颜色。                                         |
| border-left-color                               | Brush                                               | 边框左侧边缘的颜色。                                         |
| border-image                                    | Border Image                                        | 用于填充边框的图像。 图像被切成九部分，并在必要时适当拉伸。 有关详细信息，请参见边框图像。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit和QToolTip支持此属性。<br/>另请参见border-color，border-style，border-width和Box模型。 |
| **border-radius**                               | Radius                                              | **边界角的半径**。 等效于指定border-top-left-radius，border-top-right-radius，border-bottom-right-radius和border-bottom-left-radius。<br/>边界半径将剪切元素的背景。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit和QToolTip支持此属性。<br/>如果未指定此属性，则默认为0。<br/>例：<br/>QLineEdit {<br/>     border-width: 1px;<br/>     border-style: solid;<br/>     border-radius: 4px;<br/> } |
| border-top-left-radius                          | Radius                                              | 边框左上角的半径。                                           |
| border-top-right-radius                         | Radius                                              | 边框右上角的半径。                                           |
| border-bottom-right-radius                      | Radius                                              | 边框右下角的半径。                                           |
| border-bottom-left-radius                       | Radius                                              | 边框左下角的半径。                                           |
| **border-style**                                | Border Style                                        | 所有边框边缘的样式。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit和QToolTip支持此属性。<br/>如果未指定此属性，则默认为none。<br/>例：<br/>QLineEdit {<br/>     border-width: 1px;<br/>     border-style: solid;<br/>     border-color: blue;<br/> } |
| border-top-style                                | Border Style                                        | 边框上边缘的样式。                                           |
| border-right-style                              | Border Style                                        | 边框右边缘的样式。                                           |
| border-bottom-style                             | Border Style                                        | 边框下边缘的样式。                                           |
| border-left-style                               | Border Style                                        | 边框左边缘的样式。                                           |
| **border-width**                                | Box Lengths                                         | 边框的宽度。 等效于设置border-top-width，border-right-width，border-bottom-width和border-left-width。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit和QToolTip支持此属性。<br/>例：<br/>QLineEdit {<br/>     border-width: 2px;<br/>     border-style: solid;<br/>     border-color: darkblue;<br/> } |
| border-top-width                                | Length                                              | 边框顶部边缘的宽度。                                         |
| border-right-width                              | Length                                              | 边框右侧边缘的宽度。                                         |
| border-bottom-width                             | Length                                              | 边框底部边缘的宽度。                                         |
| border-left-width                               | Length                                              | 边框左侧边缘的宽度。                                         |
| **button-layout**                               | Number                                              | QDialogButtonBox或QMessageBox中按钮的布局。 可能的值为0（WinLayout），1（MacLayout），2（KdeLayout）和3（GnomeLayout）。<br/>如果未指定此属性，则默认为SH_DialogButtonLayout样式提示的当前样式指定的值。<br/>例：<br/>* { button-layout: 2 } |
| **color**                                       | Brush                                               | 用于**呈现文本的颜色**。<br/>尊重QWidget :: palette的所有小部件都支持此属性。<br/>如果未设置此属性，则默认值为在QWidget :: foregroundRole的窗口小部件的调色板中设置的值（通常为黑色）。<br/>例：<br/>QPushButton { color: red } |
| dialogbuttonbox-buttons-have-icons              | Boolean                                             | QDialogButtonBox中的按钮是否显示图标<br/>如果将此属性设置为1，则QDialogButtonBox的按钮将显示图标； 如果设置为0，则不显示图标。<br/>有关如何设置图标的信息，请参见图标列表部分。 |
| **font**                                        | Font                                                | 设置文本字体的简写符号。 等效于指定字体系列，字体大小，字体样式和/或字体粗细。<br/>尊重QWidget :: font的所有小部件都支持此属性。<br/>如果未设置此属性，则默认值为QWidget :: font。<br/>例：<br/>QCheckBox { font: bold italic large "Times New Roman" } |
| font-family                                     | String                                              | QCheckBox { font-family: "New Century Schoolbook" }          |
| font-size                                       | Font Size                                           | QTextEdit { font-size: 12px }                                |
| font-style                                      | Font Style                                          | QTextEdit { font-style: italic }                             |
| font-weight                                     | Font Weight                                         | 字体的粗细。                                                 |
| **gridline-color***                             | Color                                               | QTableView中的网格线的颜色。<br/>如果未指定此属性，则默认为由当前样式为SH_Table_GridLineColor样式提示指定的值。<br/>例：<br/>* { gridline-color: gray } |
| **height**                                      | Length                                              | 子控件（或在某些情况下为小部件）的高度。<br/>如果未指定此属性，则默认为取决于子控件/小部件以及当前样式的值。<br/>警告：除非另行指定，否则在窗口小部件上设置此属性无效。 如果要使窗口小部件具有固定的高度，请将min-height和max-height设置为相同的值。<br/>例：<br/>QSpinBox::down-button { height: 10px } |
| **width**                                       | Length                                              | 子控件（在某些情况下为小部件）的宽度。<br/>如果未指定此属性，则默认为取决于子控件/小部件以及当前样式的值。<br/>警告：除非另行指定，否则在窗口小部件上设置此属性无效。 如果要使用固定宽度的小部件，请将最小宽度和最大宽度设置为相同的值。<br/>例：<br/>QSpinBox::up-button { width: 12px } |
| **icon-size**                                   | Length                                              | 小部件中**图标的宽度和高度**。<br/>可以使用此属性设置以下窗口小部件的图标大小。<br/>QCheckBox<br/>QListView<br/>QPushButton<br/>QRadioButton<br/>QTabBar<br/>QToolBar<br/>QToolBox<br/>QTreeView |
| **image***                                      | Url+                                                | 在子控件的内容矩形中绘制的图像。<br/>image属性接受Urls或svg的列表。 使用与QIcon相同的算法确定绘制的实际图像（即，图像从不放大，但在必要时始终按比例缩小）。 如果指定了svg，则图像将缩放为内容矩形的大小。<br/>在子控件上设置image属性会隐式设置子控件的宽度和高度（除非SVG中的图像）。<br/>**在Qt 4.3及更高版本中，可以使用image-position指定图像在矩形内的对齐方式**。<br/>此属性仅用于子控件-我们不支持其他元素。<br/>警告：需要QIcon SVG插件才能渲染SVG图像。<br/>例：<br/>/* 隐式地将向下按钮的大小设置为spindown.png的大小 */<br/> QSpinBox::down-button { image: url(:/images/spindown.png) } |
| image-position                                  | alignment                                           | 在Qt 4.3及更高版本中，可以使用相对位置或绝对位置指定图像位置的对齐方式。 |
| **left**                                        | Length                                              | 如果position是相对的（默认），则将子控件向右移动一定的偏移量。<br/>如果position为绝对位置，则left属性指定相对于父控件的左边缘的子控件的左边缘（另请参见subcontrol-origin）。<br/>如果未指定此属性，则默认为0。<br/>例：<br/> |
| **right**                                       | Length                                              | 如果position是相对的（默认），则将子控件向左移动一定的偏移量； 指定右边：x等效于指定左边：-x。<br/>如果position为绝对位置，则right属性指定相对于父控件的右边缘的子控件的右边缘（另请参见subcontrol-origin）。<br/>例：<br/>QSpinBox::down-button { right: 2px } |
| **top**                                         | Length                                              | 如果position是相对的（默认），则将子控件向下移动一定的偏移量。<br/>如果position为绝对位置，则top属性指定相对于父控件的上边缘的子控件的上边缘（另请参见subcontrol-origin）。<br/>如果未指定此属性，则默认为0。<br/>例：<br/>QSpinBox::up-button { top: 2px } |
| **bottom**                                      | Length                                              | **如果position是相对的（默认），则将子控件上移一定的偏移量；否则，将子控件上移。 然后，指定bottom：y等效于指定top：-y。<br/>如果position为绝对位置，则bottom属性指定子控件相对于父控件的底部边缘的底部边缘（另请参见subcontrol-origin）。<br/>例：<br/>QSpinBox::down-button { bottom: 2px }** |
| **lineedit-password-character***                | Number                                              | QLineEdit密码字符作为Unicode数字。<br/>如果未指定此属性，则默认为SH_LineEdit_PasswordCharacter样式提示的当前样式指定的值。<br/>例：<br/>* { lineedit-password-character: 9679 } |
| **margin**                                      | Box Lengths                                         | 小部件的边距。 等效于指定上边距，右边距右边，底部边距和左边距。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit和QToolTip支持此属性。<br/>如果未指定此属性，则默认为0。<br/>例：<br/>QLineEdit { margin: 2px } |
| margin-top                                      | Length                                              | 小部件的上边距。                                             |
| margin-right                                    | Length                                              | 小部件的右边距。                                             |
| margin-bottom                                   | Length                                              | 小部件的下边距。                                             |
| margin-left                                     | Length                                              | 小部件的左边距。                                             |
| **max-height**                                  | Length                                              | 小部件或子控件的最大高度。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSizeGrip，QSpinBox，QSplitter，QStatusBar，QTextEdit和QToolTip支持此属性。<br/>*该值相对于box model中的内容rect*。<br/>例：<br/>QSpinBox { max-height: 24px } |
| **max-width**                                   | Length                                              | 小部件或子控件的最大宽度。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSizeGrip，QSpinBox，QSplitter，QStatusBar，QTextEdit和QToolTip支持此属性。<br/>*该值相对于box model中的内容rect*。<br/>例：<br/>QSpinBox { max-width: 24px } |
| min-height                                      | Length                                              | 小部件或子控件的最小高度。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSizeGrip，QSpinBox，QSplitter，QStatusBar，QTextEdit和QToolTip支持此属性。<br/>如果未指定此属性，则最小高度是基于窗口小部件的内容和样式得出的。<br/>该值相对于盒子模型中的内容rect。<br/>例：<br/>QComboBox { min-height: 24px } |
| min-width                                       | Length                                              | 小部件或子控件的最小宽度。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSizeGrip，QSpinBox，QSplitter，QStatusBar，QTextEdit和QToolTip支持此属性。<br/>如果未指定此属性，则最小宽度是基于窗口小部件的内容和样式得出的。<br/>该值相对于盒子模型中的内容rect。<br/>例：<br/>QComboBox { min-width: 72px } |
| **messagebox-text-interaction-flags***          | Number                                              | 消息框中文本的交互行为。 可能的值基于Qt :: TextInteractionFlags（指定文本的选择、编辑、链接的显示方式）。<br/>如果未指定此属性，则默认为SH_MessageBox_TextInteractionFlags样式提示的当前样式指定的值。<br/>例：<br/>QMessageBox { messagebox-text-interaction-flags: 5 } |
| **opacity***                                    | Number                                              | 小部件的不透明度。 可能的值是0（透明）到255（不透明）。 目前，仅工具提示支持此功能。<br/>如果未指定此属性，则默认为SH_ToolTipLabel_Opacity样式提示的当前样式指定的值。<br/>例：<br/>QToolTip { opacity: 223 } |
| **padding**                                     | Box Lengths                                         | 小部件的填充。 等效于指定padding-top，padding-right，padding-bottom和padding-left。<br/>QAbstractItemView子类，QAbstractSpinBox子类，QCheckBox，QComboBox，QFrame，QGroupBox，QLabel，QLineEdit，QMenu，QMenuBar，QPushButton，QRadioButton，QSplitter，QTextEdit和QToolTip支持此属性。<br/>如果未指定此属性，则默认为0。<br/>例：<br/>QLineEdit { padding: 3px } |
| padding-top                                     | Length                                              | 小部件的顶部填充。                                           |
| padding-right                                   | Length                                              | 小部件的右侧填充。                                           |
| padding-bottom                                  | Length                                              | 小部件的底部填充。                                           |
| padding-left                                    | Length                                              | 小部件的左侧填充。                                           |
| **paint-alternating-row-colors-for-empty-area** | bool                                                | QTreeView是否为空白区域（即没有项目的区域）绘制交替的行颜色  |
| **position**                                    | relative \| absolute                                | 使用左，右，上和下指定的偏移是相对坐标还是绝对坐标。<br/>如果未指定此属性，则**默认为相对**。 |
| **selection-background-color***                 | Brush                                               | 所选文字或项目的**背景**。<br/>尊重QWidget :: palette并显示选择文本的所有小部件均支持此属性。<br/>如果未设置此属性，则默认值是为调色板的“突出显示”角色设置的值。<br/>例：<br/>QTextEdit { selection-background-color: darkblue } |
| **selection-color***                            | Brush                                               | 所选文本或项目的**前景**。<br/>尊重QWidget :: palette并显示选择文本的所有小部件均支持此属性。<br/>如果未设置此属性，则默认值是为调色板的HighlightedText角色设置的任何值。<br/>例：<br/>QTextEdit { selection-color: white } |
| **show-decoration-selected***                   | Boolean                                             | 控制QListView中的选择是覆盖整个行还是仅覆盖文本范围。<br/>如果未指定此属性，则默认为SH_ItemView_ShowDecorationSelected样式提示的当前样式指定的值。<br/>例：<br/>* { show-decoration-selected: 1 } |
| **spacing***                                    | Length                                              | 小部件中的内部间距。<br/>QCheckBox，可检查的QGroupBoxes，QMenuBar和QRadioButton支持此属性。<br/>如果未指定此属性，则默认值取决于窗口小部件和当前样式。<br/>例：<br/>QMenuBar { spacing: 10 } |
| **subcontrol-origin***                          | Origin                                              | 父控件内子控件的原点矩形。<br/>如果未指定此属性，则默认值为padding。<br/>例：<br/>QSpinBox::up-button {<br/>     image: url(:/images/spinup.png);<br/>     subcontrol-origin: content;<br/>     subcontrol-position: right top;<br/> } |
| **subcontrol-position***                        | Alignment                                           | 子控件在由subcontrol-origin指定的原点矩形内的对齐方式。<br/>如果未指定此属性，则默认为依赖于子控件的值。<br/>例：<br/>QSpinBox::down-button {<br/>     image: url(:/images/spindown.png);<br/>     subcontrol-origin: padding;<br/>     subcontrol-position: right bottom;<br/> } |
| **text-align**                                  | Alignment                                           | 小部件内容中**文本和图标的对齐方式**。<br/>如果未指定此值，则默认为取决于本机样式的值。<br/>例：<br/>QPushButton {<br/>     text-align: left;<br/> } |
| **text-decoration**                             | none <br/>underline <br/>overline <br/>line-through | 附加文字效果                                                 |

## 3.List of Icons图标属性——未完

可以使用以下属性来自定义Qt中使用的图标。 本节中列出的每个属性的类型均为“图标”。

请注意，要使图标显示在QDialogButtonBox的按钮中，您需要将dialogbuttonbox-buttons-have-icons属性设置为true。 另外，要自定义图标的大小，请使用icon-size属性。

| Name | QStyle::StandardPixmap |
| ---- | ---------------------- |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |
|      |                        |



## 4.List of Property Types属性的参数类型列表

下表总结了不同属性类型的语法和含义。

| Type         | Syntax                                                       | Description                                                  |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Alignment    | { top \| bottom \| left \| right \| center}*                 | 水平和/或垂直对齐。<br/>QTextEdit { background-position: bottom center } |
| Attachment   | { scroll \| fixed }*                                         | 滚动或固定附件。                                             |
| Background   | { Brush \| Url \| Repeat \| Alignment }*                     | 一系列的笔刷，URL，重复和对齐。                              |
| Boolean      | 0 \| 1                                                       | True (1) or false (0).                                       |
| Border       | { Border Style \| Length \| Brush }*                         | 速记边框属性。                                               |
| Border Image | none \| Url Number{4}(stretch \| repeat){0,2}                | 边界图像是由九个部分组成的图像（左上，顶部居中，右上，左中，居中，右中，左下，居中和右下）。 当需要一定大小的边框时，将按原样使用角部分，并拉伸或重复顶部，右侧，底部和左侧部分以生成具有所需大小的边框。<br/>有关详细信息，请参见CSS3规范草案。 |
| Border Style | dashed \|
dot-dash \| dot-dot-dash \| dotted \| double \| groove \| inset \| outset \| ridge \| solid \| none | 指定用于绘制边框的图案。 有关详细信息，请参见CSS3规范草案。  |
| Box Colors   | Brush{1,4}                                                   | 一到四个出现的Brush，分别指定一个框的顶部，右侧，底部和左侧。 如果未指定左侧颜色，则将其与右侧颜色相同。 如果未指定底色，则将其与顶色相同。 如果未指定正确的颜色，则该颜色应与顶部的颜色相同。<br/>例：<br/>QLabel { border-color: red }   /* red red red red */<br/> QLabel { border-color: red blue } /* red blue red blue */<br/> QLabel { border-color: red blue green } /* red blue green blue */<br/> QLabel { border-color: red blue green yellow }  /* red blue green yellow */ |
| Box Lengths  | Length{1,4}                                                  | 一到四次出现的长度，分别指定一个框的顶部，右侧，底部和左侧。 如果未指定左侧长度，则将其与右侧长度相同。 如果未指定底部长度，则该长度应与顶部长度相同。 如果未指定正确的长度，则该长度应与顶部长度相同。<br/>例子：<br/>QLabel { border-width: 1px }                    /* 1px 1px 1px 1px */<br/> QLabel { border-width: 1px 2px }                /* 1px 2px 1px 2px */<br/> QLabel { border-width: 1px 2px 3px }            /* 1px 2px 3px 2px */<br/> QLabel { border-width: 1px 2px 3px 4px }        /* 1px 2px 3px 4px */ |
| Brush        | Color \| Gradient \| PaletteRole                             | 指定调色板中的颜色或渐变或条目。                             |
| Color        | rgb(r, g, b) \| rgba(r, g, b, a) \| hsv(h, s, v) \| hsva(h, s, v, a) \| \#rrggbb \| Color Name | 将颜色指定为RGB（红色，绿色，蓝色）或RGBA（红色，绿色，蓝色，alpha）或HSV（色调，饱和度，值）或HSVA（色调，饱和度，值，alpha）或命名颜色。 rgb（）或rgba（）语法可以与0到255之间的整数值或百分比一起使用。 hsv（）或hsva（）中s，v和a的值都必须在0-255范围内； h的值必须在0-359的范围内。<br/>例子：<br/>QLabel { border-color: red }                    /* opaque red */<br/> QLabel { border-color: #FF0000 }                /* opaque red */<br/> QLabel { border-color: rgba(255, 0, 0, 75%) }   /* 75% opaque red */<br/> QLabel { border-color: rgb(255, 0, 0) }         /* opaque red */<br/> QLabel { border-color: rgb(100%, 0%, 0%) }      /* opaque red */<br/> QLabel { border-color: hsv(60, 255, 255) }      /* opaque yellow */<br/> QLabel { border-color: hsva(240, 255, 255, 75%) }<br/>注意：允许的RGB颜色与CSS 2.1允许的颜色相同，如下所示。 |
| Font         | (Font Style \| Font Weight){0,2} Font Size String            | 字体属性                                                     |
| Font Size    | Length                                                       | 字体大小                                                     |
| Font Style   | normal \| italic \| oblique                                  | 字体风格                                                     |
| Font Weight  | normal \| bold \| 100 \| ... \| 900                          | 字体粗细                                                     |
| **Gradient** | qlineargradient  \| qradialgradient \| qconicalgradient      | 指定渐变填充。 共有三种类型的渐变填充：<br/>**线性渐变**会在起点和终点之间插入颜色。<br/>**径向渐变**会在焦点和围绕它的圆上的端点之间插入颜色。<br/>**圆锥形渐变**会在中心点周围插入颜色。<br/>渐变是在“对象边界模式”中指定的。 想象一下渲染渐变的盒子，其左上角为（0，0），右下角为（1，1）。 然后将渐变参数指定为从0到1的百分比。这些值在运行时外推到实际的框坐标。 可以指定位于边界框之外的值（例如，-0.6或1.8）。<br/>警告：停靠点必须按升序显示。<br/>/* linear gradient from white to green */<br/> QTextEdit {<br/>     background: qlineargradient(x1:0, y1:0, x2:1, y2:1,<br/>                 stop:0 white, stop: 0.4 gray, stop:1 green)<br/> }<br/><br/> /* linear gradient from white to green */<br/> QTextEdit {<br/>     background: qlineargradient(x1:0, y1:0, x2:1, y2:1,<br/>                 stop:0 white, stop: 0.4 rgba(10, 20, 30, 40), stop:1 rgb(0, 200, 230, 200))<br/> }<br/><br/> /* conical gradient from white to green */<br/> QTextEdit {<br/>     background: qconicalgradient(cx:0.5, cy:0.5, angle:30,<br/>                 stop:0 white, stop:1 #00FF00)<br/> }<br/><br/> /* radial gradient from white to green */<br/> QTextEdit {<br/>     background: qradialgradient(cx:0, cy:0, radius: 1,<br/>                 fx:0.5, fy:0.5, stop:0 white, stop:1 green)<br/> } |
| Icon         | (Url (disabled \| active \| normal \| selected)?(on \| off)?)* | 网址，QIcon :: Mode和QIcon :: State的列表。<br/>* {<br/>     file-icon: url(file.png),<br/>                url(file_selected.png) selected;<br/>   }<br/><br/> QMessageBox {<br/>     dialogbuttonbox-buttons-have-icons: true;<br/>     dialog-ok-icon: url(ok.svg);<br/>     dialog-cancel-icon: url(cancel.png), url(grayed_cancel.png) disabled;<br/> } |
| Length       | Number (px \| pt \| em \| ex)?                               | 一个数字，后跟一个度量单位。 CSS标准建议用户代理必须忽略具有非法值的声明。 在Qt中，必须指定度量单位。 为了与早期版本的Qt兼容，在大多数情况下，不带度量单位的数字被视为像素。 支持的单位是：<br/>px：像素<br/>pt：1点的大小（即1/72英寸）<br/>em：字体的em宽度（即'M'的宽度）<br/>ex：字体的ex宽度（即'x'的高度） |
| Number       | 十进制整数或实数                                             | Examples: 0, 18, +127, -255, 12.34, -.5, 0009.               |
| **Origin**   | margin \| border \| padding \| content                       | 指示要使用四个矩形中的哪个。<br/>margin：边距矩形。 边距落在边界之外。<br/>border：边框矩形。 这是绘制任何边框的地方。<br/>padding：填充矩形。 与边距不同，填充位于边框内。<br/>content：内容矩形。 这指定实际内容的位置，不包括任何填充，边框或边距。 |
| PaletteRole  | alternate-base \| base \| bright-text \| button \| button-text \| dark \| highlighted-text \| light \| link \| link-visited \| mid \| midlight \| shadow \| text \| window \| window-text | 这些值对应于小部件的QPalette中的“颜色”角色。<br/>例如，<br/>QPushButton { color: palette(dark); } |
| **Radius**   | Length{1, 2}                                                 | 一或两次出现“长度”。 如果仅指定一个长度，则将其用作定义角的四分之一圆的半径。 如果指定了两个长度，则第一长度是四分之一椭圆的水平半径，而第二长度是垂直半径。 |
| Repeat       | repeat-x \| repeat-y \| repeat \| no-repeat                  | 指示重复性质的值。<br/>repeat-x：水平重复。<br/>重复y：垂直重复。<br/>重复：水平和垂直重复。<br/>不重复：不重复。 |
| Url          | url(filename)                                                | filename是本地磁盘上或使用Qt资源系统存储的文件名。 设置图像会隐式设置元素的宽度和高度 |

## 5.List of Pseudo-States伪状态

| Pseudo-State       | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| :floatable         | 这些部件可以浮动。 例如，QDockWidget启用了QDockWidget :: DockWidgetFloatable功能。 |
| **:focus**         | 该部件具有输入焦点。                                         |
| **:checked**       | 该部件被选中，例如QCheckBox, QPushButton, QRadioButton, QToolButton |
| **:unchecked**     | 该部件未被选中，例如QCheckBox, QPushButton, QRadioButton, QToolButton |
| :indeterminate     | 该部件的状态不确定。 例如，部分检查了QCheckBox或QRadioButton。 |
| **:selected**      | 该部件被选择。 例如，QTabBar中的选定选项卡，QMenu中的选定项目，QListWidget选定项目，QTreeWidget选定项目 |
| **:hover**         | 鼠标悬停在该部件上。                                         |
| **:pressed**       | 鼠标点击在该部件上。可被选中(selected)的控件不必使用该状态。 |
| :active            | 当窗口小部件位于活动窗口中时，将设置此状态。                 |
| :adjoins-item      | 当QTreeView的::: branch与某个项目相邻时，将设置此状态。      |
| :alternate         | 当QAbstractItemView :: alternatingRowColors（）设置为true时，将为绘制QAbstractItemView的行的每个备用行设置此状态。 |
| :movable           | 该项目可以移动。 例如，QDockWidget启用了QDockWidget :: DockWidgetMovable功能。 |
| :closable          | 该部件可以被关闭                                             |
| :closed            | 该部件处于关闭状态。 例如，QTreeView中的非展开项             |
| :default           | 该部件是默认设置。 例如，默认的QPushButton或QMenu中的默认操作。 |
| **:disabled**      | 该部件被禁用                                                 |
| :editable          | QComboBox是可编辑的。                                        |
| :edit-focus        | 该部件具有编辑焦点（请参见QStyle :: State_HasEditFocus）。 此状态仅适用于Qt Extended应用程序。 |
| :enabled           | 该部件可被使用                                               |
| :exclusive         | 该部件属于独占部件组。 例如，专用QActionGroup中的菜单项。    |
| :first             | 该部件是第一个（在列表中）。 例如，QTabBar中的第一个选项卡。 |
| :flat              | 该部件是扁平的。 例如，一个扁平的QPushButton。               |
| :last              | 该部件是最后一个（在列表中）。 例如，QTabBar中的最后一个选项卡。 |
| :left              | 该部件位于左侧。 例如，一个QTabBar的选项卡位于左侧。         |
| :middle            | 该部件在中间（在列表中）。 例如，标签不在QTabBar的开头或结尾。 |
| :right             | 该部件位于右侧。 例如，QTabBar的选项卡位于右侧               |
| :top               | 该部件位于顶部。 例如，QTabBar的选项卡位于顶部。             |
| :bottom            | 该部件位于底部。 例如，QTabBar的选项卡位于底部。             |
| :has-children      | 该部件有孩子。 例如，QTreeView中具有子项的项。               |
| :has-siblings      | 该部件有兄弟。 例如，QTreeView中具有子项的项。               |
| :horizontal        | 该部件具有水平方向                                           |
| :maximized         | 该部件已最大化。 例如，最大化的QMdiSubWindow。               |
| :minimized         | 该项目被最小化。 例如，最小化的QMdiSubWindow。               |
| :no-frame          | The item has no frame. For example, a frameless QSpinBox or QLineEdit. |
| :non-exclusive     | 该部件属于非独占部件组。 例如，非专有QActionGroup中的菜单项。 |
| :off               | 对于可以切换的部件，这适用于处于“关闭”状态的项目。           |
| :only-one          | 对于可以切换的部件，这适用于处于“关闭”状态的项目。该项目是唯一的（在列表中）。 例如，QTabBar中的一个单独的选项卡。 |
| :open              | 该部件处于打开状态。 例如，QTreeView中的展开项目，带有打开菜单的QComboBox或QPushButton。 |
| :next-selected     | 选择下一个部件（列表中）。 例如，QTabBar的选定选项卡在此项目旁边。 |
| :on                | 对于可以切换的部件，这适用于处于“ on”状态的窗口小部件。      |
| :previous-selected | 选择上一个部件（列表中）。 例如，QTabBar中的一个选项卡位于所选选项卡的旁边。 |
| :read-only         | 该部件被标记为只读或不可编辑。 例如，只读的QLineEdit或不可编辑的QComboBox。 |
| :vertical          | 该部件具有垂直方向。                                         |
| :window            | 该小部件是一个窗口（即顶层小部件）                           |

## 6.List of Sub-Controls子控件列表

![qss样式表学习](http://file.elecfans.com/web1/M00/46/76/o4YBAFqeNriAVTMnAABrZDJ8GeI953.png)

| Sub-Control      | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| **::add-line**   | 给QScrollBar添加（向下滚动）一行的按钮。                     |
| **::add-page**   | 手柄（滑块）和QScrollBar的添加线之间的区域。                 |
| **::sub-line**   | 给QScrollBar减少（向上滚动）一行的按钮。                     |
| **::sub-page**   | 手柄（滑块）和QScrollBar的减少线之间的区域。                 |
| ::up-arrow       | QHeaderView（排序指示器），QScrollBar或QSpinBox的向上箭头。  |
| ::up-button      | QSpinBox的向上按钮。                                         |
| **::down-arrow** | QHeaderView（排序指示器），QScrollBar或QSpinBox或QComboBox的向下箭头。 |
| ::down-button    | QSpinBox的向下按钮。                                         |
| ::left-arrow     | QScrollBar的左箭头。                                         |
| ::left-corner    | QTabWidget的左上角。 例如，此控件可用于控制QTabWidget中左角控件的位置。 |
| ::right-arrow    | QScrollBar的右箭头。                                         |
| ::right-corner   | QTabWidget的右上角。 例如，此控件可用于控制QTabWidget中右角控件的位置。 |
| ::menu-arrow     | QToolButton带有菜单的箭头。                                  |
| ::menu-button    | QToolButton的菜单按钮。                                      |
| ::menu-indicator | QPushButton的菜单指示器。                                    |
| ::scroller       | QMenu或QTabBar的滚动器。                                     |
| ::branch         | QTreeView的分支指示器。                                      |
| **::chunk**      | QProgressBar的进度块。                                       |
| ::close-button   | QDockWidget或QTabBar的选项卡的关闭按钮                       |
| ::corner         | QAbstractScrollArea中两个滚动条之间的角                      |
| **::drop-down**  | QComboBox的下拉按钮。                                        |
| ::float-button   | QDockWidget的浮动按钮                                        |
| **::groove**     | QSlider的凹槽。                                              |
| ::**indicator**  | QAbstractItemView，QCheckBox，QRadioButton，可检查的QMenu项或可检查的QGroupBox的指示器。 |
| ::**handle**     | QScrollBar，QSplitter或QSlider的句柄（滑块）。               |
| ::icon           | QAbstractItemView或QMenu的图标。                             |
| ::item           | QAbstractItemView，QMenuBar，QMenu或QStatusBar的一项。       |
| ::pane           | QTabWidget的窗格（框架）。                                   |
| ::section        | QHeaderView的部分。                                          |
| ::separator      | QMenu或QMainWindow中的分隔符。                               |
| ::tab            | QTabBar或QToolBox的选项卡。                                  |
| ::tab-bar        | QTabWidget的标签栏。 该子控件仅用于控制QTabBar在QTabWidget中的位置。 使用:: tab子控件设置选项卡的样式。 |
| ::tear           | QTabBar的撕裂指示器。                                        |
| ::tearoff        | QMenu的拆卸指示器。                                          |
| ::text           | QAbstractItemView的文本                                      |
| ::title          | QGroupBox或QDockWidget的标题。                               |

## 7.常用样式

### 7.1.滚动条QScrollBar

```css
ui->QTableView->verticalScrollBar()->setStyleSheet("QScrollBar:vertical{"        //垂直滑块整体  
                                                          "background:#FFFFFF;"  //背景色  
                                                          "padding-top:20px;"    //上预留位置（放置向上箭头）  
                                                          "padding-bottom:20px;" //下预留位置（放置向下箭头）  
                                                          "padding-left:3px;"    //左预留位置（美观）  
                                                          "padding-right:3px;"   //右预留位置（美观）  
                                                          "border-left:1px solid #d7d7d7;}"//左分割线  
                                                          "QScrollBar::handle:vertical{"//滑块样式  
                                                          "background:#dbdbdb;"  //滑块颜色  
                                                          "border-radius:6px;"   //边角圆润  
                                                          "min-height:80px;}"    //滑块最小高度  
                                                          "QScrollBar::handle:vertical:hover{"//鼠标触及滑块样式  
                                                          "background:#d0d0d0;}" //滑块颜色  
                                                          "QScrollBar::add-line:vertical{"//向下箭头样式  
                                                          "background:url(:/images/resource/images/checkout/down.png) center no-repeat;}"  
                                                          "QScrollBar::sub-line:vertical{"//向上箭头样式  
                                                          "background:url(:/images/resource/images/checkout/up.png) center no-repeat;}");  
  
ui->QTableView->horizontalScrollBar()->setStyleSheet("QScrollBar:horizontal{"  
                                                          "background:#FFFFFF;"  
                                                          "padding-top:3px;"  
                                                          "padding-bottom:3px;"  
                                                          "padding-left:20px;"  
                                                          "padding-right:20px;}"  
                                                          "QScrollBar::handle:horizontal{"  
                                                          "background:#dbdbdb;"  
                                                          "border-radius:6px;"  
                                                          "min-width:80px;}"  
                                                          "QScrollBar::handle:horizontal:hover{"  
                                                          "background:#d0d0d0;}"  
                                                          "QScrollBar::add-line:horizontal{"  
                                                          "background:url(:/images/resource/images/checkout/right.png) center no-repeat;}"  
                                                          "QScrollBar::sub-line:horizontal{"  
                                                          "background:url(:/images/resource/images/checkout/left.png) center no-repeat;}");
```

### 7.2.QTreeWIdget

```css
"QTreeWidget"
"{"
"border: none;"
"outline: 0px;"			// 去除选中项时的虚线矩形边框
"}"
"QTreeWidget::item"      // 单个的列表项
"{"
"height: 26px;"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"color: #333333;"
"}"
"QTreeWidget::item:selected"
"{"
"background-color: #E4E4E4;"
"color: #333333;"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"Line-height: 20px;"
"}"
"QTreeWidget::branch:has-children:!has-siblings:closed,"    // 修改字体树的折叠展开图标
"QTreeWidget::branch:closed:has-children:has-siblings"
"{"
"border-image: none;"
"image: url(:/res/16px_fold_+.svg);"
"}"
"QTreeWidget::branch:open:has-children:!has-siblings,"
"QTreeWidget::branch:open:has-children:has-siblings"
"{"
"border-image: none;"
"image: url(:/res/16px_fold_-.svg);"
"}"
```

### 7.3.QListWidget

```css
"QListWidget#listWidget"            // 列表项整体
"{"
"border: none;"
"outline: 0px;"                     // 去除item被选中时的虚线矩形边框
"font-size: 14px;"
"background: #EFEFEF;"
"color: #333333;"
"font-family: Microsoft YaHei;"
"text-align: left;"
"}"
"QListWidget#listWidget::item"      // 单个的列表项
"{"
"width: 114px;"
"height: 40px;"
"}"
"QListWidget#listWidget::item:hover"    // 悬浮在列表项上
"{"
"background: #E4E4E4;"
"}"
"QListWidget#listWidget::item:selected" // 被选中的列表项
"{"
"color: #333333;"
"border-left:2px solid #1299DA;"
"background: white;"
"}"
```

### 7.4.QHeadView表头

```c++
"QHeaderView::section"                      // 设置Table或Tree的表头样式
"{"
"border: 1px solid white;"
"height: 26px;"
"background: #EFEFEF;"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"color: #333333;"
"}"
```

### 7.5.QTableView

表格内容留左边距：

```c++
const int PM_FocusFrameHMargin = 8;

/**
 * @brief The TableItemSpaceStyle class 设置MetaDataTableV的Item左间距为8px
 */
class TableItemSpaceStyle: public QProxyStyle
{
    int pixelMetric(QStyle::PixelMetric metric, const QStyleOption *option, const QWidget *widget) const
    {
        switch (metric)
        {
            case PM_FocusFrameHMargin:
                return 8;
            default:
                break;
        }
        return QProxyStyle::pixelMetric(metric, option, widget);
    }
};

ui->MetaDataTableV->setStyle(new TableItemSpaceStyle);
```

表头留左边距：

```css
ui->MetaDataTableV->setStyleSheet("QHeaderView::section"     // 设置表头样式
"{"
"border: 1px solid white;"
"height: 26px;"
"background: #EFEFEF;"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"color: #333333;"
"}"
"QHeaderView::section:first"
"{"
"padding-left: 8px;"          // 设置表头文字左间距
"}"
"QHeaderView::section:last"
"{"
"padding-left: 8px;"
"}"
"QScrollBar::vertical"        // 设置滚动条上面滚动不到的距离，即上边距
"{"
"padding-top: 26px;"          // 顶部的表头不随滚动条滚动
"background: white;"
"}"
);
```

### 7.6.QRadioButton

```css
"QRadioButton"                      // QRadioButton统一样式
"{"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"color: #666666;"
"}"
"QRadioButton:disabled"
"{"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"color: #CCCCCC;"
"}"
"QRadioButton::indicator"// 前面按钮的样式
"{"
"height: 12px;"
"width: 12px;"
"border-radius: 6.5px;"
"border: 1px solid #DADADA;"
"}"
"QRadioButton::indicator:hover"
"{"
"background: #F5F5F5;"
"}"
"QRadioButton::indicator:checked"
"{"
"image: url(:/radiobtn.svg);"
"}"
```

### 7.7.QCheckBox

```css
"QCheckBox"                         // QCheckBox统一样式
"{"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"color: #666666;"
"}"
"QCheckBox::indicator"
"{"
"width: 12px;"
"height: 12px;"
"border: 1px solid #DADADA;"
"}"
"QCheckBox::indicator:hover"
"{background: #F5F5F5;"
"border: 1px solid #DADADA;"
"}"
"QCheckBox::indicator:checked"
"{"
"image: url(:/checkbox.svg);"
"}"
```

### 7.8.QComboBox

```css
"QComboBox"                         // QComboBox统一样式
"{"
"font-family: Microsoft YaHei;"
"font-size: 12px;"
"color: #666666;"
"background: #FFFFFF;"
"border: 1px solid #DADADA;"
"border-radius: 2px;"
"}"
"QComboBox::drop-down"      // 下拉按钮
"{"
"width: 23px;"
"height: 23px;"
"background-color: white;"//设置与左侧LineEdit同样的背景色，去掉了按钮的突出显示
"}"
"QComboBox::down-arrow"     // 向下箭头
"{"
"background: url(:/down_arrow.svg);"
"background-position: center;"
"background-repeat: no-repeat;"
"}"
```



## 8.加载翻译文件

```c++
bool flag = true;
// 读取界面的配置参数，加载翻译文件
QTranslator qtTranslator;
QString dir = QCoreApplication::applicationDirPath();
if (qtTranslator.load("docproperty_ch", dir + "/translations", ".", ".qm"))
{
    qApp->installTranslator(&qtTranslator);
    ui->retranslateUi(this);	// 使得ui上的文字可被识别和翻译
}
else
{
    flag = false;
}
```

