# Namespace

## 1.Types

- flags	Alignment

- enum	AlignmentFlag { AlignLeft, AlignRight, AlignHCenter, AlignJustify, ..., AlignVertical_Mask }

- enum	AnchorAttribute { AnchorName, AnchorHref }

- enum	AnchorPoint { AnchorLeft, AnchorHorizontalCenter, AnchorRight, AnchorTop, AnchorVerticalCenter, AnchorBottom }

- enum	ApplicationAttribute { AA_ImmediateWidgetCreation, AA_MSWindowsUseDirect3DByDefault, AA_DontShowIconsInMenus, AA_NativeWindows, ..., AA_CaptureMultimediaKeys }

- enum	ArrowType { NoArrow, UpArrow, DownArrow, LeftArrow, RightArrow }

- enum	AspectRatioMode { IgnoreAspectRatio, KeepAspectRatio, KeepAspectRatioByExpanding }

- enum	Axis { XAxis, YAxis, ZAxis }

- enum	BGMode { TransparentMode, OpaqueMode }

- enum	BrushStyle { NoBrush, SolidPattern, Dense1Pattern, Dense2Pattern, ..., TexturePattern }

- enum	CaseSensitivity { CaseInsensitive, CaseSensitive }

- enum	CheckState { Unchecked, PartiallyChecked, Checked }

- enum	ClipOperation { NoClip, ReplaceClip, IntersectClip, UniteClip }

- enum	ConnectionType { AutoConnection, DirectConnection, QueuedConnection, BlockingQueuedConnection, UniqueConnection, AutoCompatConnection }

- enum	ContextMenuPolicy { NoContextMenu, PreventContextMenu, DefaultContextMenu, ActionsContextMenu, CustomContextMenu }

- enum	CoordinateSystem { DeviceCoordinates, LogicalCoordinates }

- enum	Corner { TopLeftCorner, TopRightCorner, BottomLeftCorner, BottomRightCorner }

- enum	CursorMoveStyle { LogicalMoveStyle, VisualMoveStyle }

- `enum	CursorShape { ArrowCursor, UpArrowCursor, CrossCursor, WaitCursor, ..., BitmapCursor }`

  这个枚举类型定义了可以使用的各种游标。

  标准的箭头光标是处于正常状态的小部件的默认值。

  | Constant               | Value | Description                                                  |
  | ---------------------- | ----- | ------------------------------------------------------------ |
  | Qt::ArrowCursor        | 0     | 标准的箭头光标。                                             |
  | Qt::UpArrowCursor      | 1     | 向上指向屏幕顶部的箭头。                                     |
  | Qt::CrossCursor        | 2     | 一种十字线光标，通常用来帮助用户准确地选择屏幕上的一个点。   |
  | Qt::WaitCursor         | 3     | 沙漏或监视游标，通常在操作期间显示，阻止用户与应用程序交互。 |
  | Qt::IBeamCursor        | 4     | 插入符号或ibeam光标，表示小部件可以接受和显示文本输入。      |
  | Qt::SizeVerCursor      | 5     | 用于垂直调整顶级窗口大小的元素的光标。                       |
  | Qt::SizeHorCursor      | 6     | 用于水平调整顶级窗口大小的元素的光标。                       |
  | Qt::SizeBDiagCursor    | 7     | 用于元素的游标，这些元素用于在其右上角和左下角对角调整顶级窗口的大小。 |
  | Qt::SizeFDiagCursor    | 8     | 用于元素的光标，这些元素用于在左上角和右下角对角调整顶级窗口的大小。 |
  | Qt::SizeAllCursor      | 9     | 用于在任何方向上调整顶级窗口大小的元素的光标。               |
  | Qt::BlankCursor        | 10    | 一种空白/不可见的光标，通常在光标形状需要隐藏时使用。        |
  | Qt::SplitVCursor       | 11    | 用于垂直分割器的光标，表示可以垂直拖动手柄来调整可用空间的使用。 |
  | Qt::SplitHCursor       | 12    | 用于水平分割器的光标，表示可以垂直拖动手柄来调整可用空间的使用。 |
  | Qt::PointingHandCursor | 13    | 通常用于超链接等可单击元素的指针。                           |
  | Qt::ForbiddenCursor    | 14    | 一种割开的圆形光标，通常在拖放操作期间使用，以表示不能在特定小部件或特定区域内拖放所拖放的内容。 |
  | Qt::ArrowCursor        | 15    |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |
  | Qt::ArrowCursor        |       |                                                              |

  

