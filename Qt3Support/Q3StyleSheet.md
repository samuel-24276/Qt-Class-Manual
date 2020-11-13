# Q3StyleSheet

继承关系:`Q3StyleSheet`->`QObject`

## 1.Detailed Description

Q3StyleSheet类是用于RTF呈现的样式的集合和标记的生成器。

通过为样式表创建Q3StyleSheetItem对象，您可以构建一组标签的定义。 内部富文本呈现系统将使用此定义来解析和显示样式表适用的文本文档。 **富文本通常在QTextEdit或QTextBrowser中可视化**。 但是，QLabel，QWhatsThis和QMessageBox也支持它，并且可能还会有其他类。 借助QSimpleRichText，也可以将富文本格式渲染器用于自定义窗口小部件。

默认的Q3StyleSheet对象具有以下样式绑定，按结构绑定，锚点，字符样式绑定（即，内联样式），特殊元素（例如水平线或图像）和其他标签排序。 另外，富文本格式支持简单的HTML表。

### 1.1.结构标签

| Structuring tags结构化标签        | Notes注解                                                    |
| --------------------------------- | ------------------------------------------------------------ |
| <qt>...</qt>                      | Qt富文本文档。 它包含以下属性：<br/>**title**-文档的标题。 该属性可以通过QTextEdit :: documentTitle（）轻松访问。<br/>**type**-文档的类型。 默认类型是页面。 它指示文档显示在自己的页面中。 另一种样式是细节，可以用几句话来更详细地解释某些表达。 有关详细信息，QTextBrowser然后将保留当前页面并在类似于QWhatsThis的小弹出窗口中显示新文档。 请注意，链接在具有<qt type =“ detail”> ... </ qt>的文档中不起作用。<br/>**bgcolor**-背景色，例如bgcolor =“ yellow”或bgcolor =“＃0000FF”。<br/>**background**-背景像素图，例如background =“ granite.xpm”。 像素图名称将由Q3MimeSourceFactory（）解析。<br/>**text**-默认的文本颜色，例如text =“ red”。<br/>**link**-链接颜色，例如link =“ green”。 |
| <h1>...</h1>                      | 1级标题                                                      |
| <h2>...</h2>                      | 2级标题                                                      |
| <h3>...</h3>                      | 3级标题                                                      |
| <p>...</p>                        | 左对齐的段落。 使用align属性调整对齐方式。 可能的值是left，right和center。 |
| <center>...<br/></center>         | 居中的段落                                                   |
| <blockquote>...<br/></blockquote> | 缩进的段落对块引用很有用。                                   |
| <ul>...</ul>                      | 无序列表。 您还可以传递类型参数来定义项目符号样式。 默认值为type = disc; 其他类型是圆形和正方形。 |
| <ol>...</ol>                      | 有序列表。 您还可以传递类型参数来定义枚举标签样式。 默认值为type =“ 1”; 其他类型是“ a”和“ A”。 |
| <li>...</li>                      | 列表项。 **此标记只能在<ol>或<ul>的上下文中使用**。          |
| <pre>...</pre>                    | 对于更大的代码块。 内容中的空白被保留。 对于少量代码，请使用内联样式代码。 |

### 1.2.锚点和链接标签

| Anchor tags  | Notes                                                        |
| ------------ | ------------------------------------------------------------ |
| \<a>...\</a> | 锚点或链接。<br/>通过使用**href**属性（例如 \<a href="target.qml">链接文本\</a>）创建链接。 指向文档内目标的链接的实现方式与HTML相同，例如 <br/> \<a href="target.qml#subtitle">链接文本\</a>。<br/>通过使用**name**属性（例如 \<a name="subtitle"> \<h2> Sub Title \</ h2> \</a>）创建目标。 |

若要对<a></a>标签内的网址设置字体格式，需要嵌套<p></p>标签，在p标签内包含文字，p内设置字体格式。

### 1.3.字符样式

