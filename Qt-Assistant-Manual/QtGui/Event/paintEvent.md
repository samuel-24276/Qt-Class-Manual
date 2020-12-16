# paintEvent

`void QWidget::paintEvent ( QPaintEvent * event ) [virtual protected]`

可以在子类中重新实现此事件处理程序，以接收事件中传递的绘画事件。

绘制事件是重新绘制小部件的全部或一部分的请求。 可能由于以下原因之一而发生：

- 调用了repaint（）或update（），
- 该小部件已被遮盖，现已被发现，或者
  许多其他原因。

许多窗口小部件在需要时可以简单地重绘整个表面，但是一些慢速窗口小部件需要通过仅绘制请求的区域来优化：QPaintEvent :: region（）。此速度优化不会更改结果，因为在事件处理期间将绘画裁剪到该区域。例如，QListView和QTableView就是这样做的。

Qt还尝试通过将多个绘画事件合并为一个来加快绘画速度。当多次调用update（）或窗口系统发送多个绘制事件时，Qt会将这些事件合并为一个具有较大区域的事件（请参见QRegion :: united（））。 repaint（）函数不允许这种优化，因此我们建议尽可能使用update（）。

发生绘画事件时，通常会擦除更新区域，因此您正在小部件的背景上绘画。

可以使用setBackgroundRole（）和setPalette（）设置背景。

从Qt 4.0开始，QWidget自动对其绘画进行双缓冲，因此无需在paintEvent（）中编写双缓冲代码来避免闪烁。

X11平台注意事项：可以通过调用qt_x11_set_global_double_buffer（）来切换全局双缓冲。例如，

```c++
 ...
 extern void qt_x11_set_global_double_buffer(bool);
 qt_x11_set_global_double_buffer(false);
 ...
```

注意：通常，应避免在paintEvent（）内部调用update（）或repaint（）。 例如，在paintevent（）内部的子级上调用update（）或repaint（）会导致未定义的行为。 孩子可能会也可能不会参加绘画活动。

警告：如果您使用的自定义绘画引擎没有Qt的后备存储，则必须设置Qt :: WA_PaintOnScreen。 否则，QWidget :: paintEngine（）将永远不会被调用； 将使用后备存储。

