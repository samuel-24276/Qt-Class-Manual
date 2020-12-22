# QTextEdit

继承关系：`QTextEdit`-> `QAbstractScrollArea`->`QFrame` ->`QWidget`

`document : QTextDocument*`此属性保存文本编辑器的基础文档。
注意：除非它是文档的父对象，否则编辑器不会拥有该文档的所有权。 提供的文档的父对象仍然是该对象的所有者。 如果先前分配的文档是编辑器的子级，则将其删除。

# 1.Public Types

- `ExtraSelection`

  QTextEdit::ExtraSelection结构体提供了一种为文档中给定选择指定字符格式的方法

  - `QTextCursor	cursor`

    在QTextDocument中包含选定内容的游标。

  - `QTextCharFormat	format`

    一种格式，用来指定选区的前景色或背景画笔/颜色。

- `flags AutoFormatting`

  `enum AutoFormattingFlag { AutoNone, AutoBulletList, AutoAll }`

  | Constant                  | Value      | Description                                                  |
  | ------------------------- | ---------- | ------------------------------------------------------------ |
  | QTextEdit::AutoNone       | 0          | 不要做任何自动格式化。                                       |
  | QTextEdit::AutoBulletList | 0x00000001 | 自动创建项目符号列表(例如，当用户在最左边的列中输入星号('*')，或者在现有的列表项中按回车键时)。 |
  | QTextEdit::AutoAll        | 0xffffffff | 应用所有自动格式。目前只支持自动项目符号列表。               |

- `enum LineWrapMode { NoWrap, WidgetWidth, FixedPixelWidth, FixedColumnWidth }`

  | Constant                    | Value |
  | --------------------------- | ----- |
  | QTextEdit::NoWrap           | 0     |
  | QTextEdit::WidgetWidth      | 1     |
  | QTextEdit::FixedPixelWidth  | 2     |
  | QTextEdit::FixedColumnWidth | 3     |

# 2.Properties

- `acceptRichText : bool`

  此属性用于表示文本编辑是否接受用户的富文本插入。

  当这个属性被设置为假文本时，编辑将只接受来自用户的纯文本输入。例如通过剪贴板或拖放。

  此属性的默认值为true。

- `autoFormatting : AutoFormatting`

  此属性保存已启用的自动格式化功能集。

  **该值可以是AutoFormattingFlag枚举中的值的任意组合**。默认是AutoNone。选择“自动全部”以启用所有自动格式。

  目前，唯一提供的自动格式化功能是AutoBulletList;Qt的未来版本可能会提供更多功能。

- `cursorWidth : int`

  此属性以像素为单位指定光标的宽度。默认值是1。

- `document : QTextDocument*`

- `documentTitle : QString`

  此属性保存从文本中解析的文档的标题。

  默认情况下，对于新创建的空文档，此属性包含一个空字符串。

- `html : QString`

  此属性为文本编辑的文本提供HTML接口。

  toHtml()返回文本编辑的文本作为html。

  setHtml()改变编辑框的文本。*以前的所有文本将被删除，撤消/重做历史记录将被清除*。输入文本被解释为html格式的富文本。

  注意:当创建一个包含HTML的QString并传递给setHtml()时，调用者负责确保文本被正确解码。

  默认情况下，对于新创建的空文档，此属性包含描述没有主体文本的HTML 4.0文档的文本。

- `lineWrapColumnOrWidth : int`

  这个属性**保存文本将要被换行的位置**(根据换行模式以像素或列的形式)。

  如果wrap模式是FixedPixelWidth，则该值是从文本编辑的左边缘开始的像素数，文本应该在那里进行换行。如果wrap模式是FixedColumnWidth，则该值是从文本编辑的左边缘开始的列号(字符列)，文本应该在那里进行换行。

  默认情况下，这个属性包含0的值。

- `lineWrapMode : LineWrapMode`

  此属性保存行换行模式。

  默认模式是WidgetWidth，这导致单词被包装在文本编辑的右边缘。换行发生在空格处，保持整个单词不受影响。如果希望在单词中发生换行，请使用setWordWrapMode()。如果你设置了FixedPixelWidth或FixedColumnWidth的wrap模式，你也应该调用setLineWrapColumnOrWidth()与你想要的宽度。

