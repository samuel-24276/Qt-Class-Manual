# QUndoStack

继承关系：`QUndoStack`->`QObject`

## 1.Properties

- active : bool

  此属性保存此堆栈的活动状态。

  **一个应用程序通常具有多个撤消堆栈，每个打开的文档一个**。 活动堆栈是与当前活动文档关联的堆栈。 如果堆栈属于QUndoGroup，则调用QUndoGroup :: undo（）或QUndoGroup :: redo（）时，该堆栈将处于活动状态。 如果QUndoView监视了QUndoGroup，则该视图在活动时将显示该堆栈的内容。 如果堆栈不属于QUndoGroup，则使其处于活动状态无效。

  **通常，当关联的文档窗口获得焦点时，程序员需要通过调用setActive（）来指定哪个堆栈处于活动状态**。

- undoLimit : int

  此属性保存此堆栈上的最大命令数。

  当堆栈上的命令数量超过堆栈的undoLimit时，将从堆栈底部删除命令。 宏命令（带有子命令的命令）被视为一个命令。 默认值为0，表示没有限制。

  仅当撤消堆栈为空时才可以设置此属性，因为在非空堆栈上进行设置可能会删除当前索引处的命令。 在非空堆栈上调用setUndoLimit（）会显示警告，但不执行任何操作。

## 2.Public Functions

- QUndoStack ( QObject * parent = 0 )

- ~QUndoStack ()

- void	beginMacro ( const QString & text )

  从给定的文本描述开始组成宏命令。

  由指定文本描述的空命令被压入堆栈。 压入堆栈的所有后续命令都将附加到空命令的子级，直到调用endMacro（）为止。

  可以嵌套对beginMacro（）和endMacro（）的调用，但是对beginMacro（）的每次调用都必须具有对endMacro（）的匹配调用。

  组成宏时，将禁用堆栈。 这意味着：

  - 不发出indexChanged（）和cleanChanged（），
  - canUndo（）和canRedo（）返回false，
  - 调用undo（）或redo（）无效，
  - 撤消/重做操作被禁用。

  当为最外面的宏调用endMacro（）时，将启用堆栈并发出适当的信号。

  ```C++
   stack.beginMacro("insert red text");
   stack.push(new InsertText(document, idx, text));
   stack.push(new SetColor(document, idx, text.length(), Qt::red));
   stack.endMacro(); // indexChanged() is emitted
  ```

  This code is equivalent to:

  ```C++
   QUndoCommand *insertRed = new QUndoCommand(); // an empty command
   insertRed->setText("insert red text");
  
   new InsertText(document, idx, text, insertRed); // becomes child of insertRed
   new SetColor(document, idx, text.length(), Qt::red, insertRed);
  
   stack.push(insertRed);
  ```

- void	endMacro ()

  结束宏命令的合成。

  如果这是一组嵌套宏中最外面的宏，则此函数对整个宏命令发出一次indexChanged（）。

- bool	canRedo () const

  如果有可用于重做的命令，则返回true； 否则返回false。

  如果堆栈为空或堆栈中的top命令已经重做，则此函数返回false。

  与index（）== count（）同义。

- bool	canUndo () const

  如果有可用于撤消的命令，则返回true；否则返回false。

  如果堆栈为空，或者堆栈上的底部命令已经撤消，则此函数返回false。

  与index（）== 0的同义词。

- int	cleanIndex () const

- void	clear ()

- const QUndoCommand *	command ( int index ) const

- int	count () const

- QAction *	createRedoAction ( QObject * parent, const QString & prefix = QString() ) const

  使用给定的父级创建一个重做QAction对象。

  触发此操作将导致对redo（）的调用。 该操作的文本是命令的文本，该命令的文本将在下一次对redo（）的调用中重做，并以指定的前缀为前缀。 如果没有可用于重做的命令，此操作将被禁用。

  如果前缀为空，则使用默认模板“Redo％1”代替前缀。 在Qt 4.8之前，默认使用前缀“ Redo”。

- QAction *	createUndoAction ( QObject * parent, const QString & prefix = QString() ) const

  使用给定的父级创建一个撤消QAction对象。

  触发此操作将导致对undo（）的调用。 该操作的文本是命令的文本，该命令的文本将在下一次调用undo（）时撤消，并以指定的prefix为前缀。 如果没有可用的撤消命令，此操作将被禁用。

  如果前缀为空，则使用默认模板“Undo％1”代替前缀。 在Qt 4.8之前，默认使用前缀“Undo”。

- int	index () const

  返回当前命令的索引。 这是将在下次调用redo（）时执行的命令。 由于许多命令可能已被撤消，因此它并不总是堆栈上最顶层的命令。

- bool	isActive () const

- bool	isClean () const