- enum	DateFormat { TextDate, ISODate, SystemLocaleShortDate, SystemLocaleLongDate, ..., LocalDate }

- enum	DayOfWeek { Monday, Tuesday, Wednesday, Thursday, ..., Sunday }

- enum	DockWidgetArea { LeftDockWidgetArea, RightDockWidgetArea, TopDockWidgetArea, BottomDockWidgetArea, AllDockWidgetAreas, NoDockWidgetArea }

- flags	DockWidgetAreas

- enum	DropAction { CopyAction, MoveAction, LinkAction, ActionMask, IgnoreAction, TargetMoveAction }

- flags	DropActions

- enum	EventPriority { HighEventPriority, NormalEventPriority, LowEventPriority }

- enum	FillRule { OddEvenFill, WindingFill }

- enum	FocusPolicy { TabFocus, ClickFocus, StrongFocus, WheelFocus, NoFocus }

- enum	FocusReason { MouseFocusReason, TabFocusReason, BacktabFocusReason, ActiveWindowFocusReason, ..., OtherFocusReason }

- enum	GestureFlag { DontStartGestureOnChildren, ReceivePartialGestures, IgnoredGesturesPropagateToParent }

- flags	GestureFlags

- enum	GestureState { GestureStarted, GestureUpdated, GestureFinished, GestureCanceled }

- enum	GestureType { TapGesture, TapAndHoldGesture, PanGesture, PinchGesture, SwipeGesture, CustomGesture }

- enum	GlobalColor { white, black, red, darkRed, ..., color1 }

- typedef	HANDLE

- enum	HitTestAccuracy { ExactHit, FuzzyHit }

- enum	ImageConversionFlag { AutoColor, ColorOnly, MonoOnly, DiffuseDither, ..., NoOpaqueDetection }

- flags	ImageConversionFlags

- enum	InputMethodHint { ImhNone, ImhHiddenText, ImhNoAutoUppercase, ImhPreferNumbers, ..., ImhExclusiveInputMask }

- flags	InputMethodHints

- enum	InputMethodQuery { ImMicroFocus, ImFont, ImCursorPosition, ImSurroundingText, ..., ImAnchorPosition }

- enum	ItemDataRole { DisplayRole, DecorationRole, EditRole, ToolTipRole, ..., UserRole }

- enum	ItemFlag { NoItemFlags, ItemIsSelectable, ItemIsEditable, ItemIsDragEnabled, ..., ItemIsTristate }

- flags	ItemFlags

- enum	ItemSelectionMode { ContainsItemShape, IntersectsItemShape, ContainsItemBoundingRect, IntersectsItemBoundingRect }

- enum	Key { Key_Escape, Key_Tab, Key_Backtab, Key_Backspace, ..., Key_Cancel }

- enum	KeyboardModifier { NoModifier, ShiftModifier, ControlModifier, AltModifier, ..., GroupSwitchModifier }

- flags	KeyboardModifiers

- enum	LayoutDirection { LeftToRight, RightToLeft, LayoutDirectionAuto }

- enum	MaskMode { MaskInColor, MaskOutColor }

- enum	MatchFlag { MatchExactly, MatchFixedString, MatchContains, MatchStartsWith, ..., MatchRecursive }

- flags	MatchFlags

- enum	Modifier { SHIFT, META, CTRL, ALT, UNICODE_ACCEL }

- enum	MouseButton { NoButton, LeftButton, RightButton, MidButton, ..., XButton2 }

- flags	MouseButtons

- enum	NavigationMode { NavigationModeNone, NavigationModeKeypadTabOrder, NavigationModeKeypadDirectional, NavigationModeCursorAuto, NavigationModeCursorForceVisible }

- enum	Orientation { Horizontal, Vertical }

- flags	Orientations

- enum	PenCapStyle { FlatCap, SquareCap, RoundCap }

- enum	PenJoinStyle { MiterJoin, BevelJoin, RoundJoin, SvgMiterJoin }

- enum	PenStyle { NoPen, SolidLine, DashLine, DotLine, ..., CustomDashLine }

- enum	ScrollBarPolicy { ScrollBarAsNeeded, ScrollBarAlwaysOff, ScrollBarAlwaysOn }