| Style tags             | Notes                                                        |
| ---------------------- | ------------------------------------------------------------ |
| \<em>...\</em>         | 强调。 默认情况下，它与<i> ... </ i>（斜体）相同。           |
| \<strong>...\</strong> | 强大。 默认情况下，它与<b> ... </ b>（粗体）相同。           |
| \<i>...\</i>           | 斜体样式                                                     |
| \<b>...\</b>           | 粗体样式                                                     |
| \<u>...\</u>           | 下划线                                                       |
| \<s>...\</s>           | 删除字体样式。                                               |
| \<big>...\</big>       | 大号字体                                                     |
| \<small>...\</small>   | 小号字体                                                     |
| \<sub>...\</sub>       | 下标文字                                                     |
| \<sup>...\</sup>       | 上标文字                                                     |
| \<code>...\</code>     | 表示代码。 默认情况下，它与<tt> ... </ tt>（打字机）相同。 对于较大的代码块，请使用块标记<pre>。 |
| \<tt>...\</tt>         | 打印机字体风格                                               |
| \<font>...\</font>     | 自定义字体大小，字体和文本颜色。 标记了解以下属性：<br/>- color-文本颜色，例如color =“ red”或color =“＃FF0000”。<br/>- size-字体的逻辑大小。 支持逻辑大小1到7。 该值可以是绝对值（例如size = 3）或相对值（size = -2）。 在后一种情况下，只需添加大小即可。<br/>- face-字体系列，例如face = times。 |

### 1.4.特殊元素

| Special tags     | Notes                                                        |
| ---------------- | ------------------------------------------------------------ |
| <img>            | 一个图像。 源属性中提供了mime源工厂的图像名称，例如<img src =“ qt.xpm”>。image标签还了解确定图像大小的属性width和height。 **如果像素图不适合指定的大小，它将自动缩放（通过使用QImage :: smoothScale（）**）。<br/>**align属性确定图像的放置位置**。 默认情况下，图像像普通字符一样被内联放置。 指定左侧或右侧以将图像放置在相应的一侧 |
| <hr>             | 水平线                                                       |
| <br/>            | 换行                                                         |
| <nobr>...</nobr> | no break.防止自动换行                                        |

另外，富文本格式支持简单的HTML表。 一个表由一个或多个行组成，每个行包含一个或多个单元格。 单元是数据单元还是标头单元，具体取决于它们的内容。 支持跨越行和列的单元格。

| Table tags         | Notes                                                        |
| ------------------ | ------------------------------------------------------------ |
| <table>...</table> | 一张表。 表支持以下属性：<br/>bgcolor-背景色。<br/>width-表格宽度 这**可以是绝对像素宽度，也可以是表格宽度的相对百分比**，例如width = 80％。<br/>border-表格边框的宽度。 默认值为0（=无边框）。<br/>**cellspacing-表格单元格周围的额外空间**。 预设值为2。<br/>**cellpadding-表格单元格内容周围的额外空间**。 预设值为1。 |
| <tr>...</tr>       | 表格行。 这仅在表内有效。 行支持以下属性：<br/>bgcolor-背景色。 |
| <th>...</th>       | 表标题单元格。 与td类似，但默认为居中对齐和粗体。            |
| <td>...</td>       | 表数据单元。 这仅在tr内有效。 单元格支持以下属性：<br/>bgcolor-背景色。<br/>width-单元格宽度 这可以是绝对像素宽度，也可以是表格宽度的相对百分比，例如width = 50％。<br/>**colspan-指定此单元格跨越多少列**。 预设值为1。<br/>**rowspan-指定此单元格跨越多少行**。 预设值为1。<br/>align-Qt :: Alignment; 可能的值是left，right和center。 默认为左。<br/>valign-Qt ::垂直对齐; 可能的值是top，middle和bottom。 默认值为中。 |

## 2.Public Functions

- Q3StyleSheet ( QObject * parent = 0, const char * name = 0 )

- virtual	~Q3StyleSheet ()

- virtual void	error ( const QString & *msg* ) const

  当处理富文本格式时发生错误时，将调用此虚拟函数。 **如果您需要捕获错误消息，请重新实现它**。

  如果某些富文本字符串包含样式表无法理解的标签，某些标签嵌套不正确或标签未正确关闭，则可能会发生错误。

  *msg*是错误消息。

- Q3StyleSheetItem *	item ( const QString & name )

  返回名为name的样式，如果没有，则返回0。

- const Q3StyleSheetItem *	item ( const QString & name ) const

