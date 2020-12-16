# QSizePolicy

## 1.Public Types

- `enum	ControlType { DefaultType, ButtonBox, CheckBox, ComboBox, ..., ToolButton }`

  `flags	ControlTypes`

  这个枚举根据布局交互指定了不同类型的小部件：

  | Constant                 | Value      | Description                                        |
  | ------------------------ | ---------- | -------------------------------------------------- |
  | QSizePolicy::DefaultType | 0x00000001 | 未指定时的默认类型。                               |
  | QSizePolicy::ButtonBox   | 0x00000002 | 一个QDialogButtonBox 实例                          |
  | QSizePolicy::CheckBox    | 0x00000004 | 一个QCheckBox实例                                  |
  | QSizePolicy::ComboBox    | 0x00000008 | 一个QComboBox 实例                                 |
  | QSizePolicy::Frame       | 0x00000010 | 一个QFrame 实例                                    |
  | QSizePolicy::GroupBox    | 0x00000020 | 一个QGroupBox 实例                                 |
  | QSizePolicy::Label       | 0x00000040 | 一个QLabel 实例                                    |
  | QSizePolicy::Line        | 0x00000080 | 具有QFrame :: HLine或QFrame :: VLine的QFrame实例。 |
  | QSizePolicy::LineEdit    | 0x00000100 | 一个QLineEdit 实例                                 |
  | QSizePolicy::PushButton  | 0x00000200 | 一个QPushButton实例                                |
  | QSizePolicy::RadioButton | 0x00000400 | 一个QRadioButton 实例                              |
  | QSizePolicy::Slider      | 0x00000800 | 一个QAbstractSlider实例                            |
  | QSizePolicy::SpinBox     | 0x00001000 | 一个QAbstractSpinBox实例                           |
  | QSizePolicy::TabWidget   | 0x00002000 | 一个QTabWidget 实例                                |
  | QSizePolicy::ToolButton  | 0x00004000 | 一个QToolButton实例                                |

  ControlTypes类型是QFlags <ControlType>的typedef。 它存储ControlType值的OR组合。

- `enum	Policy { Fixed, Minimum, Maximum, Preferred, ..., Ignored }`

  `enum	PolicyFlag { GrowFlag, ExpandFlag, ShrinkFlag, IgnoreFlag }`

  该枚举描述了构造QSizePolicy时使用的各种尺寸调整类型。

  | Constant               | Value                              | Description                                                  |
  | ---------------------- | ---------------------------------- | ------------------------------------------------------------ |
  | QSizePolicy::Fixed     | 0                                  | 窗口部件永远不会增大或缩小（例如，按钮的垂直方向）。         |
  | QSizePolicy::Minimum   | GrowFlag                           | 窗口部件的sizeHint()是它的最小大小，如有必要可以拉伸它填充尽可能多的空间 |
  | QSizePolicy::Maximum   | ShrinkFlag                         | 窗口部件的sizeHint()是它的最大大小，如有必要可以收缩它空出尽可能多的空间 |
  | QSizePolicy::Preferred | GrowFlag \| ShrinkFlag             | 窗口部件的sizeHint()是它的合适大小，如有必要可以拉伸或收缩它 |
  | QSizePolicy::Expanding | GrowFlag \|ShrinkFlag \|ExpandFlag | 可以拉伸或压缩该窗口部件，并希望它能变长变高                 |
  | QSizePolicy::Fixed     |                                    |                                                              |
  | QSizePolicy::Fixed     |                                    |                                                              |

## 2.Public Functions

- QSizePolicy ()

- QSizePolicy ( Policy horizontal, Policy vertical )

- QSizePolicy ( Policy horizontal, Policy vertical, ControlType type )

- ControlType	controlType () const

- Qt::Orientations	expandingDirections () const

  返回小部件是否可以使用比QWidget :: sizeHint（）函数指示的更多的空间。

  Qt :: Horizontal或Qt :: Vertical的值表示窗口小部件可以水平或垂直增长（即，水平或垂直策略是Expanding或MinimumExpanding），而Qt :: Horizontal | Qt :: Vertical表示它可以在两个维度上增长。

- bool	hasHeightForWidth () const

  如果小部件的首选高度取决于其宽度，则返回true； 否则返回false。

- bool	hasWidthForHeight () const

- Policy	horizontalPolicy () const

  返回大小策略的水平分量。

- int	horizontalStretch () const

  返回大小策略的水平拉伸因子。

- void	transpose ()

  交换水平和垂直策略并延伸。

- operator QVariant () const

  返回存储此QSizePolicy的QVariant。

- void	setControlType ( ControlType type )

- void	setHeightForWidth ( bool dependent )

- void	setHorizontalPolicy ( Policy policy )

- void	setHorizontalStretch ( uchar stretchFactor )

- void	setVerticalPolicy ( Policy policy )

- void	setVerticalStretch ( uchar stretchFactor )

- void	setWidthForHeight ( bool dependent )

- Policy	verticalPolicy () const

- int	verticalStretch () const

- bool	operator!= ( const QSizePolicy & other ) const

- bool	operator== ( const QSizePolicy & other ) const

## 3.Related Non-Members

- QDataStream &	operator<< ( QDataStream & stream, const QSizePolicy & policy )
- QDataStream &	operator>> ( QDataStream & stream, QSizePolicy & policy )

## 4.Detailed Description

QSizePolicy类是一个布局属性，描述了水平和垂直大小调整策略。

小部件的大小策略是其以各种方式调整大小的意愿的表达，并且影响布局引擎如何处理小部件。每个小部件都返回一个QSizePolicy，描述其布局时首选的水平和垂直大小调整策略。您可以通过更改其QWidget :: sizePolicy属性来为特定的窗口小部件更改此设置。

QSizePolicy包含两个独立的QSizePolicy :: Policy值和两个拉伸因子；一个描述小部件的水平尺寸策略，另一个描述小部件的垂直尺寸策略。它还包含一个标志，用于指示其首选大小的高度和宽度是否相关。

可以在构造函数中设置水平和垂直策略，并使用setHorizontalPolicy（）和setVerticalPolicy（）函数进行更改。可以使用setHorizontalStretch（）和setVerticalStretch（）函数来设置拉伸因子。可以使用setHeightForWidth（）函数来设置指示窗口小部件的sizeHint（）是否取决于宽度的标志（例如，菜单栏或自动换行标签）。

当前的大小策略和拉伸因子可以使用horizontalPolicy（），verticalPolicy（），horizontalStretch（）和verticalStretch（）函数进行检索。或者，使用transpose（）函数交换水平和垂直策略和拉伸。 hasHeightForWidth（）函数返回指示大小提示依赖项的标志的当前状态。

使用expandingDirections（）函数来确定关联的窗口小部件是否可以使用比其sizeHint（）函数所指示的更多的空间，以及找出可以向哪个方向扩展。

最后，QSizePolicy类为操作员提供了将此大小策略与给定策略进行比较的方法，以及为该QSizePolicy存储为QVariant对象的QVariant操作员。