- enum	ShortcutContext { WidgetShortcut, WidgetWithChildrenShortcut, WindowShortcut, ApplicationShortcut }

- enum	SizeHint { MinimumSize, PreferredSize, MaximumSize, MinimumDescent }

- enum	SizeMode { AbsoluteSize, RelativeSize }

- enum	SortOrder { AscendingOrder, DescendingOrder }

- enum	TextElideMode { ElideLeft, ElideRight, ElideMiddle, ElideNone }

- enum	TextFlag { TextSingleLine, TextDontClip, TextExpandTabs, TextShowMnemonic, ..., TextJustificationForced }

- enum	TextFormat { PlainText, RichText, AutoText, LogText }

- enum	TextInteractionFlag { NoTextInteraction, TextSelectableByMouse, TextSelectableByKeyboard, LinksAccessibleByMouse, ..., TextBrowserInteraction }

- flags	TextInteractionFlags

- enum	TileRule { StretchTile, RepeatTile, RoundTile }

- enum	TimeSpec { LocalTime, UTC, OffsetFromUTC }

- enum	ToolBarArea { LeftToolBarArea, RightToolBarArea, TopToolBarArea, BottomToolBarArea, AllToolBarAreas, NoToolBarArea }

- flags	ToolBarAreas

- enum	ToolButtonStyle { ToolButtonIconOnly, ToolButtonTextOnly, ToolButtonTextBesideIcon, ToolButtonTextUnderIcon, ToolButtonFollowStyle }

- enum	TouchPointState { TouchPointPressed, TouchPointMoved, TouchPointStationary, TouchPointReleased }

- flags	TouchPointStates

- enum	TransformationMode { FastTransformation, SmoothTransformation }

- enum	UIEffect { UI_AnimateMenu, UI_FadeMenu, UI_AnimateCombo, UI_AnimateTooltip, UI_FadeTooltip, UI_AnimateToolBox }

- typedef	WFlags

- enum	WhiteSpaceMode { WhiteSpaceNormal, WhiteSpacePre, WhiteSpaceNoWrap }

- **`enum	WidgetAttribute { WA_AcceptDrops, WA_AlwaysShowToolTips, WA_ContentsPropagated, WA_CustomWhatsThis, ..., WA_MacNoShadow }`**

  | Constant                  | Value | Description                                                  |
  | ------------------------- | ----- | ------------------------------------------------------------ |
  | Qt::WA_AcceptDrops        | 78    | 允许将来自拖放操作的数据拖放到小部件上(参见QWidget::setAcceptDrops())。 |
  | **Qt::WA_DeleteOnClose**  | 55    | 当小部件已接受关闭事件时，使Qt删除此小部件（请参阅QWidget :: closeEvent（））。 |
  | Qt::WA_AlwaysShowToolTips | 84    | 启用非活动窗口的工具提示。                                   |
  | Qt::WA_CustomWhatsThis    | 47    | 表示该小部件希望在“这是什么？”模式中继续正常运行。 这是由小部件的作者设置的。 |
  | Qt::WA_Disabled           | 0     | 表示该窗口小部件已禁用，即它没有收到任何鼠标或键盘事件。 还有一个getter功能QWidget :: isEnabled（）。 这是由Qt内核设置/清除的。 |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  |                           |       |                                                              |
  | Qt::WA_ContentsPropagated | 3     | 这个标志是多余的和过时的。 它不再具有任何作用。 从Qt 4.1开始，所有未设置WA_PaintOnScreen的小部件都会传播其内容。 |

