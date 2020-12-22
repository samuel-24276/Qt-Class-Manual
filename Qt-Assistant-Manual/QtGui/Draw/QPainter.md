# QPainter

继承者： `Q3Painter` and `QStylePainter`

## 1.Public Types

- class	PixmapFragment

- enum	CompositionMode { CompositionMode_SourceOver, CompositionMode_DestinationOver, CompositionMode_Clear, CompositionMode_Source, ..., RasterOp_SourceAndNotDestination }

- enum	PixmapFragmentHint { OpaqueHint }

- flags	PixmapFragmentHints

- enum	RenderHint { Antialiasing, TextAntialiasing, SmoothPixmapTransform, HighQualityAntialiasing, NonCosmeticDefaultPen }

  flags	RenderHints

  Renderhints用于指定QPainter的标志，任何给定的引擎可能会或不会遵守这些标志。

  | Constant                          | Value | Description                                                  |
  | --------------------------------- | ----- | ------------------------------------------------------------ |
  | QPainter::Antialiasing            | 0x01  | 表示引擎应尽可能对图元的边缘进行抗锯齿。                     |
  | QPainter::TextAntialiasing        | 0x02  | 表示引擎应尽可能对文本进行抗锯齿。 要强行禁用文本的抗锯齿功能，请不要使用此提示。 而是在字体的样式策略上设置QFont :: NoAntialias。 |
  | QPainter::SmoothPixmapTransform   | 0x04  | 指示引擎应使用平滑的像素图变换算法（例如双线性），而不是最近的邻居。 |
  | QPainter::HighQualityAntialiasing | 0x08  | 特定于OpenGL的渲染提示，指示引擎应使用片段程序和屏幕外渲染进行抗锯齿。 |
  | QPainter::NonCosmeticDefaultPen   | 0x10  | 引擎应将宽度为0的笔（否则启用QPen :: isCosmetic（））解释为宽度为1的非化妆品笔引擎应将宽度为0的笔（否则启用QPen :: isCosmetic（））解释为宽度为1的非化妆品笔 |

## 2.Public Functions

- QPainter ()

- QPainter ( QPaintDevice * device )

- ~QPainter ()

- const QBrush &	background () const

- Qt::BGMode	backgroundMode () const

- bool	begin ( QPaintDevice * device )

- void	beginNativePainting ()

- QRectF	boundingRect ( const QRectF & rectangle, int flags, const QString & text )

- QRect	boundingRect ( const QRect & rectangle, int flags, const QString & text )

- QRect	boundingRect ( int x, int y, int w, int h, int flags, const QString & text )

- QRectF	boundingRect ( const QRectF & rectangle, const QString & text, const 

- QTextOption & option = QTextOption() )

- const QBrush &	brush () const

- QPoint	brushOrigin () const

- QRectF	clipBoundingRect () const

- QPainterPath	clipPath () const

- QRegion	clipRegion () const

- QTransform	combinedTransform () const

- CompositionMode	compositionMode () const

- QPaintDevice *	device () const

- const QTransform &	deviceTransform () const

- void	drawArc ( const QRectF & rectangle, int startAngle, int spanAngle )

- void	drawArc ( const QRect & rectangle, int startAngle, int spanAngle )

- void	drawArc ( int x, int y, int width, int height, int startAngle, int spanAngle )

- void	drawChord ( const QRectF & rectangle, int startAngle, int spanAngle )

- void	drawChord ( const QRect & rectangle, int startAngle, int spanAngle )

- void	drawChord ( int x, int y, int width, int height, int startAngle, int spanAngle )

- void	drawConvexPolygon ( const QPointF * points, int pointCount )

- void	drawConvexPolygon ( const QPoint * points, int pointCount )

- void	drawConvexPolygon ( const QPolygonF & polygon )

- void	drawConvexPolygon ( const QPolygon & polygon )

- void	drawEllipse ( const QRectF & rectangle )

- void	drawEllipse ( const QRect & rectangle )

- void	drawEllipse ( int x, int y, int width, int height )

- void	drawEllipse ( const QPointF & center, qreal rx, qreal ry )

- void	drawEllipse ( const QPoint & center, int rx, int ry )

- void	drawGlyphRun ( const QPointF & position, const QGlyphRun & glyphs )

- void	drawImage ( const QRectF & target, const QImage & image, const QRectF & source, Qt::ImageConversionFlags flags = Qt::AutoColor )

- void	drawImage ( const QRect & target, const QImage & image, const QRect & source, Qt::ImageConversionFlags flags = Qt::AutoColor )

