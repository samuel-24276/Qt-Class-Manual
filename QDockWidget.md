# QDockWidget

`enum Qt::DockWidgetArea`
`flags Qt::DockWidgetAreas`

停靠窗口的枚举类型主要有以下几种：

| Constant                    | Value               |
| --------------------------- | ------------------- |
| `Qt::LeftDockWidgetArea`    | 0x1                 |
| ` Qt::RightDockWidgetArea`  | 0x2                 |
| `Qt::TopDockWidgetArea`     | 0x4                 |
| ` Qt::BottomDockWidgetArea` | 0x8                 |
| `Qt::AllDockWidgetAreas`    | DockWidgetArea_Mask |
| ` Qt::NoDockWidgetArea`     | 0                   |

DockWidgetAreas类型是QFlags <DockWidgetArea>的typedef。 它存储DockWidgetArea值的OR组合。

`AllDockWidgetAreas`和`NoDockWidgetArea`在实际运用中算是无效参数。

