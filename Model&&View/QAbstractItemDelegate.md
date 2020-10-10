# QAbstractItemDelegate

继承关系：`QAbstractItemDelegate`->`QObject`

继承者：

- QItemDelegate
- QStyledItemDelegate

## 1.Public Types

`enum EndEditHint { NoHint, EditNextItem, EditPreviousItem, SubmitModelCache, RevertModelCache }`

### 2.Public Functions

- QAbstractItemDelegate(QObject *parent = nullptr)
- virtual ~QAbstractItemDelegate()
- virtual QWidget *createEditor(QWidget *parent, const QStyleOptionViewItem &option, const QModelIndex &index) const
- virtual void destroyEditor(QWidget *editor, const QModelIndex &index) const
- virtual bool editorEvent(QEvent *event, QAbstractItemModel *model, const QStyleOptionViewItem &option, const QModelIndex &index)
- virtual bool helpEvent(QHelpEvent *event, QAbstractItemView *view, const QStyleOptionViewItem &option, const QModelIndex &index)
- virtual void paint(QPainter *painter, const QStyleOptionViewItem &option, const QModelIndex &index) const = 0
- virtual void setEditorData(QWidget *editor, const QModelIndex &index) const
- virtual void setModelData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const
- virtual QSize sizeHint(const QStyleOptionViewItem &option, const QModelIndex &index) const = 0
- virtual void updateEditorGeometry(QWidget *editor, const QStyleOptionViewItem &option, const QModelIndex &index) const

## 3.Signals

- void closeEditor(QWidget *editor, QAbstractItemDelegate::EndEditHint hint = NoHint)
- void commitData(QWidget *editor)
- void sizeHintChanged(const QModelIndex &index)

## 4.Detailed Description

