# QLineEdit

继承关系：`QLineEdit`->`QWidget`->`QObject and QPaintDevice`

## 1.Public Types

- enum ActionPosition { LeadingPosition, TrailingPosition }

  此枚举类型描述了行编辑应如何显示要添加的操作窗口小部件。

  | Constant                    | Value | Description                                                  |
  | --------------------------- | ----- | ------------------------------------------------------------ |
  | QLineEdit::LeadingPosition  | 0     | 使用布局方向Qt :: LeftToRight时，小部件显示在文本的左侧；使用Qt :: RightToLeft时，小部件显示在文本的右侧。 |
  | QLineEdit::TrailingPosition | 1     | 使用布局方向Qt :: LeftToRight时，小部件显示在文本的右侧；使用Qt :: RightToLeft时，小部件显示在文本的左侧。 |

  

- enum EchoMode { Normal, NoEcho, Password, PasswordEchoOnEdit }

  此枚举类型描述行编辑应如何显示其内容。

  | Constant                      | Value | Description                                                 |
  | ----------------------------- | ----- | ----------------------------------------------------------- |
  | QLineEdit::Normal             | 0     | 输入时显示字符。 这是默认值。                               |
  | QLineEdit::NoEcho             | 1     | 不显示任何内容。 这可能适用于密码，即使密码的长度也应保密。 |
  | QLineEdit::Password           | 2     | 显示平台相关的密码掩码字符，而不是实际输入的字符。          |
  | QLineEdit::PasswordEchoOnEdit | 3     | 编辑时显示输入的字符，否则显示与密码相同的字符。            |

  

## 2.Properties

- acceptableInput : const bool

  此属性保存输入是否满足inputMask和验证器。
  默认情况下，此属性为true。

- alignment : Qt::Alignment

  此属性保存行编辑的对齐方式。

  这里允许水平和垂直对齐，Qt :: AlignJustify将映射到Qt :: AlignLeft。

  默认情况下，此属性包含Qt :: AlignLeft和Qt :: AlignVCenter的组合。

- clearButtonEnabled : bool

  此属性保存当行编辑不为空时是否显示清除按钮。
  如果启用，则行编辑在包含某些文本时会显示一个尾随的清除按钮，否则，行编辑不会显示清除按钮（默认）。

- **cursorMoveStyle : Qt::CursorMoveStyle**

  此属性保存此行编辑中光标的移动样式。

  当此属性设置为Qt :: VisualMoveStyle时，行编辑将使用视觉移动样式。 无论文本的书写方向如何，按左箭头键都将始终导致光标向左移动。 右箭头键也有相同的行为。
  当属性为Qt :: LogicalMoveStyle（默认值）时，在LTR文本块中，按左箭头键时增加光标位置，按右箭头键时减少光标位置。 如果文本块从右到左，则适用相反的行为。

- cursorPosition : int

  此属性保存此行编辑的当前光标位置。

  设置光标位置会在适当时重绘。

  默认情况下，此属性的值为0。

- displayText : const QString

  此属性保存显示的文本。

  如果echoMode为Normal，则返回与text（）相同的值； 如果EchoMode为Password或PasswordEchoOnEdit，则它返回一个与平台相关的密码掩码字符串，其大小为text（）。length（），例如 “ ******”； 如果EchoMode为NoEcho，则返回一个空字符串“”。

  默认情况下，此属性包含一个空字符串。

- **dragEnabled : bool**

  如果用户在某些选定的文本上按下并移动鼠标，则lineedit是否开始拖动。
  默认情况下禁用拖动。

- **echoMode : EchoMode**

  此属性保存行编辑的显示模式。

  显示模式确定在行编辑中输入的文本如何显示（或回显）给用户。

  最常见的设置是“正常”，其中用户输入的文本将按原样显示，但是QLineEdit还支持允许抑制或模糊输入的文本的模式：这些模式包括NoEcho，Password和PasswordEchoOnEdit。

  窗口小部件的显示以及复制或拖动文本的能力受此设置的影响。

  默认情况下，此属性设置为“Normal”。

