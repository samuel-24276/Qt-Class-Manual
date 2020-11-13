# QSpinBox

继承关系：`QSpinBox`->`QAbstractSpinBox`->`QWidget`

**注意**：**QSpinBox和QDoubleSpinBox只能用于[1,100)内的数字，大于等于100的数字无法表示**。

## 1.Properties

- cleanText : const QString

  此属性保存SpinBox的文本，但不包括任何前缀，后缀，前导或尾随空白。

- displayIntegerBase : int

  此属性保存用于显示SpinBox的基础值，默认的displayIntegerBase值为10。

- maximum : int

  此属性保存SpinBox的最大值。

  设置此属性时，如有必要，将调整最小值，以确保范围保持有效。
  默认最大值为99。

- minimum : int

  此属性保存SpinBox的最小值。
  设置此属性时，如有必要，将调整最大值，以确保范围保持有效。
  默认最小值为0。

- **prefix : QString**

  此属性保存SpinBox的前缀。
  前缀位于显示值的开头。 典型用途是显示度量单位或货币符号。 例如：
    `sb-> setPrefix（“ $”）;`
  要关闭前缀显示，请将此属性设置为空字符串。 **默认为无前缀**。 设置value（）== minimum（）和specialValueText（）时，不显示前缀。
  如果未设置前缀，则prefix（）返回一个空字符串。

- **suffix : QString**

  此属性保存SpinBox的后缀。
  后缀将附加到显示值的末尾。 典型用途是显示度量单位或货币符号。 例如：
    sb-> setSuffix（“ km”）;
  要关闭后缀显示，请将此属性设置为空字符串。 缺省值为无后缀。 如果设置了specialValueText（），则不显示minimum（）的后缀。
  如果未设置后缀，则suffix（）返回一个空字符串。

- singleStep : int

  该属性保存步长值。
  当用户使用箭头更改微调框的值时，该值将增加或减少singleStep的数量。 默认值为1。将singleStep值设置为小于0不会执行任何操作。

- stepType : StepType

  此属性保存步骤类型。
  步长类型可以是单步或自适应十进制步长。

- value : int

  此属性保存SpinBox的值
  如果新值与旧值不同，则setValue（）将发出valueChanged（）。 value属性具有第二个通知程序信号，其中包括SpinBox的前缀和后缀。

## 2.Public Functions

- QSpinBox(QWidget *parent = nullptr)
- virtual ~QSpinBox()
- QString cleanText() const
- int displayIntegerBase() const
- int maximum() const
- int minimum() const
- QString prefix() const
- QString suffix() const
- void setDisplayIntegerBase(int base)
- void setMaximum(int max)
- void setMinimum(int min)
- void setPrefix(const QString &prefix)
- void setRange(int minimum, int maximum)
- void setSingleStep(int val)
- void setStepType(QAbstractSpinBox::StepType stepType)
- void setSuffix(const QString &suffix)
- int singleStep() const
- QAbstractSpinBox::StepType stepType() const
- int value() const

## 3.Public Slots

- `void setValue(int val)`

## 4.Signals

- void textChanged(const QString &text)

  只要SpinBox的文本，就会发出此信号。 新文本以带有prefix（）和suffix（）的文本形式传递。

- void valueChanged(int i)

  每当更改SpinBox的值时，都会发出此信号。 新值的整数值在i中传递。
  注意：属性值的通知程序信号。
  注意：信号valueChanged在此类中已重载。 为了通过使用函数指针语法连接到该信号，Qt提供了一个方便的助手来获取函数指针，如以下示例所示：
    connect（spinBox，QOverload <int> :: of（＆QSpinBox :: valueChanged），
        [=]（int i）{/ * ... * /}）；

## 5.Protected Functions

- virtual QString textFromValue(int value) const

  每当需要显示给定值时，SpinBox就会使用此虚拟函数。 默认实现返回一个字符串，该字符串包含使用QWidget :: locale（）。toString（）以标准方式打印的值，但除非设置setGroupSeparatorShown（），否则将除去千位分隔符。 重新实现可能返回任何内容。 （请参阅详细说明中的示例。）
  注意：QSpinBox不会为specialValueText（）调用此函数，并且返回值中不应包含prefix（）和suffix（）。
  如果重新实现，则可能还需要重新实现valueFromText（）和validate（）。

- virtual int valueFromText(const QString &text) const

  每当需要将用户输入的文本解释为值时，SpinBox就会使用此虚拟函数。
  需要以非数字方式显示SpinBox值的子类需要重新实现此功能。
  注意：QSpinBox分别处理specialValueText（）； 此功能仅与其他值有关。

## 6.Reimplemented Protected Functions

- virtual bool event(QEvent *event) override
- virtual void fixup(QString &input) const override
- virtual QValidator::State validate(QString &text, int &pos) const override

# QDoubleSpinBox

继承关系：`QDoubleSpinBox`->`QAbstractSpinBox`->`QWidget`

**注意**：**QSpinBox和QDoubleSpinBox只能用于[1,100)内的数字，大于等于100的数字无法表示**。

## 1.Properties

比QSpinBox少一个`displayIntegerBase : int`，多一个

- decimals : int

  此属性保存QDoubleSpinBox的精度，以十进制表示
  设置旋转框用于显示和解释双精度数的小数位数。
  警告：由于double类型的限制，小数位数的最大值为DBL_MAX_10_EXP + DBL_DIG（即323）。
  注意：更改此属性后，最大值，最小值和值可能会更改。

## 2.Public Functions

- QDoubleSpinBox(QWidget *parent = nullptr)
- virtual ~QDoubleSpinBox()
- QString cleanText() const
- int decimals() const
- double maximum() const
- double minimum() const
- QString prefix() const
- void setDecimals(int prec)
- void setMaximum(double max)
- void setMinimum(double min)
- void setPrefix(const QString &prefix)
- void setRange(double minimum, double maximum)
- void setSingleStep(double val)
- void setStepType(QAbstractSpinBox::StepType stepType)
- void setSuffix(const QString &suffix)
- double singleStep() const
- QAbstractSpinBox::StepType stepType() const
- QString suffix() const
- virtual QString textFromValue(double value) const
- double value() const
- virtual double valueFromText(const QString &text) const

## 3.Reimplemented Public Functions

- virtual void fixup(QString &input) const override
- virtual QValidator::State validate(QString &text, int &pos) const override

## 4.Public Slots

- void setValue(double val)

## 5.Signals

- void textChanged(const QString &text)
- void valueChanged(double d)