- void	drawImage ( const QPointF & point, const QImage & image )

- void	drawImage ( const QPoint & point, const QImage & image )

- void	drawImage ( const QPointF & point, const QImage & image, const QRectF & source, Qt::ImageConversionFlags flags = Qt::AutoColor )

- void	drawImage ( const QPoint & point, const QImage & image, const QRect & source, Qt::ImageConversionFlags flags = Qt::AutoColor )

- void	drawImage ( const QRectF & rectangle, const QImage & image )

- void	drawImage ( const QRect & rectangle, const QImage & image )

- void	drawImage ( int x, int y, const QImage & image, int sx = 0, int sy = 0, int sw = -1, int sh = -1, Qt::ImageConversionFlags flags = Qt::AutoColor )

- void	drawLine ( const QLineF & line )

- void	drawLine ( const QLine & line )

- void	drawLine ( const QPoint & p1, const QPoint & p2 )

- void	drawLine ( const QPointF & p1, const QPointF & p2 )

- void	drawLine ( int x1, int y1, int x2, int y2 )

- void	drawLines ( const QLineF * lines, int lineCount )

- void	drawLines ( const QLine * lines, int lineCount )

- void	drawLines ( const QPointF * pointPairs, int lineCount )

- void	drawLines ( const QPoint * pointPairs, int lineCount )

- void	drawLines ( const QVector<QPointF> & pointPairs )

- void	drawLines ( const QVector<QPoint> & pointPairs )

- void	drawLines ( const QVector<QLineF> & lines )

- void	drawLines ( const QVector<QLine> & lines )

- **void	drawPath ( const QPainterPath & path )**

  使用当前的笔绘制轮廓并使用当前的笔刷绘制给定的画家路径。

- void	drawPicture ( const QPointF & point, const QPicture & picture )

- void	drawPicture ( const QPoint & point, const QPicture & picture )

- void	drawPicture ( int x, int y, const QPicture & picture )

- void	drawPie ( const QRectF & rectangle, int startAngle, int spanAngle )

- void	drawPie ( const QRect & rectangle, int startAngle, int spanAngle )

- void	drawPie ( int x, int y, int width, int height, int startAngle, int spanAngle )

- void	drawPixmap ( const QRectF & target, const QPixmap & pixmap, const QRectF & source )

- void	drawPixmap ( const QRect & target, const QPixmap & pixmap, const QRect & source )

- void	drawPixmap ( const QPointF & point, const QPixmap & pixmap, const QRectF & source )

- void	drawPixmap ( const QPoint & point, const QPixmap & pixmap, const QRect & source )

- void	drawPixmap ( const QPointF & point, const QPixmap & pixmap )

- void	drawPixmap ( const QPoint & point, const QPixmap & pixmap )

- void	drawPixmap ( int x, int y, const QPixmap & pixmap )

- void	drawPixmap ( const QRect & rectangle, const QPixmap & pixmap )

- void	drawPixmap ( int x, int y, int width, int height, const QPixmap & pixmap )

- void	drawPixmap ( int x, int y, int w, int h, const QPixmap & pixmap, int sx, int sy, int sw, int sh )

- void	drawPixmap ( int x, int y, const QPixmap & pixmap, int sx, int sy, int sw, int sh )

- void	drawPixmapFragments ( const PixmapFragment * fragments, int fragmentCount, const QPixmap & pixmap, PixmapFragmentHints hints = 0 )

- void	drawPixmapFragments ( const QRectF * targetRects, const QRectF * sourceRects, int fragmentCount, const QPixmap & pixmap, PixmapFragmentHints hints = 0 )

- void	drawPoint ( const QPointF & position )

- void	drawPoint ( const QPoint & position )

- void	drawPoint ( int x, int y )

- void	drawPoints ( const QPointF * points, int pointCount )

- void	drawPoints ( const QPoint * points, int pointCount )

- void	drawPoints ( const QPolygonF & points )

- void	drawPoints ( const QPolygon & points )

- void	drawPolygon ( const QPointF * points, int pointCount, Qt::FillRule fillRule = Qt::OddEvenFill )

- void	drawPolygon ( const QPoint * points, int pointCount, Qt::FillRule fillRule = Qt::OddEvenFill )

- void	drawPolygon ( const QPolygonF & points, Qt::FillRule fillRule = Qt::OddEvenFill )

- void	drawPolygon ( const QPolygon & points, Qt::FillRule fillRule = Qt::OddEvenFill )

- void	drawPolyline ( const QPointF * points, int pointCount )

- void	drawPolyline ( const QPoint * points, int pointCount )

