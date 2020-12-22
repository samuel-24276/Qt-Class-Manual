# QDialogButtonBox

继承关系：`QDialogButtonBox`->`QWidget`->`QObject`and `QPaintDevice`

## 1.Public Types

- enum	ButtonLayout { WinLayout, MacLayout, KdeLayout, GnomeLayout }

  此枚举描述在排列按钮框中包含的按钮时要使用的布局策略。

  | Constant                      | Value | Description                      |
  | ----------------------------- | ----- | -------------------------------- |
  | QDialogButtonBox::WinLayout   | 0     | 使用适合Windows应用程序的策略。  |
  | QDialogButtonBox::MacLayout   | 1     | 使用适合Mac OS X应用程序的策略。 |
  | QDialogButtonBox::KdeLayout   | 2     | 使用适合KDE应用程序的策略。      |
  | QDialogButtonBox::GnomeLayout | 3     | 使用适合GNOME应用程序的策略。    |

  按钮布局是由当前样式指定的。但是，在X11平台上，它可能受到桌面环境的影响。

- enum	ButtonRole { InvalidRole, AcceptRole, RejectRole, DestructiveRole, ..., ResetRole }

  此枚举描述可用于描述按钮框中的按钮的角色。这些角色的组合就像旗帜一样，用来描述他们行为的不同方面。

  | Constant                              | Value | Description                                                  |
  | ------------------------------------- | ----- | ------------------------------------------------------------ |
  | QDialogButtonBox::InvalidRole         | -1    | 无效按钮                                                     |
  | QDialogButtonBox::AcceptRole          | 0     | 点击按钮，对话框将被接受(例如OK)。                           |
  | QDialogButtonBox::RejectRole          | 1     | 点击按钮，对话框将被拒绝(例如Cancel)。                       |
  | QDialogButtonBox::**DestructiveRole** | 2     | 单击按钮会导致**破坏性的更改**(例如放弃更改)，并关闭对话框。 |
  | QDialogButtonBox::ActionRole          | 3     | 单击该按钮会改变对话框内的元素。                             |
  | QDialogButtonBox::HelpRole            | 4     | 可以点击该按钮请求帮助。                                     |
  | QDialogButtonBox::YesRole             | 5     | 按钮是一个“Yes”类按钮。                                      |
  | QDialogButtonBox::NoRole              | 6     | 按钮是一个“No”类按钮。                                       |
  | QDialogButtonBox::ApplyRole           | 8     | 该按钮应用当前更改。                                         |
  | QDialogButtonBox::ResetRole           | 7     | 该按钮将对话框的字段重置为默认值。                           |

- enum	StandardButton { Ok, Open, Save, Cancel, ..., NoButton }
  flags	StandardButtons

  这些枚举描述标准按钮的标志。每个按钮都有一个定义好的ButtonRole。

  | Constant                          | Value | Description                                                  |
  | --------------------------------- | ----- | ------------------------------------------------------------ |
  | QDialogButtonBox::Ok              |       | AcceptRole.                                                  |
  | QDialogButtonBox::Open            |       | AcceptRole.                                                  |
  | QDialogButtonBox::Save            |       | AcceptRole.                                                  |
  | QDialogButtonBox::SaveAll         |       | AcceptRole.                                                  |
  | QDialogButtonBox::Retry           |       | AcceptRole.                                                  |
  | QDialogButtonBox::Ignore          |       | AcceptRole.                                                  |
  | QDialogButtonBox::Cancel          |       | RejectRole                                                   |
  | QDialogButtonBox::Close           |       | RejectRole                                                   |
  | QDialogButtonBox::Abort           |       | RejectRole                                                   |
  | QDialogButtonBox::Discard         |       | A "Discard" or "Don't Save" button, depending on the platform, defined with the DestructiveRole. |
  | QDialogButtonBox::Apply           |       | ApplyRole.                                                   |
  | QDialogButtonBox::Reset           |       | ResetRole.                                                   |
  | QDialogButtonBox::RestoreDefaults |       | ResetRole.                                                   |
  | QDialogButtonBox::Help            |       | HelpRole.                                                    |
  | QDialogButtonBox::Yes             |       | YesRole.                                                     |
  | QDialogButtonBox::YesToAll        |       | YesRole.                                                     |
  | QDialogButtonBox::No              |       | NoRole.                                                      |
  | QDialogButtonBox::NoToAll         |       | NoRole.                                                      |
  | QDialogButtonBox::NoButton        |       | An invalid button.                                           |

## 2.Properties

- centerButtons : bool

  此属性用于保存按钮框中的按钮是否居中。

  默认情况下，该属性为false。这种行为适用于大多数类型的对话框。一个明显的例外是大多数平台(如Windows)上的消息框，按钮框水平居中。

- orientation : Qt::Orientation

  此属性保存按钮框的方向。

  默认情况下，方向是水平的(即按钮并排放置)。可能的方向是Qt::Horizontal和Qt::Vertical。

- standardButtons : StandardButtons

  此属性在按钮框中保存标准按钮的集合。

  此属性**控制按钮框使用哪些标准按钮**。

## 3.Public Functions

