# QComboBox

# 0.常见用法

## 0.1.组合框的当前项更改，窗口切换

编写对应于`void currentIndexChanged(int index)`信号的槽函数`onCurrentIndexChanged(int index)`，槽函数内判断当前index，根据不同的index显示不同的窗口，其他窗口隐藏。注意，窗口切换失败可能是因为你把别的窗口widget放在了需要显示widegt里面，它们是平级窗口关系不是父子窗口的关系。之后在窗口初始化后监听该信号`connect(ui->comProtocol, SIGNAL(currentIndexChanged(int)), this, SLOT(onCurrentIndexChanged(int)));`，当然监听信号之前需要把展示`show()`和隐藏`hide()`的窗口设置好，否则会混杂在一起。所有的这些窗口可以放置在一个groupBox下，根据不同的窗口，groupBox可以设置不同的名字`setTitle(QString)`。

# 1.Detailed Description

QComboBox提供了一种以占用最少屏幕空间的方式向用户显示选项列表的方法。

combobox 是显示当前项目的选择小部件，并且可以弹出可选项目的列表。组合框可能是可编辑的，允许用户修改列表中的每个项目。

组合框可以包含像素图和字符串。适当地重载了`insertItem（）`和`setItemText（）`函数。对于可编辑的组合框，提供了函数`clearEditText（）`，以清除显示的字符串而不更改组合框的内容。
**如果组合框的当前项发生更改，则将发出三个信号：`currentIndexChanged（）`，`currentTextChanged（）`和`activated（）`**。无论更改是通过编程方式还是通过用户交互完成，始终都会发出`currentIndexChanged（）`和`currentTextChanged（）`，而仅当更改是由用户交互引起时才发出`activate（）`。当用户突出显示组合框弹出列表中的一个项目时，将发出`highlighted（）`信号。所有这三种信号都有两种版本，一种带有QString参数，另一种带有int参数。如果用户选择或突出显示像素图，则仅会发出int信号。只要更改了可编辑组合框的文本，就会发出`editTextChanged（）`信号。

当用户在可编辑的组合框中输入新字符串时，该窗口小部件可能会插入也可能不会插入，并且可以将其插入多个位置。默认策略是`InsertAtBottom`，但是您可以使用`setInsertPolicy（）`进行更改。
使用`QValidator`可以将输入限制为可编辑的组合框。请参见`setValidator（）`。默认情况下，接受任何输入。

例如，可以使用插入函数`insertItem（）`和`insertItems（）`来填充组合框。可以使用`setItemText（）`更改项目。可以使用`removeItem（）`删除项目，并且可以使用clear（）删除所有项目。当前项目的文本由`currentText（）`返回，而编号项目的文本由`text（）`返回。可以使用`setCurrentIndex（）`设置当前项目。组合框中的项目数由`count（）`返回；可以使用`setMaxCount（）`设置最大项目数。您可以使用`setEditable（）`进行编辑。对于可编辑的组合框，您可以使用`setCompleter（）`设置自动完成功能，并使用`setDuplicatesEnabled（）`设置用户是否可以添加重复项。
QComboBox使用模型/视图框架为其弹出列表并存储其项目。默认情况下，`QStandardItemModel`存储项目，而`QListView`子类显示弹出列表。您可以直接访问模型和视图（使用model（）和view（）），但是QComboBox还提供用于设置和获取项目数据的函数（例如`setItemData（）`和`itemText（）`）。您还可以设置新模型和视图（使用`setModel（）`和`setView（）`）。对于组合框标签中的文本和图标，使用模型中具有`Qt :: DisplayRole`和`Qt :: DecorationRole`的数据。请注意，您无法更改view（）的SelectionMode，例如，使用`setSelectionMode（）`。

# 2.Public Types

- `enum InsertPolicy { NoInsert, InsertAtTop, InsertAtCurrent, InsertAtBottom, InsertAfterCurrent, …, InsertAlphabetically }`
- `enum SizeAdjustPolicy { AdjustToContents, AdjustToContentsOnFirstShow, AdjustToMinimumContentsLengthWithIcon }`

# 3.Properties

- `count : const int`
- `currentData : const QVariant`
- `currentIndex : int`
- `currentText : QString`
- `duplicatesEnabled : bool`
- `editable : bool`
- `frame : bool`
- `iconSize : QSize`
- `insertPolicy : InsertPolicy`
- `maxCount : int`
- `maxVisibleItems : int`
- `minimumContentsLength : int`
- `modelColumn : int`
- `placeholderText : QString`
- `sizeAdjustPolicy : SizeAdjustPolicy`

# 4.Public Functions

- `QComboBox(QWidget *parent = nullptr)`

- `void addItem(const QString &text, const QVariant &userData = QVariant())`

  使用给定的文本将一个项目添加到组合框中，并包含指定的userData（存储在Qt :: UserRole中）。 该项目将追加到现有项目列表中。在这里userData 应该使用`QAccessible::CheckBox`，同时包含头文件`#include<QAccessible>`

