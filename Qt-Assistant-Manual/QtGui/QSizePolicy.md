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

  