- `markdown : QString`

- `overwriteMode : bool`

  此属性用于确定用户输入的文本是否覆盖现有文本。

  与许多文本编辑器一样，文本编辑器小部件可以配置为用用户输入的新文本插入或覆盖现有文本。

  如果此属性为真，则现有文本将被新文本覆盖，逐字符覆盖;否则，将在光标位置插入文本，替换现有文本。

  默认情况下，该属性为false(新文本不覆盖现有文本)。

- `placeholderText : QString`

- `plainText : QString`

  此属性获取并设置文本编辑器的内容为纯文本。设置此属性时，以前的内容将被删除，撤消/重做历史记录将被重置。

  如果文本编辑具有另一种内容类型，如果调用toPlainText()，它将不会被纯文本替换。唯一的例外是非break空间，它将被转换成标准空间。

  默认情况下，对于没有内容的编辑器，此属性包含空字符串。

- `readOnly : bool`

  此属性用于保存文本编辑是否为只读。

  在只读文本编辑中，用户只能浏览文本并选择文本;修改文本是不可能的。

  此属性的默认值为false。

- `tabChangesFocus : bool`

  此属性用于保存制表符是否更改焦点或是否被接受为输入。

  在某些情况下，文本编辑不应该允许用户输入制表器或使用Tab键更改缩进，因为这会破坏焦点链。默认值为false。

- `tabStopDistance : qreal`

  此属性保存制表位宽度(以像素为单位)。

  默认情况下，这个属性包含一个80像素的值。

- `textInteractionFlags : Qt::TextInteractionFlags`

  指定小部件应该如何与用户输入交互。

  默认值取决于QTextEdit是只读的还是可编辑的，以及它是否是QTextBrowser。

- `undoRedoEnabled : bool`

  此属性用于表示是否启用撤消和重做。

  只有当此属性为true，且存在可撤消(或重做)的操作时，用户才能撤消或重做操作。

- `wordWrapMode : QTextOption::WrapMode`

  此属性保存按单词包装文本时使用的QTextEdit模式。

  默认情况下，该属性被设置为`QTextOption::WrapAtWordBoundaryOrAnywhere。`

# 3.Public Functions

- `QTextEdit(const QString &text, QWidget *parent = nullptr)`

- `QTextEdit(QWidget *parent = nullptr)`

- `virtual ~QTextEdit()`

- `bool acceptRichText() const`

- `QTextEdit::AutoFormatting autoFormatting() const`

- `QString documentTitle() const`

- `bool overwriteMode() const`

- `Qt::TextInteractionFlags textInteractionFlags() const`

- `QString toHtml() const`

- `QString toMarkdown(QTextDocument::MarkdownFeatures features = QTextDocument::MarkdownDialectGitHub) const`

- `QString toPlainText() const`

- `QTextOption::WrapMode wordWrapMode() const`

- `Qt::Alignment alignment() const`

  返回当前段落的对齐方式。

- `QString anchorAt(const QPoint &pos) const`

  返回锚点位置pos处的引用，如果在该点不存在锚点，则返回空字符串。

- `bool canPaste() const`

  返回文本是否可以从剪贴板粘贴到textedit。

- `QMenu *createStandardContextMenu()`

  此函数创建标准上下文菜单，当用户用鼠标右键单击文本编辑时显示该菜单。它从默认的contextMenuEvent()处理程序调用。弹出菜单的所有权转移给调用者。

  我们建议您使用createStandardContextMenu(QPoint)版本，它将启用对用户点击的位置敏感的操作。

- **`QMenu *createStandardContextMenu(const QPoint &position)`**

  此函数创建标准上下文菜单，当用户用鼠标右键单击文本编辑时显示该菜单。它从默认的contextMenuEvent()处理程序调用，并接受鼠标单击的位置。这可以启用对用户单击的位置敏感的操作。弹出菜单的所有权转移给调用者。

- `QTextCharFormat currentCharFormat() const`

  返回插入新文本时使用的char格式。

- `QFont currentFont() const`

  返回当前格式的字体。

