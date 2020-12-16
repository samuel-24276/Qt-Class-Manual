# QSplitter布局分割器

继承关系：`QSplitter`->`QFrame`->`QWidget`->`QObject` and `QPaintDevice`

# 1. Properties

- `childrenCollapsible : bool`

  此属性保存**用户是否可以将子窗口小部件的大小调整为0**。
  默认情况下，子窗口是可折叠的。 使用setCollapsible（）可以启用和禁用单个子项的折叠。

- `handleWidth : int`

  此属性保存**拆分器手柄的宽度**。
  默认情况下，此属性包含一个值，该值取决于用户的平台和样式首选项。
  如果将handleWidth设置为1或0，则实际抓取区域将增加以重叠其各自小部件的几个像素。

- `opaqueResize : bool`

  如果在交互移动拆分器时动态（不透明）调整窗口小部件的大小，则返回true。 否则返回false。
  默认的调整大小行为取决于样式（由SH_Splitter_OpaqueResize样式提示确定）。 但是，您可以通过调用setOpaqueResize（）覆盖它。

- `orientation : Qt::Orientation `

  此属性**保留拆分器的方向**。
  默认情况下，方向是水平的（即，小部件并排放置）。 可能的方向是Qt :: Horizontal和Qt :: Vertical。

# 2. Public Functions

- `QSplitter(Qt::Orientation orientation, QWidget *parent = nullptr)`

- `QSplitter(QWidget *parent = nullptr)`

- `virtual ~QSplitter()`

- **`void addWidget(QWidget *widget)`**

  **将给定的小部件添加到拆分器的所有其他项目之后的布局**。
  如果窗口小部件已经在拆分器中，它将被移动到新位置。
  **注意：拆分器拥有窗口小部件的所有权**。

- **`void setSizes(const QList<int> &list)`**

  将子窗口部件的各自大小设置为列表list中给定的值。
  如果拆分器是水平的，则这些值将以像素为单位从左到右设置每个部件的宽度。 如果拆分器是垂直的，则将设置每个部件的高度，从上到下。
  列表中的其他值将被忽略。 如果list包含的值太少，则结果是不确定的，但是程序仍然表现良好。
  拆分器部件的整体大小不受影响。 取而代之的是，根据尺寸的相对权重，在窗口小部件之间分配任何额外/缺失的空间。
  如果将大小指定为0，则部件将不可见。 部件的大小策略将保留。 即，小于相应窗口部件的最小大小提示的值将由提示的值替换。

- **`QByteArray saveState() const`**

  **保存拆分器布局的状态**。
  **通常，它与QSettings结合使用以记住将来会话的大小**。 版本号作为数据的一部分存储。 这是一个例子：

  ```c++
  QSettings settings;
  settings.setValue("splitterSizes", splitter->saveState());
  ```

- **`bool restoreState(const QByteArray &state)`**

  **将拆分器的布局恢复到指定的状态**。 如果状态已恢复，则返回true；否则，返回false。 

  **通常，它与QSettings结合使用以从过去的会话中恢复大小**。 这是一个例子：

  ```c++
  QSettings settings;
  splitter->restoreState(settings.value("splitterSizes").toByteArray());
  ```

  所提供的字节数组中的数据无效或过期可能导致无法恢复拆分器的布局。

- `bool childrenCollapsible() const`

- `int count() const`

  返回拆分器布局中包含的小部件数量。

- `void getRange(int index, int *min, int *max) const`

  如果min和max不为0，则返回索引在min和max中的拆分器的有效范围。

- `QSplitterHandle *handle(int index) const`

  在给定的索引处返回拆分器布局中该项目左侧（或上方）的句柄；如果没有此类项目，则返回nullptr。 索引0处的句柄始终处于隐藏状态。
  对于从右到左的语言（例如阿拉伯语和希伯来语），水平分隔符的布局是相反的。 该句柄将位于窗口小部件右侧的索引处。

- `int handleWidth() const`

- `int indexOf(QWidget *widget) const`

  **返回指定窗口小部件的拆分器布局中的索引**；如果未找到窗口小部件，则返回-1。 这也适用于手柄。
  句柄从0开始编号。句柄与子窗口小部件一样多，但是位置0处的句柄始终被隐藏。

- `void insertWidget(int index, QWidget *widget)`

  **将指定的小部件插入给定索引处的拆分器布局**。
  如果窗口小部件已经在拆分器中，它将被移动到新位置。
  **如果index是一个无效索引，则该小部件将插入到末尾**。
  注意：拆分器拥有窗口小部件的所有权。

- `bool isCollapsible(int index) const`

  如果位于索引处的小部件可折叠，则返回true，否则返回false。

- `bool opaqueResize() const`

- `Qt::Orientation orientation() const`

- `void refresh()`

  更新拆分器的状态。 您不需要调用此函数。