- frame : bool

  此属性保存行编辑是否使用框架绘制自身。

  如果启用（默认设置），则行编辑将自己绘制在框架内，否则行编辑将绘制自身而没有任何框架。

- hasSelectedText : const bool

  此属性保存是否选择了任何文本。

  如果用户选择了部分或全部文本，则hasSelectedText（）返回true；否则返回false。

  默认情况下，此属性为false。

- **inputMask : QString**

  此属性保存验证输入掩码。

  如果未设置任何掩码，则inputMask（）返回一个空字符串。

  设置QLineEdit的验证掩码。 可以使用验证程序来代替掩码，也可以与掩码一起使用； 请参见setValidator（）。

  通过传递空字符串（“”），取消设置遮罩并返回正常的QLineEdit操作。

  输入掩码是输入模板字符串。 它可以包含以下元素：

  掩码角色	定义在此位置被认为有效的输入字符的类别
  元字符		各种特殊含义
  分离器		所有其他字符均视为不可变的分隔符

  下表显示了可在输入掩码中使用的掩码和元字符。

  | Mask Character | Meaning                                           |
  | -------------- | ------------------------------------------------- |
  | A              | 必需的字母类别的字符，例如A-Z，a-z。              |
  | a              | 字母类别的字符允许，但不是必需的。                |
  | N              | 要求的字母或数字类别的字符，例如A-Z，a-z，0-9。   |
  | n              | 字母或数字类别的字符允许，但不是必需的。          |
  | X              | 所需的任何非空白字符。                            |
  | x              | 允许但不是必需的任何非空白字符。                  |
  | 9              | 所需的数字类别的字符，例如0-9。                   |
  | 0              | 数字类别的字符允许，但不是必需的。                |
  | D              | 数字类别的字符，且必须大于零，例如1-9             |
  | d              | 数字类别的字符，并且允许但不要求大于零，例如1-9。 |
  | #              | 数字类别的字符，或允许但不要求加号/减号。         |
  | H              | 必须为十六进制字符。 A-F，a-f，0-9。              |
  | h              | 允许使用十六进制字符，但不是必需的。              |
  | B              | 必须为二进制字符。 0-1。                          |
  | b              | 允许使用二进制字符，但不是必需的。                |

  

  | Meta Character | Meaning                                         |
  | -------------- | ----------------------------------------------- |
  | \>             | 以下所有字母字符均大写。                        |
  | \<             | 以下所有字母字符均小写。                        |
  | \!             | 关闭大小写转换。                                |
  | ;c             | 终止输入掩码并将空白字符设置为c。               |
  | []{}           | 保留。                                          |
  | \\             | 使用\转义上面列出的特殊字符以将它们用作分隔符。 |

  创建或清除后，行编辑将使用输入掩码字符串的副本填充，其中已删除了元字符，并且掩码字符已替换为空白字符（默认为空格）。

  设置输入掩码后，text（）方法将返回行编辑内容的修改后的副本，其中所有空白字符均已删除。 可以使用displayText（）读取未修改的内容。

  如果行编辑的当前内容不满足输入掩码的要求，则hasAcceptableInput（）方法将返回false。

  | Mask掩码                          | Notes                                                      |
  | --------------------------------- | ---------------------------------------------------------- |
  | 000.000.000.000;_                 | IP地址; 空格为_。                                          |
  | HH:HH:HH:HH:HH:HH;_               | MAC地址                                                    |
  | 0000-00-00                        | ISO日期； 空白是空格                                       |
  | \>AAAAA-AAAAA-AAAAA-AAAAA-AAAAA;# | 许可证号; 空格为＃，并且所有（字母）字符均转换为大写字母。 |

  要获得范围控制（例如，用于IP地址），请使用掩码和验证程序。