- void	drawPolyline ( const QPolygonF & points )

- void	drawPolyline ( const QPolygon & points )

- void	drawRect ( const QRectF & rectangle )

- void	drawRect ( const QRect & rectangle )

- void	drawRect ( int x, int y, int width, int height )

- void	drawRects ( const QRectF * rectangles, int rectCount )

- void	drawRects ( const QRect * rectangles, int rectCount )

- void	drawRects ( const QVector<QRectF> & rectangles )

- void	drawRects ( const QVector<QRect> & rectangles )

- void	drawRoundedRect ( const QRectF & rect, qreal xRadius, qreal yRadius, Qt::SizeMode mode = Qt::AbsoluteSize )

- void	drawRoundedRect ( const QRect & rect, qreal xRadius, qreal yRadius, Qt::SizeMode mode = Qt::AbsoluteSize )

- void	drawRoundedRect ( int x, int y, int w, int h, qreal xRadius, qreal yRadius, Qt::SizeMode mode = Qt::AbsoluteSize )

- void	drawStaticText ( const QPointF & topLeftPosition, const QStaticText & staticText )

- void	drawStaticText ( const QPoint & topLeftPosition, const QStaticText & staticText )

- void	drawStaticText ( int left, int top, const QStaticText & staticText )

- void	drawText ( const QPointF & position, const QString & text )

- void	drawText ( const QPoint & position, const QString & text )

- void	drawText ( const QRectF & rectangle, int flags, const QString & text, QRectF * boundingRect = 0 )

- void	drawText ( const QRect & rectangle, int flags, const QString & text, QRect * boundingRect = 0 )

- void	drawText ( int x, int y, const QString & text )

- void	drawText ( int x, int y, int width, int height, int flags, const QString & text, QRect * boundingRect = 0 )

- void	drawText ( const QRectF & rectangle, const QString & text, const QTextOption & option = QTextOption() )

- void	drawTiledPixmap ( const QRectF & rectangle, const QPixmap & pixmap, const QPointF & position = QPointF() )

- void	drawTiledPixmap ( const QRect & rectangle, const QPixmap & pixmap, const QPoint & position = QPoint() )

- void	drawTiledPixmap ( int x, int y, int width, int height, const QPixmap & pixmap, int sx = 0, int sy = 0 )

- bool	end ()

- void	endNativePainting ()

- void	eraseRect ( const QRectF & rectangle )

- void	eraseRect ( const QRect & rectangle )

- void	eraseRect ( int x, int y, int width, int height )

- void	fillPath ( const QPainterPath & path, const QBrush & brush )

- void	fillRect ( const QRectF & rectangle, const QBrush & brush )

- void	fillRect ( int x, int y, int width, int height, Qt::BrushStyle style )

- void	fillRect ( const QRect & rectangle, Qt::BrushStyle style )

- void	fillRect ( const QRectF & rectangle, Qt::BrushStyle style )

- void	fillRect ( const QRect & rectangle, const QBrush & brush )

- void	fillRect ( const QRect & rectangle, const QColor & color )

- void	fillRect ( const QRectF & rectangle, const QColor & color )

- void	fillRect ( int x, int y, int width, int height, const QBrush & brush )

- void	fillRect ( int x, int y, int width, int height, const QColor & color )

- void	fillRect ( int x, int y, int width, int height, Qt::GlobalColor color )

- void	fillRect ( const QRect & rectangle, Qt::GlobalColor color )

- void	fillRect ( const QRectF & rectangle, Qt::GlobalColor color )

- const QFont &	font () const

- QFontInfo	fontInfo () const

- QFontMetrics	fontMetrics () const

- bool	hasClipping () const

- void	initFrom ( const QWidget * widget )

- bool	isActive () const

- Qt::LayoutDirection	layoutDirection () const

- qreal	opacity () const

- QPaintEngine *	paintEngine () const

- const QPen &	pen () const

- RenderHints	renderHints () const

- void	resetTransform ()

- void	restore ()

- void	rotate ( qreal angle )

- void	save ()

- void	scale ( qreal sx, qreal sy )

- void	setBackground ( const QBrush & brush )

- void	setBackgroundMode ( Qt::BGMode mode )

- **void	setBrush ( const QBrush & brush )**

  将画家的画笔设置为给定的brush 。

  画家的画笔定义形状的填充方式。

- void	setBrush ( Qt::BrushStyle style )

  将画家的画笔设置为黑色和指定的样式。

- void	setBrushOrigin ( const QPointF & position )

- void	setBrushOrigin ( const QPoint & position )

- void	setBrushOrigin ( int x, int y )

