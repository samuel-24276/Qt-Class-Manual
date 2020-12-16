# QWidget

继承关系：`QWidget`->`QObject` and `QPaintDevice`

继承者：

- Phonon::EffectWidget, 
- Phonon::SeekSlider, 
- Phonon::VideoPlayer, 
- Phonon::VideoWidget, 
- Phonon::VolumeSlider, 
- Q3ComboBox, 
- Q3DataBrowser,
- Q3DataView, 
- Q3DateTimeEdit, 
- Q3DateTimeEditBase, 
- Q3DockArea, 
- Q3Header, 
- Q3MainWindow, 
- QAbstractButton, 
- QAbstractSlider, 
- QAbstractSpinBox, 
- QAxWidget, 
- QCalendarWidget, 
- QComboBox, 
- QDesignerActionEditorInterface, 
- QDesignerFormWindowInterface, 
- QDesignerObjectInspectorInterface, 
- QDesignerPropertyEditorInterface, 
- QDesignerWidgetBoxInterface, 
- QDesktopWidget, 
- QDialog, 
- QDialogButtonBox, 
- QDockWidget, 
- QFocusFrame, 
- QFrame, 
- QGLWidget, 
- QGroupBox, 
- QHelpSearchQueryWidget, 
- QHelpSearchResultWidget, 
- QLineEdit, 
- QMacCocoaViewContainer, 
- QMacNativeWidget, 
- QMainWindow, 
- QMdiSubWindow, 
- QMenu, 
- QMenuBar, 
- QPrintPreviewWidget, 
- QProgressBar, 
- QRubberBand, 
- QSizeGrip, 
- QSplashScreen, 
- QSplitterHandle, 
- QStatusBar, 
- QSvgWidget, 
- QTabBar, 
- QTabWidget, 
- QToolBar, 
- QWebInspector, 
- QWebView, 
- QWizardPage, 
- QWorkspace, 
- QWSEmbedWidget
- QX11EmbedContainer
- QX11EmbedWidget

## 1.Public Types

- enum	RenderFlag { DrawWindowBackground, DrawChildren, IgnoreMask }

  该枚举描述了调用QWidget :: render（）时如何渲染(呈现)窗口小部件。

  | Constant                      | Value | Description                                                  |
  | ----------------------------- | ----- | ------------------------------------------------------------ |
  | QWidget::DrawWindowBackground | 0x1   | 如果启用此选项，则即使未设置autoFillBackground，小部件的背景也会渲染到目标中。 默认情况下，启用此选项 |
  | QWidget::DrawChildren         | 0x2   | 如果启用此选项，则将小部件的子级递归渲染到目标中。 默认情况下，启用此选项。 |
  | QWidget::IgnoreMask           | 0x4   | 如果启用此选项，则将小部件的QWidget :: mask（）渲染到目标中时将被忽略。 默认情况下，此选项是禁用的。 |

- flags	RenderFlags

## 2.Properties

- acceptDrops : bool

- accessibleDescription : QString

- accessibleName : QString

- autoFillBackground : bool

- baseSize : QSize

- childrenRect : const QRect

- childrenRegion : const QRegion

- contextMenuPolicy : Qt::ContextMenuPolicy

- cursor : QCursor

- enabled : bool

- focus : const bool

- focusPolicy : Qt::FocusPolicy

- font : QFont

- frameGeometry : const QRect

- frameSize : const QSize

- fullScreen : const bool

- geometry : QRect

- height : const int

- inputMethodHints : Qt::InputMethodHints

- isActiveWindow : const bool

- layoutDirection : Qt::LayoutDirection

- locale : QLocale

- maximized : const bool

- maximumHeight : int

- maximumSize : QSize

- maximumWidth : int

- minimized : const bool

- minimumHeight : int

- minimumSize : QSize

- minimumSizeHint : const QSize

- minimumWidth : int

- modal : const bool

- mouseTracking : bool

- normalGeometry : const QRect

- palette : QPalette

- pos : QPoint

- rect : const QRect

- size : QSize

- sizeHint : const QSize