- `QWidget *replaceWidget(int index, QWidget *widget)`

  **用widget替换给定索引处拆分器布局中的小部件**。
  如果index有效且widget不是拆分器的子级，则返回刚被替换的widget。 否则，它返回null，并且不进行任何替换或添加。
  新插入的小部件的几何形状将与其替换的小部件相同。 它的可见状态和折叠状态也被继承。
  **注意：拆分器拥有窗口小部件的所有权，并将替换后的窗口小部件的父级设置为null**。
  注意：由于窗口小部件重新绑定到拆分器中，因此可能无法立即设置其几何形状，只有在窗口小部件将接收到适当的事件之后，才能对其进行设置。

- `void setCollapsible(int index, bool collapse)`

  **设置index处的子窗口小部件是否可折叠以折叠**。
  默认情况下，子级是可折叠的，这意味着即使它们的miniSize（）或minimumSizeHint（）不为零，用户也可以将它们的大小调整为0。 可以通过调用此函数在每个小部件的基础上更改此行为，也可以通过设置childrenCollapsible属性对拆分器中的所有小部件进行全局更改。

- `void setHandleWidth(int)`

  设置分割器手柄的宽度。

- `void setOpaqueResize(bool opaque = true)`

- `void setOrientation(Qt::Orientation)`

- **`void setStretchFactor(int index, int stretch)`**

  更新位置index处的窗口小部件的大小策略以使其具有拉伸因子。
  stretch不是有效的拉伸因子； 有效拉伸因子是通过获取小部件的初始大小并将其乘以stretch来计算的。
  提供此功能是为了方便。 相当于

  ```c++
   QWidget *widget = splitter->widget(index);
   QSizePolicy policy = widget->sizePolicy();
   policy.setHorizontalStretch(stretch);
   policy.setVerticalStretch(stretch);
   widget->setSizePolicy(policy);
  ```

- `QList<int> sizes() const`

  **返回此拆分器中所有小部件的大小参数的列表**。
  如果拆分器的方向是水平的，则列表包含窗口小部件的宽度（以像素为单位），从左到右； 如果方向是垂直的，则列表从顶部到底部包含小部件的高度（以像素为单位）。
  将值提供给另一个拆分器的setSizes（）函数将生成一个与该拆分器具有相同布局的拆分器。
  请注意，不可见的小部件的大小为0。

- `QWidget *widget(int index) const`

  返回拆分器布局中给定索引处的小部件，如果没有此类小部件，则返回nullptr。

# 3. Reimplemented Public Functions

- `virtual QSize minimumSizeHint() const override`
- `virtual QSize sizeHint() const override`

# 4. Signals

- `void splitterMoved(int pos, int index)`

  **当位于特定index处的分离器手柄移至位置pos时，将发出此信号**。
  对于从右到左的语言（例如阿拉伯语和希伯来语），水平分隔符的布局是相反的。 pos是距小部件右边缘的距离。

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

**拆分器使用户可以通过拖动子控件之间的边界来控制它们的大小**。 单个拆分器可以控制任何数量的小部件。 QSplitter的典型用法是创建几个小部件，并使用insertWidget（）或addWidget（）添加它们。

下面的示例将并排显示一个QListView，QTreeView和QTextEdit，以及两个拆分器句柄：

```c++
     QSplitter *splitter = new QSplitter(parent);
     QListView *listview = new QListView;
     QTreeView *treeview = new QTreeView;
     QTextEdit *textedit = new QTextEdit;
     splitter->addWidget(listview);
     splitter->addWidget(treeview);
     splitter->addWidget(textedit);
```

如果在调用insertWidget（）或addWidget（）时，小部件已位于QSplitter中，则它将移至新位置。以后可以使用它来对拆分器中的小部件重新排序。您可以使用indexOf（），widget（）和count（）来访问拆分器内部的小部件。

**默认的QSplitter水平（并排）放置其子级**；您可以使用setOrientation（Qt :: Vertical）垂直放置其子级。

默认情况下，所有窗口小部件都可以根据用户的期望，在窗口小部件的minimumSizeHint（）（或minimumSize（））和maximumSize（）之间一样大或小。

**QSplitter默认情况下会动态调整其子级大小**。如果您希望QSplitter仅在调整大小操作结束时调整子项的大小，请调用setOpaqueResize（false）。

**小部件之间大小的初始分布是通过将初始大小乘以拉伸因子来确定的**。您还可以使用setSizes（）设置所有小部件的大小。函数size（）返回用户设置的大小。另外，您可以分别使用saveState（）和restoreState（）从QByteArray保存和恢复小部件的大小。

**当您隐藏（）一个孩子时，其空间将在其他孩子之间分配。当您再次显示它时，它将恢复**。
注意：**不支持向QSplitter添加QLayout（通过setLayout（）或使QSplitter成为QLayout的父级）；使用addWidget（）代替**（请参见上面的示例）。

