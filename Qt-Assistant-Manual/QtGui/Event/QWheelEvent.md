# QWheelEvent滚轮事件

继承关系：`QWheelEvent`->`QInputEvent`->`QEvent`

## 1.Public Functions

- QWheelEvent ( const QPoint & pos, int delta, Qt::MouseButtons buttons, Qt::KeyboardModifiers modifiers, Qt::Orientation orient = Qt::Vertical )

- QWheelEvent ( const QPoint & pos, const QPoint & globalPos, int delta, Qt::MouseButtons buttons, Qt::KeyboardModifiers modifiers, Qt::Orientation orient = Qt::Vertical )

- Qt::MouseButtons	buttons () const

  返回事件发生时的鼠标状态。

- int	delta () const

  返回滚轮旋转的距离，八分之一度。**正值表示滚轮向前旋转，远离用户;负值表示滚轮向后旋转，朝向用户**。

  大多数鼠标类型以15度为步长工作，在这种情况下，增量值是120的倍数;即120单位* 1/8 = 15度。

  然而，一些小鼠标拥有更高分辨率的滚轮，发送的delta值小于120单位(小于15度)。为了支持这种可能性，您可以累计添加事件的增量值，直到达到120为止，然后滚动小部件，或者您可以部分滚动小部件以响应每个wheel事件。

  ```c++
   void MyWidget::wheelEvent(QWheelEvent *event)
   {
       int numDegrees = event->delta() / 8;
       int numSteps = numDegrees / 15;
  
       if (event->orientation() == Qt::Horizontal) {
           scrollHorizontally(numSteps);
       } else {
           scrollVertically(numSteps);
       }
       event->accept();
   }
  ```

- const QPoint &	globalPos () const

  返回事件发生时鼠标指针的全局位置。这在异步窗口系统(如X11)中非常重要;每当您移动小部件以响应鼠标事件时，globalPos()可能与QCursor::pos()返回的当前光标位置有很大差异。

- int	globalX () const

  返回事件发生时鼠标光标的全局x位置。

- int	globalY () const

  返回事件发生时鼠标光标的全局y位置。

- Qt::Orientation	orientation () const

  返回滚轮的方向。

- const QPoint &	pos () const

  返回鼠标光标相对于接收事件的小部件的位置。

  如果您移动小部件以响应鼠标事件，请使用globalPos()而不是此函数。

- int	x () const

  返回相对于接收事件的小部件的鼠标光标的x位置。

- int	y () const

  返回相对于接收事件的小部件的鼠标光标的y位置。

## 2.Detailed Description

QWheelEvent类包含描述滚轮事件的参数。

滚轮事件被发送到鼠标光标下的小部件，但是如果小部件不处理事件，它们就被发送到焦点小部件。旋转距离由delta()提供。函数pos()和globalPos()返回事件发生时鼠标光标的位置。

滚轮事件包含一个特殊的接受标志，该标志指示接收者是否需要该事件。如果不处理wheel事件，则应该调用ignore();这确保它将被发送到父小部件。

setEnabled()函数可以用来启用或禁用小部件的鼠标和键盘事件。

事件处理程序QWidget::wheelEvent()接收滚轮事件。