- **`enum Qt::WindowType { Widget, Window, Dialog, Sheet, ..., WMacNoSheet }`**

  **`flags	WindowFlags`**

  此枚举类型用于为窗口小部件指定各种窗口系统属性。 它们相当不寻常，但在某些情况下是必需的。 其中一些标志取决于基础窗口管理器是否支持它们。

  | Constant         | Value                | Description                                                  |
  | ---------------- | -------------------- | ------------------------------------------------------------ |
  | Qt::Widget       | 0x00000000           | 这是QWidget的默认类型。 这种类型的小部件（如果有父级）是子级小部件，如果没有父级则是独立窗口。 另请参见Qt :: Window和Qt :: SubWindow。 |
  | Qt::Window       | 0x00000001           | 指示该窗口小部件是一个窗口，通常具有窗口系统框架和标题栏，而与窗口小部件是否具有父级无关。 请注意，如果小部件没有父级，则无法取消设置此标志。 |
  | Qt::Dialog       | 0x00000002 \| Window | 表示该窗口小部件是一个窗口，应将其装饰为对话框（即，标题栏中通常没有最大化或最小化按钮）。 这是QDialog的默认类型。 如果要将其用作**模态modal对话框**，则应从另一个窗口启动它，或者将其作为父窗口并与QWidget :: windowModality属性一起使用。 如果将其设置为态，则对话框将阻止应用程序中的其他顶级窗口获取任何输入。 我们将顶层窗口称为父窗口，将其作为辅助窗口。 |
  | Qt::Sheet        | 0x00000004 \| Window | 表示该窗口是Macintosh工作表。 由于使用工作表意味着窗口模态，因此推荐的方法是改用QWidget :: setWindowModality（）或QDialog :: open（）。 |
  | Qt::Drawer       | 0x00000006 \| Window | 表示该小部件是Macintosh drawer。                             |
  | Qt::Popup        | 0x00000008 \| Window | 指示该窗口小部件是弹出的顶级窗口，即它是模式窗口，但具有适合于弹出菜单的窗口系统框架。 |
  | Qt::Tool         | 0x0000000a \| Window | 指示该窗口小部件是工具窗口。 工具窗口通常是一个较小的窗口，其标题和装饰小于通常的标题栏和装饰，通常用于工具按钮的集合。 如果有父级，则工具窗口将始终保持在其顶部。 如果没有父母，您也可以考虑使用Qt :: **`WindowStaysOnTopHint`**。 如果窗户系统支持它，则可以用较轻的框架装饰工具窗。 它也可以与**`Qt :: FramelessWindowHint`**（无边框）结合使用。 在Mac OS X上，工具窗口对应于窗口的浮动类。 这意味着该窗口位于普通窗口之上的水平； 无法在其顶部放置普通窗口。 默认情况下，当应用程序处于非活动状态时，工具窗口将消失。 这可以由**`Qt :: WA_MacAlwaysShowToolWindow`**属性控制。 |
  | Qt::ToolTip      | 0x0000000c \| Window | 表示该小部件是工具提示。 在内部用于实现工具提示。            |
  | Qt::SplashScreen | 0x0000000e \| Window | 指示该窗口是初始屏幕。 这是QSplashScreen的默认类型。         |
  | Qt::Desktop      | 0x00000010 \| Window | 指示此窗口小部件是桌面。 这是QDesktopWidget的类型。          |
  | Qt::SubWindow    | 0x00000012           | 指示此窗口小部件是子窗口，例如QMdiSubWindow小部件。          |

  您还可以使用许多标志来自定义顶级窗口的外观。 这些对其他窗口没有影响：

  | Constant                               | Value      | Description                                                  |
  | -------------------------------------- | ---------- | ------------------------------------------------------------ |
  | **`Qt::MSWindowsFixedSizeDialogHint`** | 0x00000100 | 在Windows上为窗口提供细的对话框边框。 传统上，此样式用于固定大小的对话框。 |
  | Qt::MSWindowsOwnDC                     | 0x00000200 | 在Windows上为窗口提供自己的显示上下文。                      |
  | Qt::X11BypassWindowManagerHint         | 0x00000400 | 完全绕开窗口管理器。 这将导致根本无法管理的无边界窗口（即，除非您手动调用QWidget :: activateWindow（）否则就没有键盘输入）。 |
  | **`Qt::FramelessWindowHint`**          | 0x00000800 | 产生一个**无边界的窗口**。 用户无法通过窗口系统移动或调整无边界窗口的大小(需要自己重写鼠标事件才能移动，重写绘图事件绘制边框阴影)。 在X11上，标志的结果取决于窗口管理器及其理解Motif和/或NETWM提示的能力。 大多数现有的现代窗口管理器都可以处理此问题。 |

  **CustomizeWindowHint标志用于启用窗口控件的自定义**。 必须设置此标志以允许更改WindowTitleHint，WindowSystemMenuHint，WindowMinimizeButtonHint，WindowMaximizeButtonHint和WindowCloseButtonHint标志。

  | Constant                        | Value                                                | Description                                                  |
  | ------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ |
  | **`Qt::CustomizeWindowHint`**   | 0x02000000                                           | 关闭默认的窗口标题提示。                                     |
  | **`Qt::WindowStaysOnTopHint`**  | 0x00040000                                           | **通知窗口系统该窗口应保留在所有其他窗口之上**。 请注意，在X11上的某些窗口管理器上，您还必须传递Qt :: X11BypassWindowManagerHint，此标志才能正常工作。 |
  | Qt::WindowTitleHint             | 0x00001000                                           | 为窗口提供标题栏。                                           |
  | Qt::WindowSystemMenuHint        | 0x00002000                                           | 添加一个窗口系统菜单，并可能添加一个关闭按钮（例如，在Mac上）。 如果需要隐藏或显示关闭按钮，则使用WindowCloseButtonHint更加方便。 |
  | Qt::WindowMinimizeButtonHint    | 0x00004000                                           | 添加一个最小化按钮。 在某些平台上，这意味着Qt :: WindowSystemMenuHint可以正常工作。 |
  | Qt::WindowMaximizeButtonHint    | 0x00008000                                           | 添加一个最大化按钮。 在某些平台上，这意味着Qt :: WindowSystemMenuHint可以正常工作。 |
  | Qt::WindowMinMaxButtonsHint     | WindowMinimizeButtonHint \| WindowMaximizeButtonHint | 添加一个最小化和最大化按钮。 在某些平台上，这意味着Qt :: WindowSystemMenuHint可以正常工作。 |
  | Qt::WindowCloseButtonHint       | 0x08000000                                           | 添加一个关闭按钮。 在某些平台上，这意味着Qt :: WindowSystemMenuHint可以正常工作。 |
  | Qt::WindowContextHelpButtonHint | 0x00010000                                           | 在对话框中添加上下文帮助按钮。 在某些平台上，这意味着Qt :: WindowSystemMenuHint可以正常工作。 |
  | Qt::MacWindowToolBarButtonHint  | 0x10000000                                           | 在Mac OS X上，添加了一个工具栏按钮（即，带有工具栏的窗口右上方的长方形按钮）。 |
  | Qt::BypassGraphicsProxyWidget   | 0x20000000                                           | 如果已经嵌入了父窗口小部件，则防止窗口及其子级自动将其自身嵌入QGraphicsProxyWidget中。 如果希望小部件始终是桌面上的顶级小部件，则可以设置此标志，而不管父小部件是否嵌入场景中。 |
  | Qt::WindowShadeButtonHint       | 0x00020000                                           |                                                              |
  | **Qt::WindowStaysOnBottomHint** | 0x04000000                                           | 通知窗口系统该窗口应位于所有其他窗口的底部。 请注意，在X11上，此提示仅在支持_NET_WM_STATE_BELOW原子的窗口管理器中有效。 如果始终在底部的窗口有父级，则父级也将留在底部。 Mac OS X当前未实现此窗口提示。 |
  | Qt::WindowOkButtonHint          | 0x00080000                                           | 将“确定”按钮添加到对话框的窗口装饰中。 仅Windows CE支持。    |
  | Qt::WindowCancelButtonHint      | 0x00100000                                           | 在对话框的窗口装饰中添加“取消”按钮。 仅Windows CE支持。      |
  | Qt::WindowSoftkeysVisibleHint   | 0x40000000                                           | 当小部件全屏显示时，使软键可见。 仅支持Symbian。             |
  | Qt::WindowSoftkeysRespondHint   | 0x80000000                                           | 使软键即使在不可见时也可以接收键事件。 有了这个提示，即使软键不可见也将触发软键动作，即使用showFullscreen（）来显示窗口。 仅支持Symbian。 |
  | Qt::WindowType_Mask             | 0x000000ff                                           | 用于提取窗口标志的窗口类型部分的掩码。                       |

  

- enum	WindowFrameSection { NoSection, LeftSection, TopLeftSection, TopSection, ..., TitleBarArea }

- enum	WindowModality { NonModal, WindowModal, ApplicationModal }

- enum	WindowState { WindowNoState, WindowMinimized, WindowMaximized, WindowFullScreen, WindowActive }

- flags	WindowStates

## 2.Functions

## 3.Detailed Description

Qt名称空间包含在整个Qt库中使用的其他标识符。