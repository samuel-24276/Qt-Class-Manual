# QObject

注意：此类中的所有函数都是可重入的。
注意：这些函数也是**线程安全**的：

- `connect(const QObject *sender, const char *signal, const QObject *receiver, const char *method, Qt::ConnectionType type)`
- `connect(const QObject *sender, const char *signal, const char *method, Qt::ConnectionType type) const`
- `connect(const QObject *sender, PointerToMemberFunction signal, const QObject *receiver, PointerToMemberFunction method, Qt::ConnectionType type)`
- `connect(const QObject *sender, PointerToMemberFunction signal, Functor functor)`
- `connect(const QObject *sender, PointerToMemberFunction signal, const QObject *context, Functor functor, Qt::ConnectionType type)`
- `disconnect(const QObject *sender, const char *signal, const QObject *receiver, const char *method)`
- `disconnect(const char *signal, const QObject *receiver, const char *method) const`
- `disconnect(const QObject *sender, PointerToMemberFunction signal, const QObject *receiver, PointerToMemberFunction method)`
- `deleteLater() `

## 1.Properties

- `objectName : QString `——对象的名字

## 2.Public Functions

- QObject(QObject *parent = nullptr)
- virtual ~QObject()
- bool blockSignals(bool block)
- const QObjectList &children() const
- QMetaObject::Connection connect(const QObject *sender, const char *signal, const char *method, Qt::ConnectionType type = Qt::AutoConnection) const
- bool disconnect(const char *signal = nullptr, const QObject *receiver = nullptr, const char *method = nullptr) const
- bool disconnect(const QObject *receiver, const char *method = nullptr) const
- void dumpObjectInfo() const
- void dumpObjectTree() const
- QList<QByteArray> dynamicPropertyNames() const
- virtual bool event(QEvent *e)
- virtual bool eventFilter(QObject *watched, QEvent *event)
- T findChild(const QString &name = QString(), Qt::FindChildOptions options = Qt::FindChildrenRecursively) const
- QList<T> findChildren(const QString &name = QString(), Qt::FindChildOptions options = Qt::FindChildrenRecursively) const
- QList<T> findChildren(const QRegularExpression &re, Qt::FindChildOptions options = Qt::FindChildrenRecursively) const
- bool inherits(const char *className) const
- void installEventFilter(QObject *filterObj)
- bool isWidgetType() const
- bool isWindowType() const
- void killTimer(int id)
- virtual const QMetaObject *metaObject() const
- void moveToThread(QThread *targetThread)
- QString objectName() const
- QObject *parent() const
- QVariant property(const char *name) const
- void removeEventFilter(QObject *obj)
- void setObjectName(const QString &name)
- void setParent(QObject *parent)
- bool setProperty(const char *name, const QVariant &value)
- bool signalsBlocked() const
- int startTimer(int interval, Qt::TimerType timerType = Qt::CoarseTimer)
- int startTimer(std::chrono::milliseconds time, Qt::TimerType timerType = Qt::CoarseTimer)
- QThread *thread() const

## 3.Public Slots

- void deleteLater()

## 4.Signals

- void destroyed(QObject *obj = nullptr)
- void objectNameChanged(const QString &objectName)

## 5.Static Public Members

- QMetaObject::Connection connect(const QObject *sender, const char *signal, const QObject *receiver, const char *method, Qt::ConnectionType type = Qt::AutoConnection)

- QMetaObject::Connection connect(const QObject *sender, const QMetaMethod &signal, const QObject *receiver, const QMetaMethod &method, Qt::ConnectionType type = Qt::AutoConnection)

- QMetaObject::Connection connect(const QObject *sender, PointerToMemberFunction signal, const QObject *receiver, PointerToMemberFunction method, Qt::ConnectionType type = Qt::AutoConnection)

- QMetaObject::Connection connect(const QObject *sender, PointerToMemberFunction signal, Functor functor)

- QMetaObject::Connection connect(const QObject *sender, PointerToMemberFunction signal, const QObject *context, Functor functor, Qt::ConnectionType type = Qt::AutoConnection)

- bool disconnect(const QObject *sender, const char *signal, const QObject *receiver, const char *method)

- bool disconnect(const QObject *sender, const QMetaMethod &signal, const QObject *receiver, const QMetaMethod &method)

- bool disconnect(const QMetaObject::Connection &connection)

