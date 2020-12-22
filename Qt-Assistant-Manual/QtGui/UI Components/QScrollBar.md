# QScrollBar

继承关系：`QScrollBar`->`QAbstractSlider `->`QWidget`->`QObject and QPaintDevice`

![qss样式表学习](http://file.elecfans.com/web1/M00/46/76/o4YBAFqeNriAVTMnAABrZDJ8GeI953.png)

## 1.Public Functions

- QScrollBar ( QWidget * parent = 0 )
- QScrollBar ( Qt::Orientation orientation, QWidget * parent = 0 )
- ~QScrollBar ()

## 2.Reimplemented Public Functions

- virtual bool	event ( QEvent * event )
- virtual QSize	sizeHint () const

## 3.Protected Functions

- void	initStyleOption ( QStyleOptionSlider * option ) const

## 4.Reimplemented Protected Functions

- virtual void	contextMenuEvent ( QContextMenuEvent * event )
- virtual void	hideEvent ( QHideEvent * )
- virtual void	mouseMoveEvent ( QMouseEvent * e )
- virtual void	mousePressEvent ( QMouseEvent * e )
- virtual void	mouseReleaseEvent ( QMouseEvent * e )
- virtual void	paintEvent ( QPaintEvent * )
- virtual void	sliderChange ( SliderChange change )

## 5.Detailed Description

QScrollBar小部件提供垂直或水平滚动条。

滚动条是一种控件，使用户可以访问文档中大于用于显示文档的窗口小部件的部分。 它提供了用户在文档中当前位置以及可见文档量的可视指示。 **滚动条通常配有其他控件，可以实现更准确的导航**。 Qt以适合每个平台的方式显示滚动条。

如果需要在另一个窗口小部件上提供滚动视图，则使用QScrollArea类可能更方便，因为它提供了视口窗口小部件和滚动条。 如果需要使用QAbstractScrollArea为专用小部件实现类似的功能，则QScrollBar很有用。 例如，如果您决定子类化QAbstractItemView。 对于使用滑块控件获取给定范围内的值的大多数其他情况，QSlider类可能更适合您的需求。

滚动条通常包括四个单独的控件：滑块，滚动箭头和页面控件。

- a 滑块提供了一种快速访问文档任何部分的方法，但不支持在大型文档中进行精确导航。
- b 滚动箭头是按钮，可用于精确导航到文档中的特定位置。 对于连接到文本编辑器的垂直滚动条，这些滚动条通常将当前位置上移或下移一个“行”，并少量调整滑块的位置。 在编辑器和列表框中，“一行”可能表示一行文本； 在图像查看器中可能意味着20像素。
- c 页面控件是拖动滑块的区域（滚动条的背景）。 单击此处将滚动条移向单击一个“页面”。 该值通常与滑块的长度相同。

每个滚动条都有一个值，该值指示滑块与滚动条起点的距离。这是通过value（）获得的，并通过setValue（）进行设置的。此值始终在为滚动条定义的值的范围内，从minimum（）到maximum（）（包括两端）。可以使用setMinimum（）和setMaximum（）设置可接受值的范围。在最小值时，滑块的顶部边缘（对于垂直滚动条）或左边缘（对于水平滚动条）将在滚动条的顶部（或左侧）。在最大值时，滑块的底部（或右侧）边缘将在滚动条的底部（或右侧）末端。

滑块的长度通常与页面步长有关，并且通常代表滚动视图中显示的文档区域的比例。 Page step是用户按下Page Up和Page Down键时值更改的量，并使用setPageStep（）进行设置。使用光标键对行步定义的值进行较小的更改，并使用setSingleStep（）设置此数量。

请注意，所使用的值的范围与滚动条小部件的实际大小无关。选择范围和页面步长的值时，无需考虑这一点。

为滚动条指定的值范围通常与为QSlider确定的值范围不同，因为需要考虑滑块的长度。如果我们有一个包含100行的文档，并且在一个小部件中只能显示20行，则我们可能希望构建一个滚动条，其页面步长为20，最小值为0，最大值为80。给我们一个带有五个“页面”的滚动条。

在许多常见情况下，文档长度，滚动条中使用的值范围和页面步进之间的关系很简单。 滚动条的值范围是通过从代表文档长度的某个值中减去选定的页面步长来确定的。 在这种情况下，以下等式很有用：文档长度= maximum（）-minimum（）+ pageStep（）。

QScrollBar仅提供整数范围。 请注意，尽管QScrollBar可以处理非常大的数字，但当前屏幕上的滚动条无法有效地表示约100,000像素以上的范围。 除此之外，用户变得难以使用键盘或鼠标来控制滑块，并且滚动箭头的使用将受到限制。

ScrollBar从QAbstractSlider继承了一组全面的信号：

- 滚动条的值更改时将发出valueChanged（）。 tracking（）确定在用户交互过程中是否发出此信号。
- 滚动条的值范围已更改时，会发出rangeChanged（）。
- 当用户开始拖动滑块时，将发出sliderPressed（）。
- 当用户拖动滑块时，将发出sliderMoved（）。
- 当用户释放滑块时，将发出sliderReleased（）。
- 当通过用户交互或通过triggerAction（）函数更改滚动条时，将发出actionTriggered（）。

滚动条可以由键盘控制，但是它的默认focusPolicy（）为Qt :: NoFocus。 **使用setFocusPolicy（）启用键盘与滚动条的交互**：

- 向左/向右移动水平滚动条仅一步。
- 向上/向下单步移动垂直滚动条。
- PageUp向上移动一页。
- PageDown向下移动一页。
- Home移至起点（最小）。
- 结束移动到末尾（最大）。

滑块本身可以通过使用triggerAction（）函数来控制，以模拟用户与滚动条控件的交互。 如果您有许多使用共同值范围的不同小部件，这将很有用。

大多数GUI样式使用pageStep（）值来计算滑块的大小。

