# QGraphicsDropShadowEffect

继承关系：QGraphicsDropShadowEffect->`QGraphicsEffect`->`QObject`

## 1.Detailed Description

QGraphicsDropShadowEffect类提供了阴影效果。

投影效果将使用投影效果渲染源。 可以使用setColor（）函数修改投影的颜色。 可以使用setOffset（）函数修改投影偏移量，并可以使用setBlurRadius（）函数更改投影的模糊半径。

默认情况下，投影阴影是半透明的深灰色（QColor（63，63，63，180））阴影，以1的半径模糊，向右下角偏移8个像素。 阴影偏移在设备坐标中指定。

## 2.Properties

blurRadius : qreal
color : QColor
offset : QPointF
xOffset : qreal
yOffset : qreal

## 3.Public Functions