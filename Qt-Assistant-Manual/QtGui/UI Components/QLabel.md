# QLabel

继承关系：`QLabel`->`QFrame`->`QWidget`->`QObject and QPaintDevice`

## 1.Properties

- alignment : Qt::Alignment

- hasSelectedText : const bool

- indent : int

  此属性保存标签的文本缩进（以像素为单位）。

  如果标签显示文本，则如果alignment（）为Qt :: AlignLeft，则缩进将应用于左侧；如果alignment（）为Qt :: AlignRight，则缩进至右侧；如果alignment（）为Qt :: AlignTop，则缩进至顶部 ，如果alignment（）为Qt :: AlignBottom，则到达底部边缘。

  如果缩进为负，或者未设置缩进，则标签将按以下方式计算有效缩进：如果frameWidth（）为0，则有效缩进为0。如果frameWidth（）大于0，则有效缩进为一半。 小部件当前font（）的“ x”字符的宽度。

  默认情况下，缩进为-1，表示有效缩进是以上述方式计算的。

- margin : int

  此属性保存边距的宽度。

  裕度是帧的最内像素和内容的最外像素之间的距离。

  默认边距为0。

- openExternalLinks : bool

- pixmap : QPixmap

- scaledContents : bool

- selectedText : const QString

- text : QString

- textFormat : Qt::TextFormat

- textInteractionFlags : Qt::TextInteractionFlags

- **wordWrap : bool**

  此属性保存标签的自动换行策略。

  如果此属性为true，则在断字时在必要时将标签文本包装起来； 否则，它根本不会被包裹。

  默认情况下，自动换行被禁用。

## 2.Public Functions

- QLabel ( QWidget * parent = 0, Qt::WindowFlags f = 0 )

- QLabel ( const QString & text, QWidget * parent = 0, Qt::WindowFlags f = 0 )

- ~QLabel ()

- **void	setWordWrap ( bool on )**

  参数on设置为true则自动换行。

- Qt::Alignment	alignment () const

- QWidget *	buddy () const

- bool	hasScaledContents () const

- bool	hasSelectedText () const

- int	indent () const

- int	margin () const

- QMovie *	movie () const

- bool	openExternalLinks () const

- const QPicture *	picture () const

- const QPixmap *	pixmap () const

- QString	selectedText () const

- int	selectionStart () const

- void	setAlignment ( Qt::Alignment )

  此属性保留标签内容的对齐方式。

  默认情况下，标签的内容是**左对齐和垂直居中**的。

- void	setBuddy ( QWidget * buddy )

- void	setIndent ( int )

  设置文本缩进。

- void	setMargin ( int )

- void	setOpenExternalLinks ( bool open )

- void	setScaledContents ( bool )

- void	setSelection ( int start, int length )

- void	setTextFormat ( Qt::TextFormat )

- void	setTextInteractionFlags ( Qt::TextInteractionFlags flags )

- QString	text () const

- Qt::TextFormat	textFormat () const

- Qt::TextInteractionFlags	textInteractionFlags () const

- bool	wordWrap () const

## 3.Reimplemented Public Functions

- virtual int	heightForWidth ( int w ) const
- virtual QSize	minimumSizeHint () const
- virtual QSize	sizeHint () const

## 4.Public Slots

- void	linkActivated ( const QString & link )
- void	linkHovered ( const QString & link )

## 5.Reimplemented Protected Functions

- virtual void	changeEvent ( QEvent * ev )
- virtual void	contextMenuEvent ( QContextMenuEvent * ev )
- virtual bool	event ( QEvent * e )
- virtual void	focusInEvent ( QFocusEvent * ev )
- virtual bool	focusNextPrevChild ( bool next )
- virtual void	focusOutEvent ( QFocusEvent * ev )
- virtual void	keyPressEvent ( QKeyEvent * ev )
- virtual void	mouseMoveEvent ( QMouseEvent * ev )
- virtual void	mousePressEvent ( QMouseEvent * ev )
- virtual void	mouseReleaseEvent ( QMouseEvent * ev )
- virtual void	paintEvent ( QPaintEvent * )

## 6.Detailed Description