- bool disconnect(const QObject *sender, PointerToMemberFunction signal, const QObject *receiver, PointerToMemberFunction method)

- const QMetaObject staticMetaObject

- QString tr(const char *sourceText, const char *disambiguation = nullptr, int n = -1)

  返回源文本的翻译版本，可以选择基于歧义消除字符串和包含复数的字符串的n值； 否则，如果没有合适的翻译字符串，则返回QString :: fromUtf8（sourceText）。

  **警告**：仅当在调用此方法之前安装了所有转换器时，该方法才可重入。 不支持在执行翻译时安装或删除翻译器。 这样做可能会导致崩溃或其他不良行为。

## 6.Protected Functions

- virtual void childEvent(QChildEvent *event)
- virtual void connectNotify(const QMetaMethod &signal)
- virtual void customEvent(QEvent *event)
- virtual void disconnectNotify(const QMetaMethod &signal)
- bool isSignalConnected(const QMetaMethod &signal) const
- int receivers(const char *signal) const
- QObject *sender() const
- int senderSignalIndex() const
- virtual void timerEvent(QTimerEvent *event)

## 7.Related Non-Members

- typedef QObjectList
- QList<T> qFindChildren(const QObject *obj, const QRegExp &regExp)
- T qobject_cast(QObject *object)
- T qobject_cast(const QObject *object)

## 8.Macros

- QT_NO_NARROWING_CONVERSIONS_IN_CONNECT

- **Q_CLASSINFO(Name, Value)**

  该宏**将额外的信息与该类相关联**，可使用`QObject :: metaObject（）`获得该信息。 Qt仅在Active Qt，Qt D-Bus和Qt QML中有限地使用此功能。
  额外信息采用名称字符串和值文字字符串的形式。

  ```c++
   class MyClass : public QObject
   {
       Q_OBJECT
       Q_CLASSINFO("Author", "Pierre Gendron")
       Q_CLASSINFO("URL", "http://www.my-organization.qc.ca")
  
   public:
       ...
   };
  ```

- Q_DISABLE_COPY(Class)

- Q_DISABLE_COPY_MOVE(Class)

- Q_DISABLE_MOVE(Class)

- Q_EMIT

  当您想将Qt Signals and Slots与第3方信号/插槽机制一起使用时，请使用此宏来替换generate关键字来发出信号。
  通常在.pro文件中使用CONFIG变量指定no_keywords时使用该宏，但是即使未指定no_keywords时也可以使用该宏。

- **Q_ENUM(...)**

  该宏**向元对象系统*注册*一个枚举类型**。 必须将其放在具有Q_OBJECT或Q_GADGET宏的类中的枚举声明之后。 对于命名空间，请改用Q_ENUM_NS（）。

  ```c++
   class MyClass : public QObject
   {
       Q_OBJECT
  
   public:
       MyClass(QObject *parent = nullptr);
       ~MyClass();
  
       enum Priority { High, Low, VeryHigh, VeryLow };
       Q_ENUM(Priority)
       void setPriority(Priority priority);
       Priority priority() const;
   };
  ```

  用`Q_ENUM`声明的枚举在封闭的`QMetaObject`中注册了其`QMetaEnum`。 您也可以使用`QMetaEnum :: fromType（）`获得`QMetaEnum`。
  **已注册的枚举也会自动注册到Qt元类型系统**，从而使它们成为QMetaType已知的，而无需使用**Q_DECLARE_METATYPE（）**。 这将启用有用的功能； 例如，如果在QVariant中使用，则可以将它们转换为字符串。 同样，将它们传递给QDebug将打印出它们的名称。
  请注意，枚举值作为带符号的int存储在元对象系统中。 使用对int有效的值范围之外的值注册枚举将导致通过元对象系统访问它们时发生溢出和潜在的未定义行为。 例如，QML确实通过元对象系统访问注册的枚举。

- Q_ENUM_NS(...)

- Q_FLAG(...)

- Q_FLAG_NS(...)

- Q_GADGET

  Q_GADGET宏是Q_OBJECT宏的简化版本，**用于不从QObject继承但仍要使用QMetaObject提供的某些反射功能的类**。 就像Q_OBJECT宏一样，它**必须出现在类定义的私有部分中**。
  Q_GADGET可以具有Q_ENUM，Q_PROPERTY和Q_INVOKABLE，但是它们**不能具有信号或插槽**。
  Q_GADGET使类成员staticMetaObject可用。 staticMetaObject类型为QMetaObject，并提供对使用Q_ENUMS声明的枚举的访问。

