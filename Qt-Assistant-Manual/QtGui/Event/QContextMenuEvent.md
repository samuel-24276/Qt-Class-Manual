# QContextMenuEvent

继承关系：`QContextMenuEvent`->`QInputEvent `->`QEvent `

## 1.Detailed Description

当用户执行与打开上下文菜单关联的操作时，上下文菜单事件会发送到小部件。 在不同平台上，打开上下文菜单所需的操作有所不同。 例如，在Windows上，按菜单按钮或单击鼠标右键将导致发送此事件。
发生此事件时，通常会显示带有上下文菜单的QMenu（如果与上下文相关）。
上下文菜单事件包含一个特殊的接受标志，该标志指示接收者是否接受了该事件。 如果事件处理程序不接受该事件，则在可能的情况下，触发该事件的任何事件都将作为常规输入事件进行处理。

## 2.Public Types

- `enum	Reason { Mouse, Keyboard, Other }`

  该枚举描述了事件发送的原因。

  | Constant                    | Value | Description                                                  |
  | --------------------------- | ----- | ------------------------------------------------------------ |
  | QContextMenuEvent::Mouse    | 0     | 鼠标导致事件被发送。 通常，这意味着单击鼠标右键，但这取决于平台。 |
  | QContextMenuEvent::Keyboard | 1     | 键盘导致此事件被发送。 在Windows上，这意味着已按下菜单按钮。 |
  | QContextMenuEvent::Other    | 2     | 该事件是通过其他某种方式发送的（即不是通过鼠标或键盘发送的）。 |

## 3.Public Functions

- QContextMenuEvent ( Reason reason, const QPoint & pos, const QPoint & globalPos, Qt::KeyboardModifiers modifiers )
- QContextMenuEvent ( Reason reason, const QPoint & pos, const QPoint & globalPos )
- QContextMenuEvent ( Reason reason, const QPoint & pos )
- const QPoint &	globalPos () const
- int	globalX () const
- int	globalY () const
- const QPoint &	pos () const
- Reason	reason () const
- int	x () const
- int	y () const