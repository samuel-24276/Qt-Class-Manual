# QMouseEvent

继承关系：`QMouseEvent`->`QInputEvent `->`QEvent `

## 1.Public Functions

- QMouseEvent ( Type type, const QPoint & position, Qt::MouseButton button, Qt::MouseButtons buttons, Qt::KeyboardModifiers modifiers )

- QMouseEvent ( Type type, const QPoint & pos, const QPoint & globalPos, Qt::MouseButton button, Qt::MouseButtons buttons, Qt::KeyboardModifiers modifiers )

- **Qt::MouseButton	button () const**

  返回导致事件的按钮。

  请注意，对于鼠标移动事件，返回值始终为Qt :: NoButton。

- **Qt::MouseButtons	buttons () const**

  返回事件生成时的按钮状态。 按钮状态是使用OR运算符的Qt :: LeftButton，Qt :: RightButton，Qt :: MidButton的组合。 对于鼠标移动事件，这是所有按下的按钮。 对于鼠标按下和双击事件，这包括导致事件的按钮。 对于鼠标释放事件，这不包括引起事件的按钮。

- **const QPoint &	globalPos () const**

  **返回事件发生时鼠标光标的全局位置**。 这对于X11之类的异步窗口系统很重要。 每当响应鼠标事件而移动窗口小部件时，globalPos（）可能与当前指针位置QCursor :: pos（）以及QWidget :: mapToGlobal（pos（））相差很大。

- int	globalX () const

- int	globalY () const

- **const QPoint &	pos () const**

  返回鼠标光标**相对于接收事件的小部件的位置**。

  如果由于鼠标事件而移动了窗口小部件，请使用globalPos（）返回的全局位置以避免晃动。

- QPointF	posF () const

  以相对于接收事件的小部件的QPointF形式返回鼠标光标的位置。

  如果由于鼠标事件而移动了窗口小部件，请使用globalPos（）返回的全局位置以避免晃动。

  >QPointF类使用浮点精度在平面中定义一个点。
  >
  >一个点由x坐标和y坐标指定，可以使用x（）和y（）函数进行访问。 为了精确起见，使用浮点数指定了点的坐标。 如果x和y都设置为0.0，则isNull（）函数将返回true。 可以使用setX（）和setY（）函数，或者使用rx（）和ry（）函数来设置（或更改）坐标，这些函数可以返回对坐标的引用（允许直接操作）。

- int	x () const

- int	y () const

## 2.Detailed Description

QMouseEvent类包含描述鼠标事件的参数。

当在小部件内按下或释放鼠标按钮或移动鼠标光标时，会发生鼠标事件。

除非已通过QWidget :: setMouseTracking（）启用了鼠标跟踪，否则只有在按下鼠标按钮时才会发生鼠标移动事件。

>mouseTracking属性保存是否为窗口小部件启用了鼠标跟踪。
>
>如果禁用了鼠标跟踪（默认设置），则仅在移动鼠标时按下至少一个鼠标按钮时，窗口小部件才会接收鼠标移动事件。
>
>如果启用了鼠标跟踪，则即使未按任何按钮，窗口小部件也会接收鼠标移动事件。

当在小部件内按下鼠标按钮时，Qt会自动抓住鼠标。小部件将继续接收鼠标事件，直到释放最后一个鼠标按钮。

鼠标事件包含一个**特殊的接受标志**，该标志**指示接收者是否想要该事件**。如果小部件未处理鼠标事件，则应调用ignore（）。**鼠标事件将在父窗口小部件链上传播，直到窗口小部件使用accept（）接受它，或者事件过滤器将其消耗掉为止**。

注意：如果将鼠标事件传播到已设置了Qt :: WA_NoMousePropagation的窗口小部件，则该鼠标事件将不会在父窗口小部件链中进一步传播。

可以通过调用从QInputEvent继承的Modifys（）函数来找到键盘修饰键的状态。

函数pos（），x（）和y（）给出**相对于接收鼠标事件的小部件的光标位置**。如果由于鼠标事件而移动了窗口小部件，请使用globalPos（）返回的全局位置以避免晃动。

**QWidget :: setEnabled（）函数可用于启用或禁用小部件的鼠标和键盘事件**。

重新实现QWidget事件处理程序，QWidget :: mousePressEvent（），QWidget :: mouseReleaseEvent（），QWidget :: mouseDoubleClickEvent（）和QWidget :: mouseMoveEvent（），以在您自己的窗口小部件中接收鼠标事件。