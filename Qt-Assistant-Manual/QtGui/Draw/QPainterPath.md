# QPainterPath

继承关系：`QPainterPath`->``QGraphicsEffect``->`QObject`

## 1.Public Types

- class	Element

  QPainterPath :: Element类指定子路径的位置和类型。

  构造QPainterPath对象后，可以将诸如直线和曲线之类的子路径添加到路径中（创建QPainterPath :: LineToElement和QPainterPath :: CurveToElement组件）。

  直线和曲线从currentPosition（）延伸到作为参数传递的位置。 QPainterPath对象的currentPosition（）始终是最后添加的子路径（或初始起点）的结束位置。 moveTo（）函数可用于移动currentPosition（）而不添加直线或曲线，而创建QPainterPath :: MoveToElement组件。

- enum	ElementType { MoveToElement, LineToElement, CurveToElement, CurveToDataElement }

  该枚举描述了用于连接子路径中的顶点的元素的类型。

  请注意，实际上使用addEllipse（），addPath（），addPolygon（），addRect（），addRegion（）和addText（）便利函数作为封闭子路径添加的元素实际上是使用moveTo作为单独元素的集合添加到路径中的 （），lineTo（）和cubicTo（）函数。

  | Constant                         | Value | Description                                    |
  | -------------------------------- | ----- | ---------------------------------------------- |
  | QPainterPath::MoveToElement      | 0     | 新的子路径。 另请参见moveTo（）。              |
  | QPainterPath::LineToElement      | 1     | 一条线。 另请参见lineTo（）。                  |
  | QPainterPath::CurveToElement     | 2     | 一条曲线。 另请参见cubicTo（）和quadTo（）。   |
  | QPainterPath::CurveToDataElement | 3     | 描述CurveToElement元素中的曲线所需的额外数据。 |

## 2.Public Functions

- QPainterPath ()

- QPainterPath ( const QPointF & startPoint )

- QPainterPath ( const QPainterPath & path )

- ~QPainterPath ()

- **void	lineTo ( const QPointF & endPoint )**

  从当前位置到给定的端点添加一条直线。 绘制直线后，当前位置将更新为直线的终点。

- void	lineTo ( qreal x, qreal y )

- **void	moveTo ( const QPointF & point )**

  将当前点移动到给定点，*隐式*开始一个新的子路径并关闭前一个子路径。

- void	moveTo ( qreal x, qreal y )

- void	addEllipse ( const QRectF & boundingRectangle )

  在指定的boundingRectangle中创建一个椭圆，并将其作为封闭的子路径添加到绘制器路径。

  椭圆由顺时针曲线组成，从零度（3点钟位置）开始和结束。

- **void	addEllipse ( qreal x, qreal y, qreal width, qreal height )**

  在由（x，y），width和height 的左上角定义的边界矩形内创建一个椭圆，并将其作为封闭的子路径添加到绘制器路径。

- void	addEllipse ( const QPointF & center, qreal rx, qreal ry )

  创建一个半径为rx和ry的居中椭圆，并将其作为闭合子路径添加到绘制器路径。

- void	addPath ( const QPainterPath & path )

  将给定path 添加为该路径作为封闭子路径。

- **void	addPolygon ( const QPolygonF & polygon )**

  将给定的多边形作为（未封闭的）子路径添加到路径中。

  请**注意**，添加多边形后的当前位置是多边形中的最后一个点。 要将线画回到第一点，请使用closeSubpath（）函数。

- **void	addRect ( const QRectF & rectangle )**

  将给定的矩形作为封闭的子路径添加到此路径。

  矩形被添加为一组顺时针的线。 添加矩形后，画家路径的当前位置在矩形的左上角。

- **void	addRect ( qreal x, qreal y, qreal width, qreal height )**

  在位置（x，y）处添加具有给定宽度和高度的矩形，作为闭合子路径。

- void	addRegion ( const QRegion & region )

  通过将区域中的每个矩形添加为单独的封闭子路径，将给定区域添加到路径中。

- void	addRoundedRect ( const QRectF & rect, qreal xRadius, qreal yRadius, Qt::SizeMode mode = Qt::AbsoluteSize )

- void	addRoundedRect ( qreal x, qreal y, qreal w, qreal h, qreal xRadius, qreal yRadius, Qt::SizeMode mode = Qt::AbsoluteSize )

- void	addText ( const QPointF & point, const QFont & font, const QString & text )

- void	addText ( qreal x, qreal y, const QFont & font, const QString & text )

- qreal	angleAtPercent ( qreal t ) const

- void	arcMoveTo ( const QRectF & rectangle, qreal angle )

- void	arcMoveTo ( qreal x, qreal y, qreal width, qreal height, qreal angle )

- void	arcTo ( const QRectF & rectangle, qreal startAngle, qreal sweepLength )

- void	arcTo ( qreal x, qreal y, qreal width, qreal height, qreal startAngle, qreal sweepLength )

- QRectF	boundingRect () const

- void	closeSubpath ()

- void	connectPath ( const QPainterPath & path )

- bool	contains ( const QPointF & point ) const

- bool	contains ( const QRectF & rectangle ) const

- bool	contains ( const QPainterPath & p ) const

- QRectF	controlPointRect () const

- void	cubicTo ( const QPointF & c1, const QPointF & c2, const QPointF & endPoint )

- void	cubicTo ( qreal c1X, qreal c1Y, qreal c2X, qreal c2Y, qreal endPointX, qreal endPointY )

- QPointF	currentPosition () const

- const QPainterPath::Element &	elementAt ( int index ) const

- int	elementCount () const

- Qt::FillRule	fillRule () const

- QPainterPath	intersected ( const QPainterPath & p ) const

- bool	intersects ( const QRectF & rectangle ) const