- maxLength : int

  此属性保存文本的最大允许长度。

  **如果文本太长，则会在限制处将其截断**。

  **如果发生截断，则将取消选择任何选定的文本，将光标位置设置为0，并显示字符串的第一部分**。

  如果行编辑具有输入掩码，则掩码定义最大字符串长度。

  默认情况下，此属性包含一个值32767。

- modified : bool

  此属性保存用户是否修改了行编辑的内容。

  QLineEdit永远不会读取修改后的标志。 它具有默认值false，并且每当用户更改行编辑的内容时，它就会更改为true。

  这对于需要提供默认值但又不知道默认值是什么的东西很有用（也许它取决于表单上的其他字段）。 在没有最佳默认值的情况下开始行编辑，当默认值已知时，如果Modifyed（）返回false（用户未输入任何文本），请插入默认值。

  调用setText（）会将修改后的标志重置为false。

- placeholderText : QString

  此属性**保存行编辑的占位符文本**。

  设置此属性会使行编辑在行编辑为空的情况下显示为灰色的占位符文本。

  通常，空行编辑将显示占位符文本，即使它具有焦点。 但是，如果内容水平居中，则当行编辑具有焦点时，占位符文本不会显示在光标下方。

  默认情况下，此属性包含一个空字符串。

- readOnly : bool

  此属性保存行编辑是否为只读。

  在只读模式下，用户仍可以将文本复制到剪贴板，或拖放文本（如果echoMode（）为Normal），但不能对其进行编辑。

  QLineEdit在只读模式下不显示光标。

  默认情况下，此属性为false。

- redoAvailable : const bool

  此属性保存重做是否可用。

  一旦用户对行编辑中的文本执行了一个或多个撤消操作，则重做变为可用。

  默认情况下，此属性为false。

- selectedText : const QString

  此属性保存选定的文本。

  如果没有选择的文本，则此属性的值为空字符串。

  默认情况下，此属性包含一个空字符串。

- text : QString

  此属性保存行编辑的文本。

  **设置此属性将清除选择，清除撤消/重做历史记录，将光标移至该行的末尾，并将修改后的属性重置为false。 使用setText（）插入时，不会验证文本**。

  文本被截断为maxLength（）长度。

  默认情况下，此属性包含一个空字符串。

- undoAvailable : const bool

  此属性保存撤消是否可用。

  **一旦用户在行编辑中修改了文本，撤消将变为可用**。
  默认情况下，此属性为false。

## 3.Public Functions

- QLineEdit(const QString &contents, QWidget *parent = nullptr)

- QLineEdit(QWidget *parent = nullptr)

- virtual ~QLineEdit()

- void addAction(QAction *action*, QLineEdit::ActionPosition position)

  将*action*添加到该位置的actions列表中。

- QAction *addAction(const QIcon &icon, QLineEdit::ActionPosition position)

  使用给定图标在该位置创建一个新动作。

- Qt::Alignment alignment() const

- void backspace()

  如果未选择任何文本，则删除文本光标左侧的字符，然后将光标向左移动一个位置。 如果选择了任何文本，则光标将移动到所选文本的开头，并删除所选文本。

- QCompleter *completer() const

  返回提供补全的当前QCompleter。

- QMenu *createStandardContextMenu()

  此功能创建标准上下文菜单，**当用户使用鼠标右键单击行编辑时将显示该菜单**。 从默认的contextMenuEvent（）处理函数中调用它。 弹出菜单的所有权已转移给调用者。

- **void cursorBackward(bool mark, int steps = 1)**

  将光标后退一步字符。 如果mark为true，则将每个移出的字符添加到选择中； 如果mark为false，则清除选择。

  和shift + Arrow ->/<-有关。

- **void cursorForward(bool mark, int steps = 1)**

  将光标向前移动步进字符。 如果mark为true，则将每个移出的字符添加到选择中； 如果mark为false，则清除选择。

  和shift + Arrow ->/<-有关。