- void	push ( QUndoCommand * cmd )

  将cmd推入堆栈或将其与最近执行的命令合并。 无论哪种情况，都可以通过调用其redo（）函数来执行cmd。

  如果cmd的ID不为-1，并且该ID与最近执行的命令的ID相同，则QUndoStack将通过对最近执行的命令调用QUndoCommand :: mergeWith（）来尝试合并两个命令。 如果QUndoCommand :: mergeWith（）返回true，则删除cmd。

  在所有其他情况下，只需将cmd推入堆栈即可。

  如果在推入cmd之前撤消了命令，则将删除当前命令及其上方的所有命令。 因此，cmd总是最终成为堆栈中的最顶层。

  push命令后，堆栈将获得它的所有权。 没有获取程序可以返回命令，因为在执行完命令后对其进行修改几乎总是会导致文档状态的破坏。

- QString	redoText () const

  返回命令的文本，该文本将在下次调用redo（）时重做。

- void	setUndoLimit ( int limit )

- QString	text ( int idx ) const

  返回索引为idx的命令的文本。

- int	undoLimit () const

- QString	undoText () const

## 3.Public Slots

- void	redo ()

  通过调用QUndoCommand :: redo（）重做当前命令。 **增加当前命令索引**。

  如果堆栈为空，或者已重做堆栈上的top命令，则此功能不执行任何操作。

- void	setActive ( bool active = true )

- void	setClean ()

  将堆栈标记为clean，如果堆栈尚未clean，则发出cleanChanged（）。

  每当堆栈通过使用撤消/重做命令返回到此状态时，它都会发出信号cleanChanged（）。 当堆栈离开clean状态时，也会发出此信号。

- void	setIndex ( int idx )

  重复调用undo（）或redo（），直到当前命令索引达到idx。 此功能可用于使文档的状态向前或向后滚动。 **indexChanged（）仅发出一次**。

- void	undo ()

  通过调用QUndoCommand :: undo（）撤消当前命令下方的命令。 减少当前命令索引。

  如果堆栈为空，或者堆栈上的底部命令已被撤消，则此功能不执行任何操作。

## 4.Signals

- void	canRedoChanged ( bool canRedo )

- void	canUndoChanged ( bool canUndo )

- void	cleanChanged ( bool clean )

- void	indexChanged ( int idx )

- void	redoTextChanged ( const QString & redoText )

  每当redoText（）的值更改时，都会发出此信号。 它用于更新createRedoAction（）返回的重做操作的text属性。 redoText指定新文本。

- void	undoTextChanged ( const QString & undoText )

  返回命令的文本，该文本将在下次调用undo（）时撤消。

## 5.Detailed Description

QUndoStack类是QUndoCommand对象的堆栈。

有关Qt撤消框架的概述，请参见概述文档。

撤消堆栈维护已应用于文档的命令堆栈。

使用push（）将新命令压入堆栈。 可以使用undo（）和redo（）或触发createUndoAction（）和createRedoAction（）返回的操作来撤消和重做命令。

QUndoStack跟踪当前命令。 这是下一次对redo（）的调用将执行的命令。 该命令的索引由index（）返回。 可以使用setIndex（）向前或向后滚动已编辑对象的状态。 如果已经重做了堆栈上最顶层的命令，则index（）等于count（）。

QUndoStack支持撤消和重做操作，命令压缩(command compression)，命令宏(command macros)，并支持清除状态(clean state)的概念。

### Undo and Redo Actions

QUndoStack提供方便的撤消和重做QAction对象，可以将其插入菜单或工具栏。 撤消或重做命令时，QUndoStack将更新这些操作的文本属性以反映它们将触发的更改。 当没有命令可用于撤消或重做时，这些操作也将被禁用。 这些动作由QUndoStack :: createUndoAction（）和QUndoStack :: createRedoAction（）返回。

### Command Compression and Macros

当几个命令可以压缩为一个命令，并且可以在一个操作中撤消和重做时，命令压缩很有用。例如，当用户在文本编辑器中键入字符时，将创建一个新命令。该命令将字符插入到光标位置的文档中。但是，对于用户来说，撤消或重做整个单词，句子或段落的键入更为方便。命令压缩允许将这些单字符命令合并为单个命令，该命令可以插入或删除文本部分。有关更多信息，请参见QUndoCommand :: mergeWith（）和push（）。

命令宏是一系列命令，所有命令都可以一次撤消并重做。通过为命令提供子命令列表来创建命令宏。撤消或重做父命令将导致子命令被撤消或重做。可以通过在QUndoCommand构造函数中指定一个父级，或使用便利函数beginMacro（）和endMacro（）显式创建命令宏。

尽管命令压缩和宏对用户似乎具有相同的效果，但它们在应用程序中的用途常常不同。如果不需要单独记录命令，并且只有较大的更改与用户相关，则可以对执行较小更改的命令进行有用的压缩。但是，对于需要单独记录的命令或无法压缩的命令，使用宏在维护每个命令记录的同时提供更方便的用户体验很有用。

### Clean State

QUndoStack支持干净状态的概念。 将文档保存到磁盘后，可以使用setClean（）将堆栈标记为干净。 每当堆栈通过撤消和重做命令返回到此状态时，它都会发出信号cleanChanged（）。 当堆栈离开清洁状态时，也会发出此信号。 该信号**通常用于启用和禁用应用程序中的保存操作，以及更新文档标题以反映其包含未保存的更改**。