# QTextEdit

继承关系：`QTextEdit`-> `QAbstractScrollArea`->`QFrame` ->`QWidget`

`document : QTextDocument*`此属性保存文本编辑器的基础文档。
注意：除非它是文档的父对象，否则编辑器不会拥有该文档的所有权。 提供的文档的父对象仍然是该对象的所有者。 如果先前分配的文档是编辑器的子级，则将其删除。

# 1.Public Types

- `ExtraSelection`
- `flags AutoFormatting`
- `enum AutoFormattingFlag { AutoNone, AutoBulletList, AutoAll }`
- `enum LineWrapMode { NoWrap, WidgetWidth, FixedPixelWidth, FixedColumnWidth }`

# 2.Properties

- `acceptRichText : bool`
- `autoFormatting : AutoFormatting`
- `cursorWidth : int`
- `document : QTextDocument*`
- `documentTitle : QString`
- `html : QString`
- `lineWrapColumnOrWidth : int`
- `lineWrapMode : LineWrapMode`
- `markdown : QString`
- `overwriteMode : bool`
- `placeholderText : QString`
- `plainText : QString`
- `readOnly : bool`
- `tabChangesFocus : bool`
- `tabStopDistance : qreal`
- `textInteractionFlags : Qt::TextInteractionFlags`
- `undoRedoEnabled : bool`
- `wordWrapMode : QTextOption::WrapMode`

# 3.Public Functions

- `QTextEdit(const QString &text, QWidget *parent = nullptr)`
- `QTextEdit(QWidget *parent = nullptr)`
- `virtual ~QTextEdit()`
- `bool acceptRichText() const`
- `Qt::Alignment alignment() const`
- `QString anchorAt(const QPoint &pos) const`
- `QTextEdit::AutoFormatting autoFormatting() const`
- `bool canPaste() const`
- `QMenu *createStandardContextMenu()`
- `QMenu *createStandardContextMenu(const QPoint &position)`
- `QTextCharFormat currentCharFormat() const`
- `QFont currentFont() const`
- `QTextCursor cursorForPosition(const QPoint &pos) const`
- `QRect cursorRect(const QTextCursor &cursor) const`
- `QRect cursorRect() const`
- `int cursorWidth() const`
- `QTextDocument *document() const`
- `QString documentTitle() const`
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
- `bool overwriteMode() const`
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
- `Qt::TextInteractionFlags textInteractionFlags() const`
- `QString toHtml() const`
- `QString toMarkdown(QTextDocument::MarkdownFeatures features = QTextDocument::MarkdownDialectGitHub) const`
- `QString toPlainText() const`
- `QTextOption::WrapMode wordWrapMode() const`

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