- virtual void	scaleFont ( QFont & *font*, int *logicalSize* ) const

  将字体*font*缩放为与逻辑字体大小*logicalSize*相对应的适当物理点大小。

  调用此函数时，字体的磅值与逻辑字体大小3相对应。

  逻辑字体大小从1到7，最小为1。

## 3.Static Public Members

- QString	convertFromPlainText ( const QString & plain, Q3StyleSheetItem::WhiteSpaceMode mode = Q3StyleSheetItem::WhiteSpacePre )

  辅助功能。 **将纯文本字符串纯文本转换为富文本格式的段落，同时保留其大部分外观**。

  mode定义空白模式。 可能的值为Q3StyleSheetItem :: WhiteSpacePre（不包装，保留所有空白）和Q3StyleSheetItem :: WhiteSpaceNormal（包装，简化的空白）。

- Q3StyleSheet *	defaultSheet ()

  返回应用程序范围内的默认样式表。 富文本格式呈现类（例如QSimpleRichText，QWhatsThis和QMessageBox）使用此样式表来定义富文本格式文档中的呈现样式和可用标签。 它还用作更复杂的渲染小部件QTextEdit和QTextBrowser的初始样式表。

- QString	escape ( const QString & plain )

  辅助功能。 将纯文本字符串plain 转换为带有任何HTML元字符转义的富文本格式的字符串。

- bool	mightBeRichText ( const QString & text )

  如果字符串文本可能是富文本，则返回true； 否则返回false。

  此函数使用快速的启发式方法，因此很简单。 它主要检查在第一个换行符之前是否有一些看起来像标签的东西。 尽管结果在大多数情况下可能是正确的，但不能保证。

- void	setDefaultSheet ( Q3StyleSheet * sheet )

  将应用程序范围的默认样式表设置为工作表，删除先前设置的任何样式表。 所有权已转移到Q3StyleSheet。

## 4.常用样式

### 4.1.滚动条样式

```c++
verticalScrollBar()->setStyleSheet("QScrollBar:vertical"	//滚动条
                                   "{"
                                   "width:8px;"
                                   "background:rgba(0,0,0,0%);"
                                   "margin:0px,0px,0px,0px;"
                                   "padding-top:9px;"
                                   "padding-bottom:9px;"
                                   "}"
                                   "QScrollBar::handle:vertical"//滑块
                                   "{"
                                   "width:8px;"
                                   "background:rgba(0,0,0,25%);"
                                   " border-radius:4px;"
                                   "min-height:20;"
                                   "}"
                                   "QScrollBar::handle:vertical:hover"//鼠标悬浮在滑块上
                                   "{"
                                   "width:8px;"
                                   "background:rgba(0,0,0,50%);"
                                   " border-radius:4px;"
                                   "min-height:20;"
                                   "}"
                                   "QScrollBar::add-line:vertical"
                                   "{"
                                   "height:9px;width:8px;"
                                   "border-image:url(:/images/a/3.png);"
                                   "subcontrol-position:bottom;"
                                   "}"
                                   "QScrollBar::sub-line:vertical"
                                   "{"
                                   "height:9px;width:8px;"
                                   "border-image:url(:/images/a/1.png);"
                                   "subcontrol-position:top;"
                                   "}"
                                   "QScrollBar::add-line:vertical:hover"
                                   "{"
                                   "height:9px;width:8px;"
                                   "border-image:url(:/images/a/4.png);"
                                   "subcontrol-position:bottom;"
                                   "}"
                                   "QScrollBar::sub-line:vertical:hover"
                                   "{"
                                   "height:9px;width:8px;"
                                   "border-image:url(:/images/a/2.png);"
                                   "subcontrol-position:top;"
                                   "}"
                                   "QScrollBar::add-page:vertical,QScrollBar::sub-page:vertical"//滚动条上端和下端
                                   "{"
                                   "background:rgba(0,0,0,10%);"
                                   "border-radius:4px;"
                                   "}"
                                  );
```

### 4.2.QPushButton样式

```c++
BtnOpenS->setStyleSheet(
    "QPushButton{
    "font-family: PingFangSC-Regular;"
    "font-size: 12px;"
    "color: #008AD9;"
    "text-align: left;"
    "text-decoration: underline;"
    "border: none;}"
    "QPushButton:hover{color:red;}"//鼠标悬浮变色
);
```