- Qt::CursorMoveStyle cursorMoveStyle() const

- int cursorPosition() const

- int cursorPositionAt(const QPoint &pos)

  返回光标在pos点下的位置。

- void cursorWordBackward(bool mark)

  向后移动光标一个单词（字）。 如果mark为true，则还会选择该单词。

- void cursorWordForward(bool mark)

  向前移动光标一个单词（字）。 如果mark为true，则还会选择该单词。

- void del()

  如果未选择任何文本，则删除文本光标右侧的字符。 如果选择了任何文本，则光标将移动到所选文本的开头，并删除所选文本。

- void deselect()

  取消选择任何选定的文本。

- QString displayText() const

- bool dragEnabled() const

- QLineEdit::EchoMode echoMode() const

- void end(bool mark)

  将文本光标移动到该行的末尾，除非它已经在那里。 如果mark为true，则选择文本到最后一个位置。 否则，如果移动了光标，则任何选定的文本都不会被选中。

- bool hasAcceptableInput() const

- bool hasFrame() const

- bool hasSelectedText() const

- void home(bool mark)

  除非文本光标已在行首，否则将其移动到该行的开头。 如果mark为true，则选择文本到第一个位置。 否则，如果移动了光标，则任何选定的文本都不会被选中。

- QString inputMask() const

- void insert(const QString &newText)

  删除任何选定的文本，插入newText并验证结果。 如果有效，则将其设置为行编辑的新内容。

- bool isClearButtonEnabled() const

- bool isModified() const

- bool isReadOnly() const

- bool isRedoAvailable() const

- bool isUndoAvailable() const

- int maxLength() const

- QString placeholderText() const

- QString selectedText() const

- int selectionEnd() const

  直接在行编辑中选择之后返回字符的索引；如果未选择任何文本，则返回-1。

- int selectionLength() const

  返回选择的长度。

- int selectionStart() const

  返回行编辑中第一个选定字符的索引；如果未选择任何文本，则返回-1。

- void setAlignment(Qt::Alignment flag)

- void setClearButtonEnabled(bool enable)

- void setCompleter(QCompleter *c)

  设置此行编辑以提供来自completer的自动完成，c。 使用QCompleter :: setCompletionMode（）设置完成模式。

  要将QCompleter与QValidator或QLineEdit :: inputMask一起使用，您需要确保提供给QCompleter的模型包含有效条目。 您可以使用QSortFilterProxyModel来确保QCompleter的模型仅包含有效条目。

  如果c == 0，则setCompleter（）删除当前的完成程序，有效地禁用自动完成功能。

- void setCursorMoveStyle(Qt::CursorMoveStyle style)

- void setCursorPosition(int)

- void setDragEnabled(bool b)

- void setEchoMode(QLineEdit::EchoMode)

- void setFrame(bool)

- void setInputMask(const QString &inputMask)

- void setMaxLength(int)

- void setModified(bool)

- void setPlaceholderText(const QString &)

- void setReadOnly(bool)

- void setSelection(int start, int length)

  从位置开始和长度字符中选择文本。 **允许负长度**。

- void setTextMargins(int left, int top, int right, int bottom)

  将框架内文本周围的边距设置为左侧，顶部，右侧和底部。

- void setTextMargins(const QMargins &margins)

  在框架内的文本周围设置边距。

- void setValidator(const QValidator *v)

  将行编辑值的验证器设置为v。

  仅当v将行编辑的内容确认为“可接受”时，才发出行编辑的returnPressed（）和editedFinished（）信号。 用户可以在编辑过程中将内容更改为任何中间值，但将被禁止将文本编辑为v验证为无效的值。

  这使您可以限制在编辑完成后最终要输入的文本，同时使用户有足够的自由将文本从一种有效状态编辑到另一种有效状态。

  如果v == 0，则setValidator（）删除当前输入验证器。 初始设置是没有输入验证器（即，最大maxLength（）都可接受任何输入）。

