# QSplitter布局分割器

# 1. Properties

- `childrenCollapsible : bool`
- `handleWidth : int`
- `opaqueResize : bool`
- `orientation : Qt::Orientation `

# 2. Public Functions

- `QSplitter(Qt::Orientation orientation, QWidget *parent = nullptr)`

- `QSplitter(QWidget *parent = nullptr)`

- `virtual ~QSplitter()`

- `void addWidget(QWidget *widget)`

- `bool childrenCollapsible() const`

- `int count() const`

- `void getRange(int index, int *min, int *max) const`

- `QSplitterHandle *handle(int index) const`

- `int handleWidth() const`

- `int indexOf(QWidget *widget) const`

- `void insertWidget(int index, QWidget *widget)`

- `bool isCollapsible(int index) const`

- `bool opaqueResize() const`

- `Qt::Orientation orientation() const`

- `void refresh()`

- `QWidget *replaceWidget(int index, QWidget *widget)`

- `bool restoreState(const QByteArray &state)`

- `QByteArray saveState() const`

- `void setChildrenCollapsible(bool)`

- `void setCollapsible(int index, bool collapse)`

- `void setHandleWidth(int)`

- `void setOpaqueResize(bool opaque = true)`

- `void setOrientation(Qt::Orientation)`

- `void setSizes(const QList<int> &list)`

  将子窗口部件的各自大小设置为列表list中给定的值。
  如果拆分器是水平的，则这些值将以像素为单位从左到右设置每个部件的宽度。 如果拆分器是垂直的，则将设置每个部件的高度，从上到下。
  列表中的其他值将被忽略。 如果list包含的值太少，则结果是不确定的，但是程序仍然表现良好。
  拆分器部件的整体大小不受影响。 取而代之的是，根据尺寸的相对权重，在窗口小部件之间分配任何额外/缺失的空间。
  如果将大小指定为0，则部件将不可见。 部件的大小策略将保留。 即，小于相应窗口部件的最小大小提示的值将由提示的值替换。

- `void setStretchFactor(int index, int stretch)`

- `QList<int> sizes() const`

- `QWidget *widget(int index) const`

# 3. Reimplemented Public Functions

- `virtual QSize minimumSizeHint() const override`
- `virtual QSize sizeHint() const override`

# 4. Signals

- `void splitterMoved(int pos, int index)`

# 5. Protected Functions

- `int closestLegalPosition(int pos, int index)`
- `virtual QSplitterHandle *createHandle()`
- `void moveSplitter(int pos, int index)`
- `void setRubberBand(int pos)`

# 6. Reimplemented Protected Functions

- `virtual void changeEvent(QEvent *ev) override`
- `virtual void childEvent(QChildEvent *c) override`
- `virtual bool event(QEvent *e) override`
- `virtual void resizeEvent(QResizeEvent *) override`

# 7. Detailed Description

