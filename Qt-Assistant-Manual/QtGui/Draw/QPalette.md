# QPalette



## 4.Detailed Description

QPalette类包含每种小部件状态的颜色组。 调色板由三个颜色组组成：Active, Disabled, and Inactive。 Qt中的所有小部件都包含一个调色板，并使用其调色板进行绘制。 这使用户界面易于配置并且更易于保持一致。 如果创建新的小部件，我们强烈建议您使用调色板中的颜色，而不是硬编码特定颜色。 颜色组：

- 活动组（Active）用于具有**键盘焦点**的窗口。 
- 不活动组（Inactive）用于其他窗口。
-  “禁用”组（Disabled）用于因某些原因禁用的窗口小部件（非Windows）。

活动窗口和非活动窗口都可以包含禁用的窗口小部件。 （禁用的小部件通常称为不可访问或显示为灰色。）

 在大多数样式中，“活动”和“非活动”外观相同。 

可以使用setColor（）和setBrush（）为调色板的任何颜色组中的特定角色设置颜色和画笔。颜色组包含小部件用来绘制自身的一组颜色。我们**建议小部件使用调色板中的颜色组角色，例如“foreground”和“"base”，而不要使用文字颜色**，例如“红色”或“绿松石turquoise”。颜色角色在ColorRole文档中进行了枚举和定义。

 强烈建议您使用当前样式的默认调色板（由QApplication :: palette（）返回），并根据需要进行修改。这是由Qt的小部件在绘制时完成的。 

要修改颜色组，请调用函数setColor（）和setBrush（），具体取决于您要纯色还是像素图图案。 

还有对应的color（）和brush（）getters，以及用于获取当前ColorGroup的ColorRole的常用便利函数：window（），windowText（），base（）等。

 您可以使用复制构造函数复制一个调色板，并使用isCopyOf（）测试两个调色板是否相同。 

QPalette通过使用**隐式共享**进行了优化，因此**将QPalette对象作为参数传递非常有效**。

警告：例如，某些样式如果使用本机主题引擎，则不会在所有图形上使用调色板。 Windows XP，Windows Vista和Mac OS X样式都是这种情况。