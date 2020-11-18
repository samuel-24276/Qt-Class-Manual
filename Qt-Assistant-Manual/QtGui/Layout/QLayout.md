# QLayout

继承关系：`QLayout`->`QObject` and `QLayoutItem`

继承者：

- QBoxLayout
- QFormLayout
- QGridLayout
- QStackedLayout

## 1.Public Types

- enum SizeConstraint { SetDefaultConstraint, SetFixedSize, SetMinimumSize, SetMaximumSize, SetMinAndMaxSize, SetNoConstraint }

  | Constant                      | Value | Description                                                  |
  | ----------------------------- | ----- | ------------------------------------------------------------ |
  | QLayout::SetDefaultConstraint | 0     | 主窗口小部件的最小大小设置为minimumSize（），除非窗口小部件已经具有最小大小。 |
  | QLayout::SetFixedSize         | 3     | 主窗口小部件的大小设置为sizeHint（）; 根本无法调整大小。     |
  | QLayout::SetMinimumSize       | 2     | 主窗口小部件的最小大小设置为minimumSize（）; 它不能更小。    |
  | QLayout::SetMaximumSize       | 4     | 主窗口小部件的最大大小设置为maximumSize（）; 它不能更大。    |
  | QLayout::SetMinAndMaxSize     | 5     | 主窗口小部件的最小大小设置为minimumSize（），其最大大小设置为maximumSize（）。 |
  | QLayout::SetNoConstraint      | 1     | 窗口大小没有限制                                             |

  

## 2.Properties

- sizeConstraint : SizeConstraint

  此属性保存布局的调整大小模式，默认模式为 SetDefaultConstraint

- spacing : int 

  **此属性保存布局内小部件之间的间距**。

  如果未显式设置任何值，则布局的间距将从父布局或父窗口小部件的样式设置继承。
  **对于QGridLayout和QFormLayout，可以使用setHorizontalSpacing（）和setVerticalSpacing（）设置不同的水平和垂直间距**。 在这种情况下，space（）返回-1。

## 3.Public Functions

- QLayout()

- QLayout(QWidget *parent)

- bool activate()

- virtual void addItem(QLayoutItem *item) = 0

  在子类中实现以添加项目。 如何添加它特定于每个子类。
  在应用程序代码中通常不调用此函数。 要将小部件添加到布局中，请使用addWidget（）函数； **要添加子布局，请使用相关QLayout子类提供的addLayout（）函数**。
  注意：项目的所有权已转移到布局，并且布局的责任是删除它。

- **void addWidget(QWidget *w)**

  以特定于布局的方式将小部件w添加到此布局。 此函数使用addItem（）。

- QMargins contentsMargins() const

- QRect contentsRect() const

- virtual int count() const = 0

- void getContentsMargins(int *left, int *top, int *right, int *bottom) const

- virtual int indexOf(QWidget *widget) const

  搜索此布局中的窗口小部件widget（不包括子布局）。
  返回widget的索引；如果未找到widget，则返回-1。

- int indexOf(QLayoutItem *layoutItem) const

  搜索此布局中的布局项目layoutItem（不包括子布局）。
  返回layoutItem的索引，如果未找到layoutItem，则返回-1。

- bool isEnabled() const

  如果启用了布局，则返回true；否则返回false。 

- virtual QLayoutItem *itemAt(int index) const = 0

- QWidget *menuBar() const

- QWidget *parentWidget() const

- **void removeItem(QLayoutItem *item)**

  **从布局中删除布局项目**。 删除项目是调用者的责任。
  请注意，该项可以是布局（因为QLayout继承了QLayoutItem）。

- **void removeWidget(QWidget *widget)**

  **从布局中删除窗口小部件widget。** 调用之后，调用方有责任为窗口小部件提供合理的几何形状，或将窗口小部件放回布局中，或在必要时显式隐藏它。
  注意：小部件的所有权与添加时的所有权相同。

- QLayoutItem *replaceWidget(QWidget *from, QWidget *to, Qt::FindChildOptions options = Qt::FindChildrenRecursively)

- bool setAlignment(QWidget *w, Qt::Alignment alignment)

- bool setAlignment(QLayout *l, Qt::Alignment alignment)

- void setContentsMargins(int left, int top, int right, int bottom)

- void setContentsMargins(const QMargins &margins)

- void setEnabled(bool enable)

- void setMenuBar(QWidget *widget)

- void setSizeConstraint(QLayout::SizeConstraint)

- void setSpacing(int)

- QLayout::SizeConstraint sizeConstraint() const

- int spacing() const

- virtual QLayoutItem *takeAt(int index) = 0

- void update()

## 4.Reimplemented Public Functions

- virtual QSizePolicy::ControlTypes controlTypes() const override
- virtual Qt::Orientations expandingDirections() const override
- virtual QRect geometry() const override
- virtual void invalidate() override
- virtual bool isEmpty() const override
- virtual QLayout *layout() override
- virtual QSize maximumSize() const override
- virtual QSize minimumSize() const override
- virtual void setGeometry(const QRect &r) override

## 5.Static Public Members

- QSize closestAcceptableSize(const QWidget *widget, const QSize &size)

## 6.Protected Functions

- void addChildLayout(QLayout *l)
- void addChildWidget(QWidget *w)
- QRect alignmentRect(const QRect &r) const

## 7.Reimplemented Protected Functions

- virtual void childEvent(QChildEvent *e) override

## 8.Detailed Description

这是由具体类QBoxLayout，QGridLayout，QFormLayout和QStackedLayout继承的**抽象基类**。

对于QLayout子类或QMainWindow的用户，几乎不需要使用QLayout提供的基本功能，例如setSizeConstraint（）或setMenuBar（）。 有关更多信息，请参见布局管理。
要创建自己的布局管理器，请实现函数addItem（），sizeHint（），setGeometry（），itemAt（）和takeAt（）。 您还应该实现minimumSize（），以确保如果空间太小，布局不会调整为零大小。 为了支持高度取决于其宽度的子级，请实现hasHeightForWidth（）和heightForWidth（）。 有关实现自定义布局管理器的更多信息，请参见Border Layout和Flow Layout示例。
删除布局管理器后，Geometry几何管理将停止。