- QString text() const

- QMargins textMargins() const

  返回窗口小部件的文本边距。

- const QValidator *validator() const

  返回指向当前输入验证器的指针，如果未设置验证器，则返回nullptr。

## 4.Reimplemented Public Functions

- virtual bool event(QEvent *e) override
- virtual QVariant inputMethodQuery(Qt::InputMethodQuery property) const override
- virtual QSize minimumSizeHint() const override
- virtual QSize sizeHint() const override

## 5.Public Slots

- void clear()

  清空文本框内容。

- void copy() const

  如果有文本，并且echoMode（）为Normal，则将所选文本复制到剪贴板。

- void cut()

  将所选文本复制到剪贴板，如果有，并且echoMode（）为Normal，则将其删除。

  如果当前验证器不允许删除所选文本，则cut（）将复制而不删除。

- void paste()

  如果行编辑不是只读的，则将剪贴板的文本插入光标位置，删除所有选定的文本。

  如果最终结果对当前的验证程序无效，则什么都不会发生。

- void redo()

  如果可以重做，则重做上一个操作。

- void selectAll()

  选择所有文本（即突出显示文本）并将光标移到末尾。 当插入默认值时，这很有用，因为如果用户在单击窗口小部件之前键入内容，则所选文本将被删除。

- void setText(const QString &)

- void undo()

  如果撤消可用，则撤消上一次操作。 取消选择任何当前选择，并将选择开始更新为当前光标位置。

## 6.Signals

- void cursorPositionChanged(int oldPos, int newPos)

  每当光标移动时，都会发出此信号。 上一个光标位置由oldPos赋予，新光标位置由newPos赋予。

- void editingFinished()

  当按下Return或Enter键或行编辑失去焦点时，将发出此信号。 请注意，如果在行编辑中设置了validator（）或inputMask（）并按下了enter / return，则仅当输入跟随在inputMask（）上并且validator（）返回QValidator :: Acceptable时，才会发出editingFinished（）信号。

- void inputRejected()

  当用户按下不可接受的键时，将发出此信号。 例如，如果按键导致验证器的validate（）调用返回Invalid。 另一种情况是尝试输入超出行编辑最大长度的更多字符。

  注意：在部分文本被接受但并非全部被接受的情况下，该信号仍然会发出。 例如，如果设置了最大长度，并且剪贴板文本比粘贴时的最大长度长。

- void returnPressed()

  当按下Return或Enter键时，将发出此信号。 请注意，如果在行编辑中设置了validator（）或inputMask（），则仅当输入跟随inputMask（）并且validator（）返回QValidator :: Acceptable时，才会发出returnPressed（）信号。

- void selectionChanged()

  选择更改时，将发出此信号。

- void textChanged(const QString &text)

  每当文本更改时，都会发出此信号。 text参数是新文本。

  与textEdited（）不同，例如，通过调用setText（）以编程方式更改文本时，也会发出此信号。

- void textEdited(const QString &text)

  每当编辑文本时，都会发出此信号。 text参数是新文本。

  与textChanged（）不同，例如，通过调用setText（）以编程方式更改文本时，不会发出此信号。

## 7.Protected Functions

- QRect cursorRect() const
- void initStyleOption(QStyleOptionFrame *option) const

## 8.Reimplemented Protected Functions

- virtual void changeEvent(QEvent *ev) override
- virtual void contextMenuEvent(QContextMenuEvent *event) override
- virtual void dragEnterEvent(QDragEnterEvent *e) override
- virtual void dragLeaveEvent(QDragLeaveEvent *e) override
- virtual void dragMoveEvent(QDragMoveEvent *e) override
- virtual void dropEvent(QDropEvent *e) override
- virtual void focusInEvent(QFocusEvent *e) override
- virtual void focusOutEvent(QFocusEvent *e) override
- virtual void inputMethodEvent(QInputMethodEvent *e) override
- virtual void keyPressEvent(QKeyEvent *event) override
- virtual void mouseDoubleClickEvent(QMouseEvent *e) override
- virtual void mouseMoveEvent(QMouseEvent *e) override
- virtual void mousePressEvent(QMouseEvent *e) override
- virtual void mouseReleaseEvent(QMouseEvent *e) override
- virtual void paintEvent(QPaintEvent *) override

