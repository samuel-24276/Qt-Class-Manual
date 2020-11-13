# QPlainTextEdit

继承关系：`QPlainTextEdit`->`QAbstractScrollArea`->`QFrame`->`QWidget`->` QObject and QPaintDevice`

## 1.Public Types

- enum	LineWrapMode { NoWrap, WidgetWidth }

## 2.Properties

- backgroundVisible : bool

  此属性保存调色板背景在文档区域之外是否可见。

  如果设置为true，则纯文本编辑会在文本文档未涵盖的视口区域上绘制调色板背景。如果设置为false，则不会。 该功能使用户可以在视觉上区分用调色板的基础颜色绘制的文档区域和未被任何文档覆盖的空白区域。

  默认为false。

- blockCount : const int

  此属性保存文档中文本块的数量。

  默认情况下，在空文档中，此属性的值为1。

- centerOnScroll : bool

  此属性保存光标是否应该在屏幕上居中。

  如果设置为true，纯文本编辑将垂直滚动文档以使光标在视口的中心可见。 这也允许文本编辑滚动到文档末尾下方。 否则，如果将其设置为false，则纯文本编辑将滚动尽可能最小的量以确保光标可见。 将相同的算法应用于通过appendPlainText（）附加的任何新行。

  默认为false。

- cursorWidth : int

  此属性指定光标的宽度（以像素为单位）。 预设值为1。

- documentTitle : QString

  此属性保存从文本解析的文档的标题。

  默认情况下，此属性包含一个空字符串。

- lineWrapMode : LineWrapMode

  此属性保留换行模式。

  默认模式是WidgetWidth，它使单词被包裹在文本编辑的右边缘。 包装发生在空白处，使整个单词保持完整。 如果要在单词内进行换行，请使用setWordWrapMode（）。

- maximumBlockCount : int

  此属性保留文档中块的限制。

  指定文档可能具有的最大块数。 如果文档中还有更多用此属性指定的块，则从文档开头删除这些块。

  负值或零值表示文档可以包含无限数量的块。

  默认值为0。

  请注意，设置此属性会将限制立即应用于文档内容。 **设置此属性还会禁用撤消重做历史记录**。

- overwriteMode : bool

  此属性保存用户输入的文本是否将覆盖现有文本。

  与许多文本编辑器一样，纯文本编辑器窗口小部件可以配置为使用用户输入的新文本来插入或覆盖现有文本。

  如果此属性为true，则现有文本将被新文本按字符替换； 否则，在光标位置插入文本，替换现有文本。

  默认情况下，此属性为false（新文本不会覆盖现有文本）。

- plainText : QString

  此属性获取并设置纯文本编辑器的内容。 设置此属性后，将删除先前的内容并重置撤消/重做历史记录。

  默认情况下，对于没有内容的编辑器，此属性包含一个空字符串。

- readOnly : bool

  **此属性保存文本编辑是否为只读**。

  在只读文本编辑中，用户只能浏览文本并选择文本。 修改文本是不可能的。

  此属性的默认值为false。

- tabChangesFocus : bool

  此属性保存Tab是否更改焦点还是被接受为输入。

  在某些情况下，文本编辑不应允许用户使用Tab键输入制表符或更改缩进，因为这会破坏焦点链。 默认为false。

- tabStopWidth : int

  此属性保存制表位的宽度（以像素为单位）。

  默认情况下，此属性的值为80。

- textInteractionFlags : Qt::TextInteractionFlags

  指定标签显示文本时应如何与用户输入交互。

  如果标志包含Qt :: LinksAccessibleByKeyboard或Qt :: TextSelectableByKeyboard，则焦点策略也将自动设置为Qt :: ClickFocus。

  默认值取决于QPlainTextEdit是只读的还是可编辑的。

- undoRedoEnabled : bool

  此属性保存是否启用撤消和重做。

  如果此属性为true，并且存在可以撤消（或重做）的操作，则用户只能撤消或重做操作。

  默认情况下，此属性为true。

- wordWrapMode : QTextOption::WrapMode

  此属性保留QPlainTextEdit在按文字换行时将使用的模式。

  默认情况下，此属性设置为QTextOption :: WrapAtWordBoundaryOrAnywhere。

## 3.Public Functions

- QPlainTextEdit ( QWidget * parent = 0 )
- QPlainTextEdit ( const QString & text, QWidget * parent = 0 )
- virtual	~QPlainTextEdit ()
- QString	anchorAt ( const QPoint & pos ) const
- bool	backgroundVisible () const
- int	blockCount () const
- bool	canPaste () const
- bool	centerOnScroll () const
- QMenu *	createStandardContextMenu ()
- QTextCharFormat	currentCharFormat () const
- QTextCursor	cursorForPosition ( const QPoint & pos ) const
- QRect	cursorRect ( const QTextCursor & cursor ) const
- QRect	cursorRect () const
- int	cursorWidth () const
- QTextDocument *	document () const
- QString	documentTitle () const
- void	ensureCursorVisible ()
- QList\<QTextEdit::ExtraSelection>	extraSelections () const
- bool	find ( const QString & exp, QTextDocument::FindFlags options = 0 )
- bool	isReadOnly () const
- bool	isUndoRedoEnabled () const
- LineWrapMode	lineWrapMode () const
- virtual QVariant	loadResource ( int type, const QUrl & name )
- int	maximumBlockCount () const
- void	mergeCurrentCharFormat ( const QTextCharFormat & modifier )
- void	moveCursor ( QTextCursor::MoveOperation operation, 
- QTextCursor::MoveMode mode = QTextCursor::MoveAnchor )
- bool	overwriteMode () const
- void	print ( QPrinter * printer ) const
- void	setBackgroundVisible ( bool visible )
- void	setCenterOnScroll ( bool enabled )
- void	setCurrentCharFormat ( const QTextCharFormat & format )
- void	setCursorWidth ( int width )
- void	setDocument ( QTextDocument * document )
- void	setDocumentTitle ( const QString & title )
- void	setExtraSelections ( const QList\<QTextEdit::ExtraSelection> & selections )
- void	setLineWrapMode ( LineWrapMode mode )
- void	setMaximumBlockCount ( int maximum )
- void	setOverwriteMode ( bool overwrite )
- void	setReadOnly ( bool ro )
- void	setTabChangesFocus ( bool b )
- void	setTabStopWidth ( int width )
- void	setTextCursor ( const QTextCursor & cursor )
- void	setTextInteractionFlags ( Qt::TextInteractionFlags flags )
- void	setUndoRedoEnabled ( bool enable )
- void	setWordWrapMode ( QTextOption::WrapMode policy )
- bool	tabChangesFocus () const
- int	tabStopWidth () const
- QTextCursor	textCursor () const
- Qt::TextInteractionFlags	textInteractionFlags () const
- QString	toPlainText () const
- QTextOption::WrapMode	wordWrapMode () const