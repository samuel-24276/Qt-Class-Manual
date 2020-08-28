# QMenu

# 1.Properties

- `icon : QIcon`
- `separatorsCollapsible : bool`
- `tearOffEnabled : bool`
- `title : QString`
- `toolTipsVisible : bool`

# 2.Public Functions

- `QMenu(const QString &title, QWidget *parent = nullptr)`

- `QMenu(QWidget *parent = nullptr)`

- `virtual ~QMenu()`

- `QAction *actionAt(const QPoint &pt) const`

- `QRect actionGeometry(QAction *act) const`

- `QAction *activeAction() const`

- `QAction *addAction(const QString &text)`

- `QAction *addAction(const QIcon &icon, const QString &text)`

- `QAction *addAction(const QString &text, const QObject *receiver, const char *member, const QKeySequence &shortcut = 0)`

  此便利功能使用文本和可选的快捷方式创建新动作。 动作的trigger（）信号连接到接收者的成员插槽。 **该函数将新创建的动作添加到菜单的动作列表中并返回它**。
  QMenu拥有返回的QAction的所有权。

- `QAction *addAction(const QIcon &icon, const QString &text, const QObject *receiver, const char *member, const QKeySequence &shortcut = 0)`

- `QAction *addAction(const QString &text, Functor functor, const QKeySequence &shortcut = 0)`

- `QAction *addAction(const QString &text, const QObject *context, Functor functor, const QKeySequence &shortcut = 0)`

- `QAction *addAction(const QIcon &icon, const QString &text, Functor functor, const QKeySequence &shortcut = 0)`

- `QAction *addAction(const QIcon &icon, const QString &text, const QObject *context, Functor functor, const QKeySequence &shortcut = 0)`

- `QAction *addMenu(QMenu *menu)`

- `QMenu *addMenu(const QString &title)`

- `QMenu *addMenu(const QIcon &icon, const QString &title)`

- `QAction *addSection(const QString &text)`

- `QAction *addSection(const QIcon &icon, const QString &text)`

- `QAction *addSeparator()`

- `void clear()`

- `QAction *defaultAction() const`

- `QAction *exec()`

- `QAction *exec(const QPoint &p, QAction *action = nullptr)`

- `void hideTearOffMenu()`

- `QIcon icon() const`

- `QAction *insertMenu(QAction *before, QMenu *menu)
  QAction *insertSection(QAction *before, const QString &text)`

- `QAction *insertSection(QAction *before, const QIcon &icon, const QString &text)`

- `QAction *insertSeparator(QAction *before)`

- `bool isEmpty() const`

- `bool isTearOffEnabled() const`

- `bool isTearOffMenuVisible() const`

- `QAction *menuAction() const`

- `void popup(const QPoint &p, QAction *atAction = nullptr)`

- `bool separatorsCollapsible() const`

- `void setActiveAction(QAction *act)`

- `void setAsDockMenu()`

- `void setDefaultAction(QAction *act)`

- `void setIcon(const QIcon &icon)`

- `void setSeparatorsCollapsible(bool collapse)`

- `void setTearOffEnabled(bool)`

- `void setTitle(const QString &title)`

- `void setToolTipsVisible(bool visible)`

- `void showTearOffMenu(const QPoint &pos)`

- `void showTearOffMenu()`

- `QString title() const`

- `NSMenu *toNSMenu()`

- `bool toolTipsVisible() const`

# 3.Reimplemented Public Functions

`virtual QSize sizeHint() const override`

# 4.Signals

- `void aboutToHide()`

  就在用户隐藏菜单之前发出此信号。

- `void aboutToShow()`

  **在菜单显示给用户之前就发出该信号**。

- `void hovered(QAction *action)`

  突出显示菜单操作时会发出此信号。 动作是导致信号发出的动作。
  通常，这用于更新状态信息

- **`void triggered(QAction *action)`**

  触发此菜单中的动作时，将发出此信号。
  动作是导致信号发出的动作。
  通常，您将每个菜单动作的trigger（）信号连接到其自己的自定义插槽，但是有时您希望将多个动作连接到单个插槽，例如，当您有一组紧密相关的动作时，例如“ left justify” ，“中心”，“右对齐”。
  注意：此信号是为层次结构中的主父菜单发出的。 因此，只有父菜单需要连接到插槽。 子菜单无需连接。