- Q_INTERFACES(...)

  这个宏告诉Qt类实现了哪些接口。 **在实现插件时使用**。

  

  ```c++
   class BasicToolsPlugin : public QObject,
                            public BrushInterface,
                            public ShapeInterface,
                            public FilterInterface
   {
       Q_OBJECT
       Q_PLUGIN_METADATA(IID "org.qt-project.Qt.Examples.PlugAndPaint.BrushInterface" FILE "basictools.json")
       Q_INTERFACES(BrushInterface ShapeInterface FilterInterface)
  
   public:
       ...
   };
  ```

- Q_INVOKABLE

  **将此宏应用于成员函数的声明，以允许它们通过元对象系统被调用**。 宏将在返回类型之前写入，如以下示例所示：

  ```c++
   class Window : public QWidget
   {
       Q_OBJECT
  
   public:
       Window();
       void normalMethod();
       Q_INVOKABLE void invokableMethod();
   };
  ```

  使用Q_INVOKABLE标记了`invokableMethod（）`函数，从而使其在元对象系统中**注册**，并允许使用`QMetaObject :: invokeMethod（）`对其进行调用。 由于`normalMethod（）`函数没有以这种方式注册，因此无法使用`QMetaObject :: invokeMethod（）`来调用它。
  如果可调用成员函数返回指向QObject或QObject的子类的指针并从QML调用，则适用特殊的所有权规则。 有关更多信息，请参见QML和C ++之间的数据类型转换。

- `Q_NAMESPACE`

  `Q_NAMESPACE`宏可用于将`QMetaObject`功能添加到名称空间。
  `Q_NAMESPACE`可以具有`Q_CLASSINFO`，`Q_ENUM_NS`，Q_FLAG_NS，但不能具有`Q_ENUM`，Q_FLAG，Q_PROPERTY，Q_INVOKABLE，信号或插槽。
  `Q_NAMESPACE`使外部变量`staticMetaObject`可用。 `staticMetaObject`类型为`QMetaObject`，并提供对使用`Q_ENUM_NS `/ Q_FLAG_NS声明的枚举的访问。

- Q_NAMESPACE_EXPORT(EXPORT_MACRO)

  Q_NAMESPACE_EXPORT宏可用于**将QMetaObject功能添加到名称空间**。
  它的工作原理与Q_NAMESPACE宏完全相同。 但是，使用提供的EXPORT_MACRO限定符声明在名称空间中定义的外部staticMetaObject变量。 如果需要从动态库中导出对象，这很有用。

  ```c++
    namespace test {
   Q_NAMESPACE_EXPORT(EXPORT_MACRO)
   ...
  ```

- ***Q_OBJECT***

  Q_OBJECT宏**必须出现在类定义的私有部分中**，该类声明其自身的信号和插槽，或者使用Qt的元对象系统提供的其他服务。

  注意：**此宏要求该类是QObject的子类**。 使用Q_GADGET而不是Q_OBJECT来启用元对象系统对不是QObject子类的类中的枚举的支持。

- Q_PROPERTY(...)

  此宏**用于在继承QObject的类中声明属性**。 属性的行为类似于类数据成员，但是它们**具有可通过元对象系统访问的其他功能**。

  ```c++
  Q_PROPERTY(type name
              (READ getFunction [WRITE setFunction] |
               MEMBER memberName [(READ getFunction | WRITE setFunction)])
              [RESET resetFunction]
              [NOTIFY notifySignal]
              [REVISION int]
              [DESIGNABLE bool]
              [SCRIPTABLE bool]
              [STORED bool]
              [USER bool]
              [CONSTANT]
              [FINAL])
              [REQUIRED]
  ```

  属性名称和类型以及READ函数是必需的。 该类型可以是QVariant支持的任何类型，也可以是用户定义的类型。 其他项目是可选的，但是WRITE功能是常见的。 除USER（默认为false）外，这些属性默认为true。

- Q_REVISION

- Q_SET_OBJECT_NAME(Object)

- Q_SIGNAL

- Q_SIGNALS

- Q_SLOT

- Q_SLOTS

## 9.Detailed Description

