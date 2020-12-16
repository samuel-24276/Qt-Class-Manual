# QEvent

继承者：

- QAccessibleEvent
- QActionEvent
- QChildEvent
- QCloseEvent
- QCustomEvent
- QDragLeaveEvent
- QDropEvent
- QDynamicPropertyChangeEvent
-  QFileOpenEvent
-  QFocusEvent
- QGestureEvent
- QGraphicsSceneEvent
- QHelpEvent
- QHideEvent
- QHoverEvent
- QIconDragEvent 
- QInputEvent
- QInputMethodEvent
- QMoveEvent
- QPaintEvent
- QResizeEvent
- QShortcutEvent
- QShowEvent 
- QStatusTipEvent
- QTimerEvent
- QWhatsThisClickedEvent
- QWindowStateChangeEvent

## 1.Public Types

- `enum	Type { None, AccessibilityDescription, AccessibilityHelp, AccessibilityPrepare, ..., MaxUser }`

  | Constant                        | Value | Description                                           |
  | ------------------------------- | ----- | ----------------------------------------------------- |
  | QEvent::None                    | 0     | Not an event.                                         |
  | QEvent::Close                   | 19    | Widget was closed (QCloseEvent).                      |
  | QEvent::CloseSoftwareInputPanel | 200   | 小部件要关闭软件输入面板（SIP）。                     |
  | QEvent::ContextMenu             | 82    | Context popup menu (QContextMenuEvent).               |
  | QEvent::DragEnter               | 60    | 光标在拖放操作（QDragEnterEvent）期间进入小部件。     |
  | QEvent::DragLeave               | 62    | 光标在拖放操作（QDragLeaveEvent）期间离开窗口小部件。 |
  | QEvent::DragMove                | 61    | 正在进行拖放操作（QDragMoveEvent）。                  |
  | QEvent::Drop                    | 63    | 拖放操作完成（QDropEvent）。                          |
  | QEvent::Enter                   | 10    | 鼠标进入小部件的边界。                                |
  | QEvent::Hide                    | 18    | Widget was hidden (QHideEvent).                       |
  | QEvent::HideToParent            | 27    | A child widget has been hidden.                       |
  | QEvent::HoverEnter              | 127   | 鼠标光标进入一个悬停窗口小部件（QHoverEvent）。       |
  | QEvent::HoverLeave              | 128   | 鼠标光标离开一个悬停窗口小部件（QHoverEvent）。       |
  | QEvent::HoverMove               | 129   | 鼠标光标在悬停窗口小部件（QHoverEvent）内移动。       |
  | QEvent::KeyPress                | 6     | Key press (QKeyEvent).                                |
  | QEvent::KeyRelease              | 7     | Key release (QKeyEvent).                              |
  | QEvent::Leave                   | 11    | 鼠标离开小部件的边界。                                |
  | QEvent::LeaveEditFocus          | 151   | 编辑器小部件失去了编辑的焦点。                        |
  | QEvent::EnterEditFocus          | 150   | 编辑器小部件获得了编辑的焦点。                        |
  | **QEvent::MouseButtonDblClick** | 4     | 鼠标双击 (QMouseEvent).                               |
  | **QEvent::MouseButtonPress**    | 2     | 鼠标按下(QMouseEvent).                                |
  | **QEvent::MouseButtonRelease**  | 3     | 鼠标释放(QMouseEvent).                                |
  | **QEvent::MouseMove**           | 5     | 鼠标移动(QMouseEvent).                                |
  | QEvent::MouseTrackingChange     | 109   | 鼠标追踪的状态被改变                                  |
  | QEvent::Move                    | 13    | 小部件的位置已更改（QMoveEvent）。                    |
  | QEvent::Paint                   | 12    | 屏幕更新是必需的（QPaintEvent）。                     |
  | QEvent::Show                    | 17    | Widget was shown on screen (QShowEvent).              |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |
  |                                 |       |                                                       |

  

## 2.Properties

- accepted : bool

  事件对象的接受标志

  设置accept参数表示事件接收者想要该事件。 不需要的事件可能会传播到父窗口小部件。 默认情况下，isAccepted（）设置为true，但是不要依赖于此，因为子类可以选择在其构造函数中清除它。

## 3.Public Functions

- QEvent ( Type type )

- virtual	~QEvent ()

- void	accept ()

  设置事件对象的接受标志，等效于调用setAccepted（true）。

  设置accept参数表示事件接收者想要该事件。 不需要的事件可能会传播到父窗口小部件。

- void	ignore ()

  清除事件对象的接受标志参数，等效于调用setAccepted（false）。

  清除accept参数表示事件接收者不需要该事件。 不需要的事件可能会传播到父窗口小部件。

- bool	isAccepted () const

- void	setAccepted ( bool accepted )

- bool	spontaneous () const

  如果事件起源于应用程序之外，则返回true（系统事件）； 否则返回false。

  没有为绘画事件定义此函数的返回值。

- Type	type () const

  返回事件类型。