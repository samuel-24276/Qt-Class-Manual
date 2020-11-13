# QFont

## 1.Public Types

- `enum	Capitalization { MixedCase, AllUppercase, AllLowercase, SmallCaps, Capitalize }`

  此字体适用的文本的渲染选项。

  | Constant            | Value | Description                                              |
  | ------------------- | ----- | -------------------------------------------------------- |
  | QFont::MixedCase    | 0     | 这是普通的文本呈现选项，其中**不应用任何大写字母更改**。 |
  | QFont::AllUppercase | 1     | 这会更改要以全部大写形式呈现的文本。                     |
  | QFont::AllLowercase | 2     | 这会更改要以全部小写形式呈现的文本。                     |
  | QFont::SmallCaps    | 3     | 这会更改要以小写字体显示的文本。                         |
  | QFont::Capitalize   | 4     | 这更改了要渲染的文本，每个单词的第一个字符为大写字符。   |

- `enum	HintingPreference { PreferDefaultHinting, PreferNoHinting, PreferVerticalHinting, PreferFullHinting }`

  该枚举描述了可以应用于字形的不同级别的提示，以提高在显示器上的清晰度（在这种情况下，像素的密度可能会保证此提示）。

  | Constant                     | Value | Description                                                  |
  | ---------------------------- | ----- | ------------------------------------------------------------ |
  | QFont::PreferDefaultHinting  | 0     | 使用目标平台的默认提示级别。                                 |
  | QFont::PreferNoHinting       | 1     | 如果可能，**在不提示字形轮廓的情况下呈现文本**。 文字版式将采用与例如 打印时。 |
  | QFont::PreferVerticalHinting | 2     | 如果可能，渲染没有水平提示的文本，但将字形在垂直方向上与像素网格对齐。 在密度太低而无法准确显示字形的显示器上，文本将显得清晰。 但是，由于不显示字形的水平度量，因此文本的布局将可扩展到更高密度的设备（例如打印机），而不会影响诸如换行符之类的细节。 |
  | QFont::PreferFullHinting     | 3     | 如果可能的话，在水平和垂直方向上都显示带有提示的文本。 将更改文本以优化目标设备上的可读性，但是由于度量标准将取决于文本的目标大小，因此字形，换行符和其他印刷细节的位置不会缩放，这意味着文本布局可能看起来 在具有不同像素密度的设备上有所不同。 |

  请注意，此枚举仅描述首选项，因为并非所有Qt支持的平台都支持所有提示级别。 下表详细介绍了给定的提示首选项对所选目标平台集的影响。

  注意：请注意，可以通过DirectWrite字体引擎在Windows上更改提示首选项。 在安装平台更新后的Windows Vista和Windows 7上，此功能可用。为了使用此扩展名，请使用-directwrite配置Qt。 然后，目标应用程序将取决于目标系统上DirectWrite的可用性。

- `enum	SpacingType { PercentageSpacing, AbsoluteSpacing }`

  | Constant                 | Value | Description                                                  |
  | ------------------------ | ----- | ------------------------------------------------------------ |
  | QFont::PercentageSpacing | 0     | 值100将使间距保持不变； 值200将使字符后的间距扩大字符本身的宽度。 |
  | QFont::AbsoluteSpacing   | 1     | 正值将字母间距增加相应像素； 负值会减小间距。                |

- `enum	Stretch { UltraCondensed, ExtraCondensed, Condensed, SemiCondensed, ..., UltraExpanded }`

  遵循CSS命名约定的预定义拉伸值。 值越高，文本越伸展。

  | Constant                                  | Value | Description |
  | ----------------------------------------- | ----- | ----------- |
  | QFont::UltraCondensed超浓缩               | 50    | 50          |
  | QFont::ExtraCondensedExtraCondensed很浓缩 | 62    | 62          |
  | QFont::Condensed                          | 75    | 75          |
  | QFont::SemiCondensed半浓缩                | 87    | 87          |
  | QFont::Unstretched不拉伸                  | 100   | 100         |
  | QFont::SemiExpanded                       | 112   | 112         |
  | QFont::Expanded                           | 125   | 125         |
  | QFont::ExtraExpanded                      | 150   | 150         |
  | QFont::UltraExpanded                      | 200   | 200         |

  

- `enum	Style { StyleNormal, StyleItalic, StyleOblique }`

  该枚举描述了用于**显示文本的不同字形样式**。

  | Constant            | Value | Description                                                  |
  | ------------------- | ----- | ------------------------------------------------------------ |
  | QFont::StyleNormal  | 0     | 无样式文字中使用的普通字形。                                 |
  | QFont::StyleItalic  | 1     | 专为表示斜体文本而设计的斜体字形。                           |
  | QFont::StyleOblique | 2     | 具有斜体外观的字形通常基于未样式化的字形，但出于表示斜体文本的目的而未进行微调。 |