- sizeIncrement : QSize

- sizePolicy : QSizePolicy

- statusTip : QString

- styleSheet : QString

- toolTip : QString

- updatesEnabled : bool

- visible : bool

- whatsThis : QString

- width : const int

- windowFilePath : QString

- windowFlags : Qt::WindowFlags

- windowIcon : QIcon

- windowIconText : QString

- **windowModality : Qt::WindowModality**

  此属性保存哪些窗口被模式窗口小部件阻止（模态）。

  此属性仅对Windows有意义。 模态窗口小部件可防止其他窗口中的窗口小部件获得输入。 该属性的值控制在小部件可见时哪些窗口被阻止。 在窗口可见时更改此属性无效； 您必须先hide()小部件，然后再次show()。

  默认情况下，此属性为Qt :: NonModal。

  | Constant               | Value | Description                                                  |
  | ---------------------- | ----- | ------------------------------------------------------------ |
  | `Qt::NonModal`         | `0`   | 该窗口不是模态窗口，不会阻止其他窗口的输入。                 |
  | `Qt::WindowModal`      | `1`   | 窗口是单个窗口层次结构的模态，并阻止输入到其父窗口，所有祖父母窗口以及其父窗口和祖父母窗口的所有同级窗口。 |
  | `Qt::ApplicationModal` | `2`   | 窗口是应用程序的模态，并阻止所有窗口的输入。                 |

- windowModified : bool

- windowOpacity : double

- windowTitle : QString

- x : const int

- y : const int

## 3.Public Functions

- QWidget ( QWidget * parent = 0, Qt::WindowFlags f = 0 )

- ~QWidget ()

- void	setWindowModality ( Qt::WindowModality windowModality )

  设置窗口的模态级别。

