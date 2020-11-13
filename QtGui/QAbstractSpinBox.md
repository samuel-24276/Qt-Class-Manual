# QAbstractSpinBox

## 1.Public Types

- enum ButtonSymbols { UpDownArrows, PlusMinus, NoButtons }
- enum CorrectionMode { CorrectToPreviousValue, CorrectToNearestValue }
- flags StepEnabled
- enum StepEnabledFlag { StepNone, StepUpEnabled, StepDownEnabled }
- enum StepType { DefaultStepType, AdaptiveDecimalStepType }

## 2.Properties

- accelerated : bool
- acceptableInput : const bool
- alignment : Qt::Alignment
- buttonSymbols : ButtonSymbols
- correctionMode : CorrectionMode
- frame : bool
- keyboardTracking : bool
- readOnly : bool
- showGroupSeparator : bool
- specialValueText : QString
- text : const QString
- wrapping : bool

## 3.Public Functions

- QAbstractSpinBox(QWidget *parent = nullptr)
- virtual ~QAbstractSpinBox()
- Qt::Alignment alignment() const
- QAbstractSpinBox::ButtonSymbols buttonSymbols() const
- QAbstractSpinBox::CorrectionMode correctionMode() const
- virtual void fixup(QString &input) const
- bool hasAcceptableInput() const
- bool hasFrame() const
- void interpretText()
- bool isAccelerated() const
- bool isGroupSeparatorShown() const
- bool isReadOnly() const
- bool keyboardTracking() const
- void setAccelerated(bool on)
- void setAlignment(Qt::Alignment flag)
- void setButtonSymbols(QAbstractSpinBox::ButtonSymbols bs)
- void setCorrectionMode(QAbstractSpinBox::CorrectionMode cm)
- void setFrame(bool)
- void setGroupSeparatorShown(bool shown)
- void setKeyboardTracking(bool kt)
- void setReadOnly(bool r)
- void setSpecialValueText(const QString &txt)
- void setWrapping(bool w)
- QString specialValueText() const
- virtual void stepBy(int steps)
- QString text() const
- virtual QValidator::State validate(QString &input, int &pos) const
- bool wrapping() const

## 4.Reimplemented Public Functions

- virtual bool event(QEvent *event) override
- virtual QVariant inputMethodQuery(Qt::InputMethodQuery query) const override
- virtual QSize minimumSizeHint() const override
- virtual QSize sizeHint() const override

## 5.Public Slots

- virtual void clear()
- void selectAll()
- void stepDown()
- void stepUp()

## 6.Signals

- void editingFinished()

## 7.Protected Functions

- void initStyleOption(QStyleOptionSpinBox *option) const
- QLineEdit *lineEdit() const
- void setLineEdit(QLineEdit *lineEdit)
- virtual QAbstractSpinBox::StepEnabled stepEnabled() const

## 8.Reimplemented Protected Functions

- virtual void changeEvent(QEvent *event) override
- virtual void closeEvent(QCloseEvent *event) override
- virtual void contextMenuEvent(QContextMenuEvent *event) override
- virtual void focusInEvent(QFocusEvent *event) override
- virtual void focusOutEvent(QFocusEvent *event) override
- virtual void hideEvent(QHideEvent *event) override
- virtual void keyPressEvent(QKeyEvent *event) override
- virtual void keyReleaseEvent(QKeyEvent *event) override
- virtual void mouseMoveEvent(QMouseEvent *event) override
- virtual void mousePressEvent(QMouseEvent *event) override
- virtual void mouseReleaseEvent(QMouseEvent *event) override
- virtual void paintEvent(QPaintEvent *event) override
- virtual void resizeEvent(QResizeEvent *event) override
- virtual void showEvent(QShowEvent *event) override
- virtual void timerEvent(QTimerEvent *event) override
- virtual void wheelEvent(QWheelEvent *event) override