- bool	intersects ( const QPainterPath & p ) const

- bool	isEmpty () const

- qreal	length () const

- qreal	percentAtLength ( qreal len ) const

- QPointF	pointAtPercent ( qreal t ) const

- void	quadTo ( const QPointF & c, const QPointF & endPoint )

- void	quadTo ( qreal cx, qreal cy, qreal endPointX, qreal endPointY )

- void	setElementPositionAt ( int index, qreal x, qreal y )

- **void	setFillRule ( Qt::FillRule fillRule )**

  将绘画者路径的填充规则设置为给定的fillRule。 Qt提供了两种填充路径的方法：

  | Constant        | Value | Description                                                  |
  | --------------- | ----- | ------------------------------------------------------------ |
  | Qt::OddEvenFill | 0     | 指定使用奇数偶数填充规则填充区域。 使用此规则，我们可以通过以下方法确定点是否在形状内。 从该点到形状外部的位置绘制一条水平线，并计算相交的数量。 如果相交数是奇数，则该点在形状内。 此模式是默认模式。 |
  | Qt::WindingFill | 1     | 指定使用非零缠绕规则填充区域。 使用此规则，我们可以通过以下方法确定点是否在形状内。 从该点到形状外部的位置绘制一条水平线。 确定每个交点处的线的方向是向上还是向下。 绕组数是通过将每个交叉点的方向求和来确定的。 如果数字非零，则该点在形状内。 在大多数情况下，此填充模式也可以视为闭合形状的交集。 |

  

- QPainterPath	simplified () const

- qreal	slopeAtPercent ( qreal t ) const

- QPainterPath	subtracted ( const QPainterPath & p ) const

- void	swap ( QPainterPath & other )

- QPolygonF	toFillPolygon ( const QTransform & matrix ) const

- QPolygonF	toFillPolygon ( const QMatrix & matrix = QMatrix() ) const

- QList<QPolygonF>	toFillPolygons ( const QTransform & matrix ) const

- QList<QPolygonF>	toFillPolygons ( const QMatrix & matrix = QMatrix() ) const

- QPainterPath	toReversed () const

- QList<QPolygonF>	toSubpathPolygons ( const QTransform & matrix ) const

- QList<QPolygonF>	toSubpathPolygons ( const QMatrix & matrix = QMatrix() ) const

- void	translate ( qreal dx, qreal dy )

- void	translate ( const QPointF & offset )

- QPainterPath	translated ( qreal dx, qreal dy ) const

- QPainterPath	translated ( const QPointF & offset ) const

- QPainterPath	united ( const QPainterPath & p ) const

- bool	operator!= ( const QPainterPath & path ) const

- QPainterPath	operator& ( const QPainterPath & other ) const

- QPainterPath &	operator&= ( const QPainterPath & other )

- QPainterPath	operator+ ( const QPainterPath & other ) const

- QPainterPath &	operator+= ( const QPainterPath & other )

- QPainterPath	operator- ( const QPainterPath & other ) const

- QPainterPath &	operator-= ( const QPainterPath & other )

- QPainterPath &	operator= ( const QPainterPath & path )

- bool	operator== ( const QPainterPath & path ) const

- QPainterPath	operator| ( const QPainterPath & other ) const

- QPainterPath &	operator|= ( const QPainterPath & other )

## 3.Related Non-Members

- QDataStream &	operator<< ( QDataStream & stream, const QPainterPath & path )
- QDataStream &	operator>> ( QDataStream & stream, QPainterPath & path )

## 4.Detailed Description

QPainterPath类为绘画操作提供了一个容器，从而可以构造和重用图形形状。

绘制器路径是由许多图形构造块（例如矩形，椭圆形，直线和曲线）组成的对象。可以将构建块连接到闭合的子路径中，例如以矩形或椭圆形。闭合路径的起点和终点重合。或者它们可以作为未封闭的子路径（例如直线和曲线）独立存在。

QPainterPath对象可用于填充，概述和裁剪。要为给定的绘制路径生成可填充的轮廓，请使用QPainterPathStroker类。与常规绘图操作相比，画家路径的主要优势在于，复杂的形状只需要创建一次即可。然后可以仅使用对QPainter :: drawPath（）函数的调用来绘制它们多次。

QPainterPath提供了一组函数，这些函数可用于获取有关路径及其元素的信息。另外，可以使用toReversed（）函数反转元素的顺序。还有一些函数可以将此绘制程序路径对象转换为多边形表示。

### Composing a QPainterPath

QPainterPath对象可以构造为具有给定起点的空路径，也可以构造为另一个QPainterPath对象的副本。创建之后，可以使用lineTo（），arcTo（），cubicTo（）和quadTo（）函数将直线和曲线添加到路径。直线和曲线从currentPosition（）延伸到作为参数传递的位置。

QPainterPath对象的currentPosition（）始终是最后添加的子路径（或初始起点）的结束位置。使用moveTo（）函数移动currentPosition（）而不添加组件。 moveTo（）函数隐式启动一个新的子路径，并关闭前一个子路径。启动新子路径的另一种方法是调用closeSubpath（）函数，该函数通过从currentPosition（）回到路径的起始位置添加一条线来关闭当前路径。请注意，新路径的初始currentPosition（）将具有（0，0）。

QPainterPath类还提供了几个方便的功能，可将封闭的子路径添加到绘制器路径：addEllipse（），addPath（），addRect（），addRegion（）和addText（）。 addPolygon（）函数添加未封闭的子路径。实际上，这些函数都是moveTo（），lineTo（）和cubicTo（）操作的集合。

另外，可以使用connectPath（）函数将路径添加到当前路径。但是请注意，此函数将通过添加一行将当前路径的最后一个元素连接到给定元素的第一个元素。

以下是显示如何使用QPainterPath对象的代码段：