- bool	acceptDrops () const
  QString	accessibleDescription () const
  QString	accessibleName () const
  QList<QAction *>	actions () const
  void	activateWindow ()
  void	addAction ( QAction * action )
  void	addActions ( QList<QAction *> actions )
  void	adjustSize ()
  bool	autoFillBackground () const
  QPalette::ColorRole	backgroundRole () const
  QSize	baseSize () const
  QWidget *	childAt ( int x, int y ) const
  QWidget *	childAt ( const QPoint & p ) const
  QRect	childrenRect () const
  QRegion	childrenRegion () const
  void	clearFocus ()
  void	clearMask ()
  QMargins	contentsMargins () const
  QRect	contentsRect () const
  Qt::ContextMenuPolicy	contextMenuPolicy () const
  QCursor	cursor () const
  WId	effectiveWinId () const
  void	ensurePolished () const
  Qt::FocusPolicy	focusPolicy () const
  QWidget *	focusProxy () const
  QWidget *	focusWidget () const
  const QFont &	font () const
  QFontInfo	fontInfo () const
  QFontMetrics	fontMetrics () const
  QPalette::ColorRole	foregroundRole () const
  QRect	frameGeometry () const
  QSize	frameSize () const
  const QRect &	geometry () const
  void	getContentsMargins ( int * left, int * top, int * right, int * bottom ) const
  void	grabGesture ( Qt::GestureType gesture, Qt::GestureFlags flags = Qt::GestureFlags() )
  void	grabKeyboard ()
  void	grabMouse ()
  void	grabMouse ( const QCursor & cursor )
  int	grabShortcut ( const QKeySequence & key, Qt::ShortcutContext context = Qt::WindowShortcut )
  QGraphicsEffect *	graphicsEffect () const
  QGraphicsProxyWidget *	graphicsProxyWidget () const
  bool	hasEditFocus () const
  bool	hasFocus () const
  bool	hasMouseTracking () const
  int	height () const
  virtual int	heightForWidth ( int w ) const
  QInputContext *	inputContext ()
  Qt::InputMethodHints	inputMethodHints () const
  virtual QVariant	inputMethodQuery ( Qt::InputMethodQuery query ) const
  void	insertAction ( QAction * before, QAction * action )
  void	insertActions ( QAction * before, QList<QAction *> actions )
  bool	isActiveWindow () const
  bool	isAncestorOf ( const QWidget * child ) const
  bool	isEnabled () const
  bool	isEnabledTo ( QWidget * ancestor ) const
  bool	isFullScreen () const
  bool	isHidden () const
  bool	isMaximized () const
  bool	isMinimized () const
  bool	isModal () const
  bool	isVisible () const
  bool	isVisibleTo ( QWidget * ancestor ) const
  bool	isWindow () const
  bool	isWindowModified () const
  QLayout *	layout () const
  Qt::LayoutDirection	layoutDirection () const
  QLocale	locale () const
  Qt::HANDLE	macCGHandle () const
  Qt::HANDLE	macQDHandle () const
  QPoint	mapFrom ( QWidget * parent, const QPoint & pos ) const
  QPoint	mapFromGlobal ( const QPoint & pos ) const
  QPoint	mapFromParent ( const QPoint & pos ) const
  QPoint	mapTo ( QWidget * parent, const QPoint & pos ) const
  QPoint	mapToGlobal ( const QPoint & pos ) const
  QPoint	mapToParent ( const QPoint & pos ) const
  QRegion	mask () const
  int	maximumHeight () const
  QSize	maximumSize () const
  int	maximumWidth () const
  int	minimumHeight () const
  QSize	minimumSize () const
  virtual QSize	minimumSizeHint () const
  int	minimumWidth () const
  void	move ( const QPoint & )
  void	move ( int x, int y )
  QWidget *	nativeParentWidget () const
  QWidget *	nextInFocusChain () const
  QRect	normalGeometry () const
  void	overrideWindowFlags ( Qt::WindowFlags flags )
  const QPalette &	palette () const
  QWidget *	parentWidget () const
  QPlatformWindow *	platformWindow () const (preliminary)
  QPlatformWindowFormat	platformWindowFormat () const
  QPoint	pos () const
  QWidget *	previousInFocusChain () const
  QRect	rect () const
  void	releaseKeyboard ()
  void	releaseMouse ()
  void	releaseShortcut ( int id )
  void	removeAction ( QAction * action )
  void	render ( QPaintDevice * target, const QPoint & targetOffset = QPoint(), const QRegion & sourceRegion = QRegion(), RenderFlags renderFlags = RenderFlags( DrawWindowBackground | DrawChildren ) )
  void	render ( QPainter * painter, const QPoint & targetOffset = QPoint(), const QRegion & sourceRegion = QRegion(), RenderFlags renderFlags = RenderFlags( DrawWindowBackground | DrawChildren ) )
  void	repaint ( int x, int y, int w, int h )
  void	repaint ( const QRect & rect )
  void	repaint ( const QRegion & rgn )
  void	resize ( const QSize & )
  void	resize ( int w, int h )
  bool	restoreGeometry ( const QByteArray & geometry )
  QByteArray	saveGeometry () const
  void	scroll ( int dx, int dy )
  void	scroll ( int dx, int dy, const QRect & r )
  void	setAcceptDrops ( bool on )
  void	setAccessibleDescription ( const QString & description )
  void	setAccessibleName ( const QString & name )
  void	setAttribute ( Qt::WidgetAttribute attribute, bool on = true )
  void	setAutoFillBackground ( bool enabled )
  void	setBackgroundRole ( QPalette::ColorRole role )
  void	setBaseSize ( const QSize & )
  void	setBaseSize ( int basew, int baseh )
  void	setContentsMargins ( int left, int top, int right, int bottom )
  void	setContentsMargins ( const QMargins & margins )
  void	setContextMenuPolicy ( Qt::ContextMenuPolicy policy )
  void	setCursor ( const QCursor & )
  void	setEditFocus ( bool enable )
  void	setFixedHeight ( int h )
  void	setFixedSize ( const QSize & s )
  void	setFixedSize ( int w, int h )
  void	setFixedWidth ( int w )
  void	setFocus ( Qt::FocusReason reason )
  void	setFocusPolicy ( Qt::FocusPolicy policy )
  void	setFocusProxy ( QWidget * w )
  void	setFont ( const QFont & )
  void	setForegroundRole ( QPalette::ColorRole role )
  void	setGeometry ( const QRect & )
  void	setGeometry ( int x, int y, int w, int h )
  void	setGraphicsEffect ( QGraphicsEffect * effect )
  void	setInputContext ( QInputContext * context )
  void	setInputMethodHints ( Qt::InputMethodHints hints )
  void	setLayout ( QLayout * layout )
  void	setLayoutDirection ( Qt::LayoutDirection direction )
  void	setLocale ( const QLocale & locale )
  void	setMask ( const QBitmap & bitmap )
  void	setMask ( const QRegion & region )
  void	setMaximumHeight ( int maxh )
  void	setMaximumSize ( const QSize & )
  void	setMaximumSize ( int maxw, int maxh )
  void	setMaximumWidth ( int maxw )
  void	setMinimumHeight ( int minh )
  void	setMinimumSize ( const QSize & )
  void	setMinimumSize ( int minw, int minh )
  void	setMinimumWidth ( int minw )
  void	setMouseTracking ( bool enable )
  void	setPalette ( const QPalette & )
  void	setParent ( QWidget * parent )
  void	setParent ( QWidget * parent, Qt::WindowFlags f )
  void	setPlatformWindow ( QPlatformWindow * window ) (preliminary)
  void	setPlatformWindowFormat ( const QPlatformWindowFormat & format )
  void	setShortcutAutoRepeat ( int id, bool enable = true )
  void	setShortcutEnabled ( int id, bool enable = true )
  void	setSizeIncrement ( const QSize & )
  void	setSizeIncrement ( int w, int h )
  void	setSizePolicy ( QSizePolicy )
  void	setSizePolicy ( QSizePolicy::Policy horizontal, QSizePolicy::Policy vertical )
  void	setStatusTip ( const QString & )
  void	setStyle ( QStyle * style )
  void	setToolTip ( const QString & )
  void	setUpdatesEnabled ( bool enable )
  void	setWhatsThis ( const QString & )
  void	setWindowFilePath ( const QString & filePath )
  void	setWindowFlags ( Qt::WindowFlags type )
  void	setWindowIcon ( const QIcon & icon )
  void	setWindowIconText ( const QString & )
  void	setWindowOpacity ( qreal level )
  void	setWindowRole ( const QString & role )
  void	setWindowState ( Qt::WindowStates windowState )
  void	setWindowSurface ( QWindowSurface * surface ) (preliminary)
  void	setupUi ( QWidget * widget )
  QSize	size () const
  virtual QSize	sizeHint () const
  QSize	sizeIncrement () const
  QSizePolicy	sizePolicy () const
  void	stackUnder ( QWidget * w )
  QString	statusTip () const
  QStyle *	style () const
  QString	styleSheet () const
  bool	testAttribute ( Qt::WidgetAttribute attribute ) const
  QString	toolTip () const
  bool	underMouse () const
  void	ungrabGesture ( Qt::GestureType gesture )
  void	unsetCursor ()
  void	unsetLayoutDirection ()
  void	unsetLocale ()
  void	update ( int x, int y, int w, int h )
  void	update ( const QRect & rect )
  void	update ( const QRegion & rgn )
  void	updateGeometry ()
  bool	updatesEnabled () const
  QRegion	visibleRegion () const
  QString	whatsThis () const
  int	width () const
  WId	winId () const
  QWidget *	window () const
  QString	windowFilePath () const
  Qt::WindowFlags	windowFlags () const
  QIcon	windowIcon () const
  QString	windowIconText () const
  Qt::WindowModality	windowModality () const
  qreal	windowOpacity () const
  QString	windowRole () const
  Qt::WindowStates	windowState () const
  QWindowSurface *	windowSurface () const (preliminary)
  QString	windowTitle () const
  Qt::WindowType	windowType () const
  int	x () const
  const QX11Info &	x11Info () const
  Qt::HANDLE	x11PictureHandle () const
  int	y () const