## 9.Detailed Description

QLineEdit允许用户使用有用的编辑功能集合输入和编辑一行纯文本，包括撤消和重做(undo and redo)，剪切和粘贴以及拖放（请参阅setDragEnabled（））。

通过更改QLineEdit的echoMode（），它也可以用作“只写”字段，用于输入密码，例如。
文本的长度可以限制为maxLength（）。可以使用Validator（）或inputMask（）或两者任意约束文本。在同一行编辑器中的验证器和输入掩码之间切换时，最好清除验证器或输入掩码，以防止发生未定义的行为。

一个相关的类是QTextEdit，它允许多行富文本编辑。

您可以使用setText（）或insert（）更改文本。使用text（）检索文本；使用displayText（）检索显示的文本（可能有所不同，请参见EchoMode）。可以使用setSelection（）或selectAll（）来选择文本，并且可以对cut（），copy（）ied和paste（）d进行选择。文本可以与setAlignment（）对齐。

当文本更改时，将发出textChanged（）信号；**当通过调用setText（）而不是更改文本时，将发出textEdited（）信号**；当光标移动时，会发出cursorPositionChanged（）信号；当按下Return或Enter键时，将返回returnPressed（）信号。

编辑完成后，由于行编辑失去焦点或按下了Return / Enter键，都会发出editFinished（）信号。

请注意，**如果在行编辑中设置了验证器，则仅当验证器返回QValidator :: Acceptable时，才会发出returnPressed（）/ editingFinished（）信号**。

默认情况下，QLineEdits具有由平台样式指南指定的框架。您可以通过调用setFrame（false）将其关闭。

默认键绑定如下所述。行编辑还提供了一个上下文菜单（通常通过右键单击来调用），其中显示了一些编辑选项。

| Keypress          | Action                                                   |
| ----------------- | -------------------------------------------------------- |
| Left Arrow        | 将光标向左移动一个字符。                                 |
| Shift+Left Arrow  | 将光标向左移动一个字符并选择该文本，一直移动则选中多个。 |
| Right Arrow       | 将光标向右移动一个字符。                                 |
| Shift+Right Arrow | 将光标向右移动一个字符并选择该文本，一直移动则选中多个。 |
| Home              | 将光标移动到行的开头。                                   |
| End               | 将光标移动到行的末尾。                                   |
| Backspace         | 删除光标左侧的字符。                                     |
| Ctrl+Backspace    | 删除光标左侧的单词。                                     |
| Delete            | 删除光标右边的字符。                                     |
| Ctrl+Delete       | 删除光标右侧的单词。                                     |
| Ctrl+A            | 全选                                                     |
| Ctrl+C            | 将所选文本复制到剪贴板。                                 |
| Ctrl+Insert       | 将所选文本复制到剪贴板。                                 |
| Ctrl+K            | 删除到行尾。？？？？                                     |
| Ctrl+V            | 将剪贴板文本粘贴到单行文本编辑框中。                     |
| Shift+Insert      | 将剪贴板文本粘贴到单行文本编辑框中。                     |
| Ctrl+X            | 删除所选文本并将其复制到剪贴板。                         |
| Shift+Delete      | 删除所选文本并将其复制到剪贴板。                         |
| Ctrl+Z            | 撤销上次操作                                             |
| Ctrl+Y            | 重复上次操作                                             |

代表有效字符的任何其他键序列都将导致该字符被插入到LineEdit中。