- `void addItem(const QIcon &icon, const QString &text, const QVariant &userData = QVariant())`

  icon是组合框的项的图标

- `void addItems(const QStringList &texts)`

  texts是添加的一系列项的列表。

- `QCompleter *completer() const`

- `int count() const`

- `QVariant currentData(int role = Qt::UserRole) const`

- `int currentIndex() const`

- `QString currentText() const`

- `bool duplicatesEnabled() const`

- `int findData(const QVariant &data, int role = Qt::UserRole, Qt::MatchFlags flags = static_cast<Qt::MatchFlags>(Qt::MatchExactly|Qt::MatchCaseSensitive)) const`

- `int findText(const QString &text, Qt::MatchFlags flags = Qt::MatchExactly|Qt::MatchCaseSensitive) const`

- `bool hasFrame() const`

- `virtual void hidePopup()`

- `QSize iconSize() const`

- `void insertItem(int index, const QString &text, const QVariant &userData = QVariant())`

- `void insertItem(int index, const QIcon &icon, const QString &text, const QVariant &userData = QVariant())`

- `void insertItems(int index, const QStringList &list)`

- `QComboBox::InsertPolicy insertPolicy() const`

- `void insertSeparator(int index)`

- `bool isEditable() const`

- `QVariant itemData(int index, int role = Qt::UserRole) const`

- `QAbstractItemDelegate *itemDelegate() const`

- `QIcon itemIcon(int index) const`

- `QString itemText(int index) const`

- `QLineEdit *lineEdit() const`

- `int maxCount() const`

- `int maxVisibleItems() const`

- `int minimumContentsLength() const`

- `QAbstractItemModel *model() const`

- `int modelColumn() const`

- `QString placeholderText() const`

- `void removeItem(int index)`

- `QModelIndex rootModelIndex() const`

- `void setCompleter(QCompleter *completer)`

- `void setDuplicatesEnabled(bool enable)`

- `void setEditable(bool editable)`

- `void setFrame(bool)`

- `void setIconSize(const QSize &size)`

- `void setInsertPolicy(QComboBox::InsertPolicy policy)`

- `void setItemData(int index, const QVariant &value, int role = Qt::UserRole)`

- `void setItemDelegate(QAbstractItemDelegate *delegate)`

- `void setItemIcon(int index, const QIcon &icon)`

- `void setItemText(int index, const QString &text)`

- `void setLineEdit(QLineEdit *edit)`

- `void setMaxCount(int max)`

- `void setMaxVisibleItems(int maxItems)`

- `void setMinimumContentsLength(int characters)`

- `void setModel(QAbstractItemModel *model)`

- `void setModelColumn(int visibleColumn)`

- `void setPlaceholderText(const QString &placeholderText)`

- `void setRootModelIndex(const QModelIndex &index)`

- `void setSizeAdjustPolicy(QComboBox::SizeAdjustPolicy policy)`

- `void setValidator(const QValidator *validator)`

- `void setView(QAbstractItemView *itemView)`

- `virtual void showPopup()`

- `QComboBox::SizeAdjustPolicy sizeAdjustPolicy() const`

- `const QValidator *validator() const`

- `QAbstractItemView *view() const`

# 5.Reimplemented Public Functions

- `virtual bool event(QEvent *event) override`
- `virtual QVariant inputMethodQuery(Qt::InputMethodQuery query) const override`
- `virtual QSize minimumSizeHint() const override`
- `virtual QSize sizeHint() const override`

# 6.Public Slots

- void clear()
- void clearEditText()
- void setCurrentIndex(int index)
- void setCurrentText(const QString &text)
- void setEditText(const QString &text)

# 7.Signals

- `void activated(int index)`
- `void currentIndexChanged(int index)`
- `void currentTextChanged(const QString &text)`
- `void editTextChanged(const QString &text)`
- `void highlighted(int index)`
- `void textActivated(const QString &text)`
- `void textHighlighted(const QString &text)`

# 8.Protected Functions

- `void initStyleOption(QStyleOptionComboBox *option) const`

# 9.Reimplemented Protected Functions

- `virtual void changeEvent(QEvent *e) override`

- `virtual void contextMenuEvent(QContextMenuEvent *e) override`

- `virtual void focusInEvent(QFocusEvent *e) override`

- `virtual void focusOutEvent(QFocusEvent *e) override`

- `virtual void hideEvent(QHideEvent *e) override`

- `virtual void inputMethodEvent(QInputMethodEvent *e) override`

- `virtual void keyPressEvent(QKeyEvent *e) override`

- `virtual void keyReleaseEvent(QKeyEvent *e) override`

- `virtual void mousePressEvent(QMouseEvent *e) override`

- `virtual void mouseReleaseEvent(QMouseEvent *e) override`

- `virtual void paintEvent(QPaintEvent *e) override`

- `virtual void resizeEvent(QResizeEvent *e) override`

- `virtual void showEvent(QShowEvent *e) override`

- `virtual void wheelEvent(QWheelEvent *e) override`

  





