# QAction

# 1.Public Types

- `enum ActionEvent { Trigger, Hover }`
- `enum MenuRole { NoRole, TextHeuristicRole, ApplicationSpecificRole, AboutQtRole, AboutRole, …, QuitRole }`
- `enum Priority { LowPriority, NormalPriority, HighPriority }`

# 2.Properties

- `autoRepeat : bool`
- `checkable : bool`
- `checked : bool`
- `enabled : bool`
- `font : QFont`
- `icon : QIcon`
- `iconText : QString`
- `iconVisibleInMenu : bool`
- `menuRole : MenuRole`
- `priority : Priority`
- `shortcut : QKeySequence`
- `shortcutContext : Qt::ShortcutContext`
- `shortcutVisibleInContextMenu : bool`
- `statusTip : QString`
- `text : QString`
- `toolTip : QString`
- `visible : bool`
- `whatsThis : QString`

# 3.Public Functions

- `QAction(const QIcon &icon, const QString &text, QObject *parent = nullptr)`

- `QAction(const QString &text, QObject *parent = nullptr)`

- `QAction(QObject *parent = nullptr)`

- `virtual ~QAction()`

- `void setCheckable(bool)`

  此属性保存该动作是否为可检查动作
  一种**可检查的动作是具有打开/关闭状态的动作**。 例如，在文字处理器中，粗体工具栏按钮可以打开或关闭。 **不是切换动作的动作是命令动作**。 简单地执行命令动作，例如 文件保存。 默认情况下，此属性为false。
  在某些情况下，一个切换动作的状态应取决于其他动作的状态。 例如，“左对齐”，“居中”和“右对齐”切换动作是互斥的。 要实现**独占切换**，请将相关的切换动作添加到QActionGroup :: exclusive属性设置为true的QActionGroup中。

- `void QAction::setSeparator(bool b)`

  如果b为true，则此操作将被视为分隔符。
  分隔符的表示方式取决于插入分隔符的小部件。 在大多数情况下，分隔符操作将忽略文本，子菜单和图标。

- `void setShortcut(const QKeySequence &shortcut)`

  `QKeySequence`类型的shortcut参数保存操作的主快捷键，该函数设置操作的快捷键。
  可在**`Qt :: Key`**和**`Qt :: Modifier`**中找到此属性的有效键码。 没有默认的快捷键。

- `void setStatusTip(const QString &statusTip)`

  QString类型的statusTip参数保存操作的状态提示。
  状态提示显示在操作的顶级父窗口小部件提供的所有状态栏上。
  默认情况下，此属性包含一个空字符串。

# 4.Public Slots

- void hover()
- void setChecked(bool)
- void setDisabled(bool b)
- void setEnabled(bool)
- void setVisible(bool)
- void toggle()
- void trigger()

# 5.Signals

- void changed()

  动作更改时将发出此信号。 如果您仅对给定窗口小部件中的动作感兴趣，则可以查看与`QEvent :: ActionChanged`一起发送的`QWidget :: actionEvent（）`。

  注意：属性autoRepeat的通知程序信号。 用于属性检查的通知程序信号。 已启用属性的通知程序信号。 属性字体的通知程序信号。 属性图标的通知程序信号。 属性iconText的通知程序信号。 属性iconVisibleInMenu的通知程序信号。 属性menuRole的通知程序信号。 属性快捷方式的通知程序信号。 属性shortcutContext的通知程序信号。 属性shortcutVisibleInContextMenu的通知程序信号。 属性状态的通知程序信号提示。 属性文本的通知程序信号。 属性工具提示的通知程序信号。 属性的通知程序信号可见。 属性whatsThis的通知程序信号。

- **void hovered()**

  当用户突出显示某个动作时，将发出此信号。 例如，当用户将光标停在菜单选项，工具栏按钮上或按操作的快捷键组合时。

- void toggled(bool checked)

  每当可检查操作更改其isChecked（）状态时，就会发出此信号。 这**可能是用户交互的结果，或者是因为调用了setChecked（）**。 当setChecked（）更改QAction时，除了toggled（）之外，它还会发出change（）。

  如果动作被选中，则checked为true；如果动作未被选中，则为false。

  注意：已检查属性的通知程序信号。

- void triggered(bool checked = false)

  当用户激活某个动作时，将发出此信号。 例如，当用户单击菜单选项，工具栏按钮或按操作的快捷键组合时，或在调用trigger（）时。 值得注意的是，当调用setChecked（）或toggle（）时，不会发出该消息。
  如果该动作是可检查的，则如果该动作被选中，则true；如果未选中该动作，则false。

