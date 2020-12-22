# QAbstractScrollArea

## 1.Public Functions

- `void setHorizontalScrollBar(QScrollBar *scrollBar)`

  **用scrollBar替换现有的水平滚动条**，并在新的滚动条上设置以前所有滚动条的滑块属性。 然后**删除以前的滚动条**。
  QAbstractScrollArea默认已经提供了水平和垂直滚动条。 您可以调用此函数将默认的水平滚动条替换为您自己的自定义滚动条。

- `void setVerticalScrollBar(QScrollBar *scrollBar)`

  用scrollBar替换现有的垂直滚动条，并在新的滚动条上设置以前所有滚动条的滑块属性。 然后删除以前的滚动条。
  默认情况下，QAbstractScrollArea已提供垂直和水平滚动条。 您可以调用此函数，用您自己的自定义滚动条替换默认的垂直滚动条。

- `void setHorizontalScrollBarPolicy(Qt::ScrollBarPolicy)`

  此属性保存水平滚动条的策略,有以下几种：

  - `Qt::ScrollBarAsNeeded`

    当内容太大而无法容纳时，QAbstractScrollArea将显示滚动条。 这是默认值。

  - `Qt::ScrollBarAlwaysOff`

    关闭进度条显示

  - `Qt::ScrollBarAlwaysOn`

    QAbstractScrollArea始终显示滚动条。 在具有瞬时滚动条的系统上，将忽略此属性

- `void setVerticalScrollBarPolicy(Qt::ScrollBarPolicy)`