- `enum	StyleHint { AnyStyle, SansSerif, Helvetica, Serif, ..., System }`

  如果选定的字体系列不可用，字体匹配算法将使用样式提示来查找适当的默认系列。

  | Constant        | Value | Description |
  | --------------- | ----- | ----------- |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |
  | QFont::AnyStyle |       |             |

  - QPalette palette;
    palette.setColor(QPalette::Text,Qt::red); 
    lineEdit.setPalette(palette);
  - lineEdit.setStyleSheet("color:red");//文本颜色
    lineEdit.setStyleSheet("background-color:red");//背景色
  - lineEdit.setFont(QFont("Timers" , 28 ,  QFont::Bold));
  -  label = QLabel("<h1><fontcolor=black>定值1</font><fontcolor=red>定值2</font><font color=black>定值3</font></h1>");

- `enum	StyleStrategy { PreferDefault, PreferBitmap, PreferDevice, PreferOutline, ..., ForceIntegerMetrics }`

- `enum	Weight { Light, Normal, DemiBold, Bold, Black }`

## 2.Public Functions

- QFont ()

- QFont ( const QString & family, int pointSize = -1, int weight = -1, bool italic = false )

- QFont ( const QFont & font, QPaintDevice * pd )

- QFont ( const QFont & font )

- ~QFont ()

- bool	bold () const

- Capitalization	capitalization () const

- QString	defaultFamily () const

- bool	exactMatch () const

- QString	family () const

- bool	fixedPitch () const

- FT_Face	freetypeFace () const

- bool	fromString ( const QString & descrip )

- HFONT	handle () const

- HintingPreference	hintingPreference () const

- bool	isCopyOf ( const QFont & f ) const

- bool	italic () const

- bool	kerning () const

- QString	key () const

- QString	lastResortFamily () const

- QString	lastResortFont () const

- qreal	letterSpacing () const

- SpacingType	letterSpacingType () const

- quint32	macFontID () const

- bool	overline () const

- int	pixelSize () const

- int	pointSize () const

- qreal	pointSizeF () const

- bool	rawMode () const

- QString	rawName () const

- QFont	resolve ( const QFont & other ) const

- void	setBold ( bool enable )

- `void	setCapitalization ( Capitalization caps )`

  将此字体的大写字母设置为大写。

  字体的大写字母使文本以所选的大写字母显示。

- void	setFamily ( const QString & family )

- void	setFixedPitch ( bool enable )

- void	setHintingPreference ( HintingPreference hintingPreference )

- void	setItalic ( bool enable )

- void	setKerning ( bool enable )

- void	setLetterSpacing ( SpacingType type, qreal spacing )

- void	setOverline ( bool enable )

- void	setPixelSize ( int pixelSize )

- void	setPointSize ( int pointSize )

- void	setPointSizeF ( qreal pointSize )

- void	setRawMode ( bool enable )

- void	setRawName ( const QString & name )

- void	setStretch ( int factor )

- void	setStrikeOut ( bool enable )

- void	setStyle ( Style style )

- void	setStyleHint ( StyleHint hint, StyleStrategy strategy = PreferDefault )

- void	setStyleName ( const QString & styleName )

- void	setStyleStrategy ( StyleStrategy s )

- void	setUnderline ( bool enable )

- `void	setWeight ( int weight )`

  将字体的权重设置为weight，它应该是QFont :: Weight枚举中的值。

- **int	weight () const**

  返回**字体的粗细**，它是QFont :: Weight的枚举值之一。

- **`void	setWordSpacing ( qreal spacing )`**

  将字体的字间距设置为spacing 。

  单词间距更改单个单词之间的默认间距。 正值将字间距增加相应数量的像素，而负值会相应地减小字间距。

  单词间距不适用于书写系统，在该书写系统中，各个单词之间不用空格隔开。

- int	stretch () const

- bool	strikeOut () const

- Style	style () const

- StyleHint	styleHint () const

- QString	styleName () const

- StyleStrategy	styleStrategy () const

- QString	toString () const

- bool	underline () const

- qreal	wordSpacing () const

- operator QVariant () const

- bool	operator!= ( const QFont & f ) const

- bool	operator< ( const QFont & f ) const

- QFont &	operator= ( const QFont & font )

- bool	operator== ( const QFont & f ) const

## 3.Static Public Members

- void	insertSubstitution ( const QString & familyName, const QString & substituteName )
- void	insertSubstitutions ( const QString & familyName, const QStringList & substituteNames )
- void	removeSubstitution ( const QString & familyName )
- QString	substitute ( const QString & familyName )
- QStringList	substitutes ( const QString & familyName )
- QStringList	substitutions ()

## 4.Related Non-Members

- QDataStream &	operator<< ( QDataStream & s, const QFont & font )
- QDataStream &	operator>> ( QDataStream & s, QFont & font )

## 5.Detailed Description

