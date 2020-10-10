# QTabWidget

继承自基类`QWidget`

# 1.Signals

- `void currentChanged(int index)`

  当前页面索引index更改时，将发出此信号。 该参数是新的当前页面索引位置，如果没有新的位置，则返回-1（例如，如果QTabWidget中没有窗口小部件）

- `void tabBarClicked(int index)`

- `void tabBarDoubleClicked(int index)`

- `void tabCloseRequested(int index)`

# 2.Public Slots

- `void    setCurrentIndex(int index)`

- `void setCurrentWidget(QWidget *widget)`

要实现按下不同按钮显示不同QTabWidget页面的功能，可以编写按钮的clicked()槽函数，在槽函数内利用`setCurrentIndex()`来设置QTabWidget显示的页面。

要实现QTabWidget页面切换，`QRadioButton`按钮随页面切换选中不同按钮的功能，可以编写当前QTabWidget的currentChanged()信号的槽函数，在里面通过传入的当前页面索引，设置不同的选中按钮。