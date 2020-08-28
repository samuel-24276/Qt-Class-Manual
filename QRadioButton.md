#  QRadioButton广播按钮

继承关系：`QRadioButton`->`QAbstractButton`->`QWidget`

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

# 3.Public Functions

- `QRadioButton(const QString &text, QWidget *parent = nullptr)`
- `QRadioButton(QWidget *parent = nullptr)`
- `virtual ~QRadioButton()`

# 4.Reimplemented Public Functions

- `virtual QSize minimumSizeHint() const override`
- `virtual QSize sizeHint() const override`

# 5.Protected Functions

- `void initStyleOption(QStyleOptionButton *option) const`

# 6.Reimplemented Protected Functions

- `virtual bool event(QEvent *e) override`
- `virtual bool hitButton(const QPoint &pos) const override`
- `virtual void mouseMoveEvent(QMouseEvent *e) override`
- `virtual void paintEvent(QPaintEvent *) override`

