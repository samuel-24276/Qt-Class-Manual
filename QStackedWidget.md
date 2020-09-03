# QStackedWidget

继承关系：`QStackedWidget`->`QFrame`->`QWidget`->`QObject and QPaintDevice`

# 1.Properties

- `count : const int`

  堆栈窗口包含的窗口数量

- `currentIndex : int`

  堆栈窗口中可见窗口的索引位置
  如果没有当前窗口，则当前索引为-1。
  默认情况下，此属性包含值-1，因为堆栈最初是空的。

# 2.Public Functions

- `QStackedWidget(QWidget *parent = nullptr)`

- `virtual ~QStackedWidget()`

- `int addWidget(QWidget *widget)`

  将给定的窗口部件追加到QStackedWidget并返回索引位置。 窗口部件的所有权传递给QStackedWidget。
  如果在调用此函数之前QStackedWidget为空，则窗口部件将成为当前窗口。

- `int count() const`

  堆栈窗口包含的窗口数量，默认值为0。

- `int currentIndex() const`

  堆栈窗口中可见窗口的索引位置
  如果没有当前窗口，则当前索引为-1。
  默认情况下，此属性包含值-1，因为堆栈最初是空的。

- `QWidget *currentWidget() const`

  返回当前窗口部件，如果没有子窗口部件，则返回nullptr。

- `int indexOf(QWidget *widget) const`

  返回给定窗口部件的索引；如果给定窗口部件不是QStackedWidget的子级，则返回-1。

- `int insertWidget(int index, QWidget *widget)`

  将给定的窗口部件插入QStackedWidget中的给定索引处。 窗口部件的所有权传递给QStackedWidget。 **如果index超出范围，则将附加窗口部件（在这种情况下，它是返回的窗口部件的实际索引）**。
  如果在调用此函数之前QStackedWidget为空，则给定的窗口部件将成为当前窗口。
  **在小于或等于当前索引的索引处插入新窗口部件将增加当前索引，但保留当前窗口小部件**。

- `void removeWidget(QWidget *widget)`

  从QStackedWidget中删除窗口部件。 也就是说，**窗口部件不会被删除，而只是从堆叠的布局中删除，从而使其被隐藏。**
  注意：窗口部件的父对象和父窗口部件将保留为QStackedWidget。 **如果应用程序要重用已删除的窗口小部件，则建议对其重新父化。**

- `QWidget *widget(int index) const`

  返回给定索引的窗口部件；如果没有这样的窗口部件，则返回nullptr。

# 3.Public Slots

- `void setCurrentIndex(int index)`

  设置当前堆栈窗口所展示的窗口的索引。

- `void setCurrentWidget(QWidget *widget)`

  将当前窗口部件设置为指定的窗口部件。 当前的新窗口部件必须已经包含在此堆叠窗口部件中。

# 4.Signals

- `void currentChanged(int index)`

  每当当前窗口部件更改时，都会发出此信号。
  该参数保存新的当前窗口部件的索引，如果没有新的窗口部件，则为-1（例如，如果QStackedWidget中没有小部件）。
  note：属性currentIndex的通知程序信号。

- `void widgetRemoved(int index)`

  每当删除窗口部件时，都会发出此信号。 窗口部件的索引作为参数传递。

# 5.Reimplemented Protected Functions

- `virtual bool event(QEvent *e) override`

  最终由QObject实现，这是主事件处理程序； 它处理事件事件。 您可以在子类中重新实现此函数，但是我们建议改用一种专用的事件处理程序。
  按键和释放事件与其他事件的处理方式有所不同。 event（）检查Tab和Shift + Tab并尝试适当地移动焦点。 如果没有将焦点移至的小部件（或者按键不是Tab或Shift + Tab），则event（）会调用keyPressEvent（）。
  鼠标和平板电脑的事件处理也有些特殊：仅当启用小部件时，event（）才会调用专门的处理程序，例如mousePressEvent（）;。 否则将丢弃该事件。
  如果事件被识别，则此函数返回true，否则返回false。 如果识别的事件被接受（请参见QEvent :: accepted），则任何进一步的处理（例如，事件传播到父窗口小部件）都将停止。

# 6.Detailed Description

QStackedWidget可用于创建类似于QTabWidget提供的用户界面。 它是在QStackedLayout类顶部构建的便捷布局部件。
与QStackedLayout一样，QStackedWidget可以被构造并填充许多子窗口部件（“页面”）：

```c++
QWidget *firstPageWidget = new QWidget;
QWidget *secondPageWidget = new QWidget;
QWidget *thirdPageWidget = new QWidget;

QStackedWidget *stackedWidget = new QStackedWidget;
stackedWidget->addWidget(firstPageWidget);
stackedWidget->addWidget(secondPageWidget);
stackedWidget->addWidget(thirdPageWidget);

QVBoxLayout *layout = new QVBoxLayout;
layout->addWidget(stackedWidget);
setLayout(layout);
```

QStackedWidget没有为用户提供切换页面的内在手段。 这通常是通过QComboBox或QListWidget完成的，该QComboBox或QListWidget存储QStackedWidget页面的标题。 例如：

```c++
QComboBox *pageComboBox = new QComboBox;
pageComboBox->addItem(tr("Page 1"));
pageComboBox->addItem(tr("Page 2"));
pageComboBox->addItem(tr("Page 3"));
connect(pageComboBox, QOverload<int>::of(&QComboBox::activated), stackedWidget, &QStackedWidget::setCurrentIndex);
```

当填充堆叠的窗口部件时，这些窗口部件将添加到内部列表中。 indexOf（）函数返回该列表中部件的索引。 可以使用addWidget（）函数将窗口部件添加到列表的末尾，或者使用insertWidget（）函数将窗口部件插入给定的索引。 removeWidget（）函数从堆叠的部件中删除小部件。 可以使用count（）函数获取堆叠的部件中包含的部件数量。
widget（）函数在给定的索引位置返回部件。 屏幕上显示的窗口部件的索引由currentIndex（）给出，可以使用setCurrentIndex（）进行更改。 以类似的方式，可以使用currentWidget（）函数检索当前显示的窗口小部件，并使用setCurrentWidget（）函数对其进行更改。
每当堆叠的窗口小部件中的当前窗口部件发生更改或从堆叠的窗口部件中删除窗口部件时，都会分别发出currentChanged（）和widgetRemoved（）信号。