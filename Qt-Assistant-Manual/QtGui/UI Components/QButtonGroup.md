# QButtonGroup

继承关系：`QButtonGroup`->`QObject`

## 1.Properties

- exclusive : bool

  此属性用于判断按钮组是否是**独占**的。

  如果此属性为true，则在任何给定时间只能选中组中的一个按钮。用户可以单击任何按钮来检查它，该按钮将替换现有的按钮，作为组中已检查的按钮。

  **在独占组中，用户不能通过单击取消选中当前选中的按钮;相反，必须单击组中的另一个按钮，以设置该组的新选中按钮**。

  默认情况下，该属性为true。

## 2.Public Functions

- QButtonGroup ( QObject * parent = 0 )

- ~QButtonGroup ()

- void	addButton ( QAbstractButton * button )

  将给定按钮添加到组的内部按钮列表的末尾。一个id将被这个QButtonGroup分配给这个按钮。自动分配的id保证为负，从-2开始。如果您也要分配自己的id，请使用正值以避免冲突。

- void	addButton ( QAbstractButton * button, int id )

  使用给定的id将给定的按钮添加到按钮组中。建议只分配正的id。

- QAbstractButton *	button ( int id ) const

  返回具有指定id的按钮，如果不存在这样的按钮，则返回0。

- QList<QAbstractButton *>	buttons () const

  返回此组按钮的列表。这个可能是空的。

- QAbstractButton *	checkedButton () const

  返回按钮组的已选中按钮，如果没有选中按钮，则返回0。

- int	checkedId () const

  返回checkedButton()的id，如果没有选中按钮，则返回-1。

- bool	exclusive () const

- int	id ( QAbstractButton * button ) const

- void	removeButton ( QAbstractButton * button )

  从按钮组中移除给定的按钮。

- void	setExclusive ( bool )

- void	setId ( QAbstractButton * button, int id )

## 3.Signals

- void	buttonClicked ( QAbstractButton * button )
- void	buttonClicked ( int id )
- void	buttonPressed ( QAbstractButton * button )
- void	buttonPressed ( int id )
- void	buttonReleased ( QAbstractButton * button )
- void	buttonReleased ( int id )

## 4.Detailed Description

QButtonGroup类提供了一个容器来**组织按钮部件**组。

QButtonGroup提供了一个抽象容器，可以在其中放置按钮部件。它没有提供此容器的可视化表示(请参阅QGroupBox以了解容器小部件)，而是管理组中每个按钮的状态。

**独占按钮组关闭除被单击的按钮外的所有可选中(切换)按钮。默认情况下，按钮组是独占的**。按钮组中的按钮通常是可检查的QPushButton、qcheckbox(通常用于非排他的按钮组)或QRadioButtons。如果您创建了一个排他按钮组，您应该确保该组中的一个按钮最初被选中;否则，组最初将处于没有选中按钮的状态。

使用addButton()将一个按钮添加到组中。可以使用removeButton()将其从组中删除。如果组是排他的，则当前选中的按钮作为checkedButton()可用。如果单击了一个按钮，就会发出buttonClicked()信号。对于排他组中的可检查按钮，这意味着该按钮已被选中。组中的按钮列表由buttons()返回。

此外，QButtonGroup可以在整数和按钮之间进行映射。您可以使用setId()将一个整数id分配给一个按钮，并使用id()检索它。当前选中的按钮的id在checkedId()中可用，并且有一个重载的信号buttonClicked()发出按钮的id。id -1被QButtonGroup保留，表示“没有这样的按钮”。映射机制的目的是简化用户界面中枚举值的表示。