- `QTextCursor cursorForPosition(const QPoint &pos) const`

  返回一个QTextCursor在位置pos(视口坐标)。

- `QRect cursorRect(const QTextCursor &cursor) const`

  返回一个包含光标的矩形(在视区坐标中)。

- `QRect cursorRect() const`

  返回一个包含文本编辑光标的矩形(以视区坐标表示)。

- `int cursorWidth() const`

- `QTextDocument *document() const`

- `void ensureCursorVisible()`

- `QList<QTextEdit::ExtraSelection> extraSelections() const`

- `bool find(const QString &exp, QTextDocument::FindFlags options = QTextDocument::FindFlags())`

- `bool find(const QRegExp &exp, QTextDocument::FindFlags options = QTextDocument::FindFlags())`

- `bool find(const QRegularExpression &exp, QTextDocument::FindFlags options = QTextDocument::FindFlags())`

- `QString fontFamily() const`

- `bool fontItalic() const`

- `qreal fontPointSize() const`

- `bool fontUnderline() const`

- `int fontWeight() const`

- `bool isReadOnly() const`

- `bool isUndoRedoEnabled() const`

- `int lineWrapColumnOrWidth() const`

- `QTextEdit::LineWrapMode lineWrapMode() const`

- `virtual QVariant loadResource(int type, const QUrl &name)`

- `void mergeCurrentCharFormat(const QTextCharFormat &modifier)`

- `void moveCursor(QTextCursor::MoveOperation operation, QTextCursor::MoveMode mode = QTextCursor::MoveAnchor)`

- `QString placeholderText() const`

- `void print(QPagedPaintDevice *printer) const`

- `void setAcceptRichText(bool accept)`

- `void setAutoFormatting(QTextEdit::AutoFormatting features)`

- `void setCurrentCharFormat(const QTextCharFormat &format)`

- `void setCursorWidth(int width)`

- `void setDocument(QTextDocument *document)`

- `void setDocumentTitle(const QString &title)`

- `void setExtraSelections(const QList<QTextEdit::ExtraSelection> &selections)`

- `void setLineWrapColumnOrWidth(int w)`

- `void setLineWrapMode(QTextEdit::LineWrapMode mode)`

- `void setOverwriteMode(bool overwrite)`

- `void setPlaceholderText(const QString &placeholderText)`

- `void setReadOnly(bool ro)`

- `void setTabChangesFocus(bool b)`

- `void setTabStopDistance(qreal distance)`

- `void setTextCursor(const QTextCursor &cursor)`

- `void setTextInteractionFlags(Qt::TextInteractionFlags flags)`

- `void setUndoRedoEnabled(bool enable)`

- `void setWordWrapMode(QTextOption::WrapMode policy)`

- `bool tabChangesFocus() const`

- `qreal tabStopDistance() const`

- `QColor textBackgroundColor() const`

- `QColor textColor() const`

- `QTextCursor textCursor() const`

# QWidget

`QTextEdit`继承并重写了`QWidget`的

```c++
virtual void closeEvent(QCloseEvent *event)
```

函数，当Qt从窗口系统收到对顶级窗口小部件的窗口关闭请求时，将使用给定事件调用此事件处理程序。
默认情况下，事件被接受并且小部件关闭。 您可以重新实现此功能，以更改小部件响应窗口关闭请求的方式。 例如，可以通过在所有事件上调用ignore（）来防止窗口关闭。
**主窗口应用程序通常使用此功能的重新实现来检查用户的工作是否已保存并在关闭前请求许可**。 例如，应用程序示例使用帮助器函数来确定是否关闭窗口：

```c++
void MainWindow::closeEvent(QCloseEvent *event)
 {
     if (maybeSave()) {
         writeSettings();
         event->accept();
     } else {
         event->ignore();
     }
 }
```

- `void QEvent::accept()`设置事件对象的接受标志，等效于调用`setAccepted（true）`。
  设置accept参数表示事件接收者想要该事件。 不需要的事件可能会传播到父窗口小部件。

- `void QEvent::ignore()`清除事件对象的接受标志参数，等效于调用setAccepted（false）。
  清除accept参数表示事件接收者不需要该事件。 不需要的事件可能会传播到父窗口小部件。