- QDialogButtonBox ( QWidget * parent = 0 )

- QDialogButtonBox ( Qt::Orientation orientation, QWidget * parent = 0 )

- QDialogButtonBox ( StandardButtons buttons, Qt::Orientation orientation = Qt::Horizontal, QWidget * parent = 0 )

- ~QDialogButtonBox ()

- void	addButton ( QAbstractButton * button, ButtonRole role )

  将给定按钮添加到具有指定角色的按钮框中。如果角色无效，则不添加按钮。

  如果已经添加了按钮，则将删除它，并使用新角色再次添加它。

  注意:按钮框拥有按钮的所有权。

- QPushButton *	addButton ( const QString & text, ButtonRole role )

  使用给定文本创建一个按钮，将其添加到指定角色的按钮框中，并返回相应的按钮。如果角色无效，则不会创建任何按钮，并且返回零。

- QPushButton *	addButton ( StandardButton button )

  如果这样做是有效的，将一个标准按钮添加到按钮框中，并返回一个按钮。如果button无效，则不会将其添加到按钮框中，并返回0。

- void	removeButton ( QAbstractButton * button )

  从按钮框中移除按钮而不删除它，并将其父节点设置为零。

- QPushButton *	button ( StandardButton which ) const

  返回与标准按钮对应的QPushButton，如果标准按钮在此按钮框中不存在，则返回0。

- ButtonRole	buttonRole ( QAbstractButton * button ) const

  返回指定按钮的按钮角色。这个函数返回InvalidRole，如果按钮为0或没有被添加到按钮框中。

- QList<QAbstractButton *>	buttons () const

  返回已添加到按钮框的所有按钮的列表。

- bool	centerButtons () const

- void	clear ()

  清除按钮框，删除其中的所有按钮。

- Qt::Orientation	orientation () const

- void	setCenterButtons ( bool center )

- void	setOrientation ( Qt::Orientation orientation )

- void	setStandardButtons ( StandardButtons buttons )

- StandardButton	standardButton ( QAbstractButton * button ) const

- StandardButtons	standardButtons () const

## 4.Signals

- void	accepted ()

  当单击按钮框内的按钮时，就会发出这个信号，只要它是用AcceptRole或YesRole定义的。

- void	clicked ( QAbstractButton * button )

  当单击按钮框内的按钮时，会发出此信号。按下的特定按钮由button 指定。

- void	helpRequested ()

  当单击按钮框中的按钮时，就会发出这个信号，只要它是用HelpRole定义的。

- void	rejected ()

  当单击按钮框内的按钮时，就会发出这个信号，只要它是用RejectRole或NoRole定义的。

## 5.Detailed Description

QDialogButtonBox类是一个小部件，它以适合于当前小部件样式的布局显示按钮。

对话框和消息框通常以符合该平台的界面指导原则的布局显示按钮。不同平台的对话框总是有不同的布局。QDialogButtonBox允许开发人员添加按钮，并将自动为用户的桌面环境使用适当的布局。

对话框的大多数按钮都遵循特定的角色。这样的角色包括:

- 接受或拒绝对话。
- 寻求帮助。
- 对对话框本身执行操作(例如重置字段或应用更改)。

还可以用其他方法来消除可能导致破坏性结果的对话框。

大多数对话框都有可以被认为是标准的按钮(例如OK和取消按钮)。有时以标准的方式创建这些按钮是很方便的。

有几种使用QDialogButtonBox的方法。一种方法是自己创建按钮(或按钮文本)，并将它们添加到按钮框中，指定它们的角色。

```c++
findButton = new QPushButton(tr("&Find"));
findButton->setDefault(true);
moreButton = new QPushButton(tr("&More"));
moreButton->setCheckable(true);
moreButton->setAutoDefault(false);

buttonBox = new QDialogButtonBox(Qt::Vertical);
buttonBox->addButton(findButton, QDialogButtonBox::ActionRole);
buttonBox->addButton(moreButton, QDialogButtonBox::ActionRole);
```
另外，QDialogButtonBox提供了几个标准的按钮(例如:OK，取消，保存)，你可以使用。它们作为标志存在，因此您可以在构造函数中同时使用它们。

```c++
buttonBox = new QDialogButtonBox(QDialogButtonBox::Ok
| QDialogButtonBox::Cancel);

connect(buttonBox, SIGNAL(accepted()), this, SLOT(accept()));
connect(buttonBox, SIGNAL(rejected()), this, SLOT(reject()));
```

您可以混合和匹配普通按钮和标准按钮。

目前，如果按钮框是水平的，按钮的布局如下:

当按钮在按钮框中被单击时，clicked()信号会因被按下的实际按钮而发出。为了方便起见，如果按钮有AcceptRole、RejectRole或HelpRole，则分别发出accepted()、rejected()或helpRequested()信号。

如果你想要一个特定的按钮是默认的，你需要自己调用QPushButton::setDefault()。然而，当使用QPushButton::autoDefault属性时，如果没有默认按钮设置并且为了保留哪个按钮是跨平台的默认按钮，当QDialogButtonBox显示时，第一个具有accept角色的按钮将成为默认按钮.