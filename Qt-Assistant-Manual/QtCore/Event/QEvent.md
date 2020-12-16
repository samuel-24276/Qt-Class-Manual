# QEvent

继承者：

- `QCloseEvent`
- `QShowEvent`
- `QPaintEvent`
- `QMoveEvent`
- QHideEvent
- QHoverEvent
- QIconDragEvent
- QInputEvent
- QInputMethodEvent
- QResizeEvent
- QShortcutEvent
- QStatusTipEvent
- QTimerEvent, 
- QWhatsThisClickedEvent
- QWindowStateChangeEvent
- QAccessibleEvent
- QActionEvent
- QChildEvent
- QCustomEvent
- QDragLeaveEvent
- QDropEvent
- QDynamicPropertyChangeEvent
- QFileOpenEvent
- QFocusEvent
- QGestureEvent
- QGraphicsSceneEvent
- QHelpEvent

## 1.Public Types

- `enum	Type { None, AccessibilityDescription, AccessibilityHelp, AccessibilityPrepare, ..., MaxUser }`

  此枚举类型定义Qt中的有效事件类型。 事件类型和每种类型的专用类如下：

  

## 2.Properties

- accepted : bool

## 3.Public Functions

- QEvent ( Type type )

- virtual	~QEvent ()

- void	accept ()

  设置事件对象的接受标志，等效于调用setAccepted（true）。 **设置accept参数表示事件接收者想要该事件。 不需要的事件可能会传播到父窗口小部件**。

- void	ignore ()

  **清除事件对象的接受标志参数，等效于调用setAccepted（false）。 清除accept参数表示事件接收者不需要该事件。 不需要的事件可能会传播到父窗口小部件**。

- bool	isAccepted () const

- void	setAccepted ( bool accepted )

- bool	spontaneous () const

  如果事件起源于应用程序之外，则返回true（系统事件）； 否则返回false。 没有为绘画事件定义此函数的返回值。

- Type	type () const

  返回事件类型。

## 4.Static Public Members

- int	registerEventType ( int hint = -1 )

## 5.Detailed Description

QEvent类是所有事件类的基类。事件对象包含事件参数。 

Qt的主事件循环（QCoreApplication :: exec（））从事件队列中获取本机窗口系统事件，将其转换为QEvents，然后将转换后的事件发送给QObjects。 

通常，事件来自基础窗口系统（spontaneous（）返回true），但是也可以使用QCoreApplication :: sendEvent（）和QCoreApplication :: postEvent（）手动发送事件（spontaneous（）返回false）。 

QObject通过调用其QObject :: event（）函数来接收事件。可以在子类中重新实现该函数，以自定义事件处理并添加其他事件类型。 QWidget :: event（）是一个著名的例子。**默认情况下，事件被分派到事件处理程序**，例如QObject :: timerEvent（）和QWidget :: mouseMoveEvent（）。 QObject :: installEventFilter（）允许一个对象拦截发往另一个对象的事件。 

**基本的QEvent仅包含事件类型参数和“ accept”标志。接受标志设置为accept（），并使用ignore（）清除**。它是默认设置的，但是不要依赖它，因为子类可以选择在其构造函数中清除它。

 QEvent的子类包含描述特定事件的其他参数。