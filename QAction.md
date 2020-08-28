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

- 