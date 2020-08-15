#  QRadioButton广播按钮

继承自抽象按钮`QAbstractButton`，

# 1.Signals

- `void clicked(bool checked = false)`按钮点击信号

- `void pressed()`按钮按下信号
- `void released()`按钮松开信号

- `void toggled(bool checked)`按钮切换信号

# 2.Public Slots

- `void animateClick(int msec = 100)`
- `void click()`点击
- `void setChecked(bool)`设置选中槽
- `void setIconSize(const QSize &size)`设置按钮图标大小
- `void toggle()`按钮切换