# QAbstractButton按钮基类

# 1.Signals

- `void clicked(bool checked = false)`点击信号
- `void pressed()`按压信号
- `void released()`释放信号
- `void toggled(bool checked)`切换信号

# 2.Public Slots

- `void animateClick(int msec = 100)`

  执行动画点击：立即按下该按钮，并在毫秒后释放（默认值为100毫秒），可以实现按下按钮后按钮图片浮动的效果。
  释放按钮之前再次调用此功能将重置释放计时器。
  与点击相关的所有信号都会适当发出。
  如果禁用该按钮，则此功能不起作用。

- `void click()`

  单击。
  会适当发出与click相关的所有常规信号。 如果按钮是可选择(checkable)的，则将切换按钮的状态。
  如果禁用该按钮，则此功能不起作用。

- `void setChecked(bool)`设置选中状态

- `void setIconSize(const QSize &size)`设置按钮显示的图像大小

- `void toggle()`切换可检查按钮的状态。