- void	setClipPath ( const QPainterPath & path, Qt::ClipOperation operation = Qt::ReplaceClip )

- void	setClipRect ( const QRectF & rectangle, Qt::ClipOperation operation = Qt::ReplaceClip )

- void	setClipRect ( int x, int y, int width, int height, Qt::ClipOperation operation = Qt::ReplaceClip )

- void	setClipRect ( const QRect & rectangle, Qt::ClipOperation operation = Qt::ReplaceClip )

- void	setClipRegion ( const QRegion & region, Qt::ClipOperation operation = Qt::ReplaceClip )

- void	setClipping ( bool enable )

- void	setCompositionMode ( CompositionMode mode )

- void	setFont ( const QFont & font )

- void	setLayoutDirection ( Qt::LayoutDirection direction )

- void	setOpacity ( qreal opacity )

- void	setPen ( const QPen & pen )

  将画家的笔设置为给定的笔。

  笔定义了绘制线条和轮廓的方式，还定义了文字颜色。

- **void	setPen ( const QColor & color )**

  设置画家的笔具有Qt :: SolidLine样式，宽度0和指定的颜色。

- void	setPen ( Qt::PenStyle style )

- void	setRenderHint ( RenderHint hint, bool on = true )

- void	setRenderHints ( RenderHints hints, bool on = true )

- void	setTransform ( const QTransform & transform, bool combine = false )

- void	setViewTransformEnabled ( bool enable )

- void	setViewport ( const QRect & rectangle )

- void	setViewport ( int x, int y, int width, int height )

- void	setWindow ( const QRect & rectangle )

- void	setWindow ( int x, int y, int width, int height )

- void	setWorldMatrixEnabled ( bool enable )

- void	setWorldTransform ( const QTransform & matrix, bool combine = false )

- void	shear ( qreal sh, qreal sv )

- void	strokePath ( const QPainterPath & path, const QPen & pen )

- bool	testRenderHint ( RenderHint hint ) const

- const QTransform &	transform () const

- void	translate ( const QPointF & offset )

- void	translate ( const QPoint & offset )

- void	translate ( qreal dx, qreal dy )

- bool	viewTransformEnabled () const

- QRect	viewport () const

- QRect	window () const

- bool	worldMatrixEnabled () const

- const QTransform &	worldTransform () const

## 3.Detailed Description

QPainter类在小部件和其他绘画设备上执行低级绘画。

QPainter提供了高度优化的功能，可以完成大多数图形GUI程序所需的功能。 它可以绘制从简单的线条到复杂的形状（如派和弦）的所有内容。 它还可以绘制对齐的文本和像素图。 通常，它绘制“自然”坐标系，但它也可以进行视图和世界变换。 QPainter可以对继承QPaintDevice类的任何对象进行操作。

QPainter的常见用法是在小部件的paint事件内：构建和自定义（例如，设置笔或画笔）painter。 然后画。 记住在绘制后销毁QPainter对象。 例如：

```c++
void SimpleExampleWidget::paintEvent(QPaintEvent *)
 {
     QPainter painter(this);
     painter.setPen(Qt::blue);
     painter.setFont(QFont("Arial", 30));
     painter.drawText(rect(), Qt::AlignCenter, "Qt");
 }
```

QPainter的核心功能是绘图，但是该类还提供了几个功能，可让您自定义QPainter的设置及其呈现质量，以及其他一些可进行裁剪的功能。另外，您可以通过指定画家的构图模式来控制如何将不同的形状合并在一起。

isActive（）函数指示绘画者是否处于活动状态。 Painter由begin（）函数和采用QPaintDevice参数的构造函数激活。 end（）函数和析构函数将其停用。

QPainter与QPaintDevice和QPaintEngine类一起构成了Qt绘画系统的基础。 QPainter是用于执行绘图操作的类。 QPaintDevice表示可以使用QPainter进行绘制的设备。 QPaintEngine提供了画家用来在不同类型的设备上绘制的界面。如果画家是活动的，则device（）返回画家在其上进行绘画的绘画设备，而paintEngine（）返回画家当前在其上操作的画家引擎。有关更多信息，请参见绘画系统。

有时，希望有人在不常见的QPaintDevice上绘画。 QPainter支持一个静态函数setRedirected（）。

警告：当paintdevice是窗口小部件时，QPainter只能在paintEvent（）函数内部或paintEvent（）调用的函数中使用；除非设置了Qt :: WA_PaintOutsidePaintEvent小部件属性。在Mac OS X和Windows上，无论此属性的设置如何，您都只能在paintEvent（）函数中进行绘制。