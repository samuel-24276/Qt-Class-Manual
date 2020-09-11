# QVariant

# 1.Public Functions

- QVariant(QVariant &&other)

- QVariant(const QPersistentModelIndex &val)

- QVariant(const QModelIndex &val)

- QVariant(const QJsonDocument &val)

- QVariant(const QJsonArray &val)

- QVariant(const QJsonObject &val)

- QVariant(const QJsonValue &val)

- QVariant(const QUrl &val)

- QVariant(const QUuid &val)

- QVariant(const QEasingCurve &val)

- QVariant(const QRegularExpression &re)

- QVariant(const QRegExp &regExp)

- QVariant(const QLocale &l)

- QVariant(const QRectF &val)

- QVariant(const QRect &val)

- QVariant(const QLineF &val)

- QVariant(const QLine &val)

- QVariant(const QPointF &val)

- QVariant(const QPoint &val)

- QVariant(const QSizeF &val)

- QVariant(const QSize &val)

- QVariant(const QHash<QString, QVariant> &val)

- QVariant(const QMap<QString, QVariant> &val)

- QVariant(const QList<QVariant> &val)

- QVariant(const QDateTime &val)

- QVariant(const QTime &val)

- QVariant(const QDate &val)

- QVariant(QChar c)

- QVariant(const QStringList &val)

- QVariant(QLatin1String val)

- QVariant(const QString &val)

- QVariant(const QBitArray &val)

- QVariant(const QByteArray &val)

- QVariant(const char *val)

- QVariant(float val)

- QVariant(double val)

- QVariant(bool val)

- QVariant(qulonglong val)

- QVariant(qlonglong val)

- QVariant(uint val)

- QVariant(int val)

- QVariant(QDataStream &s)

- QVariant(const QVariant &p)

- QVariant(int typeId, const void *copy)

- QVariant(QVariant::Type type)

- QVariant()

- QVariant &operator=(QVariant &&other)

- QVariant &operator=(const QVariant &variant)

- ~QVariant()

  

- bool canConvert(int targetTypeId) const

  如果变量的类型可以转换为请求的类型targetTypeId，则返回true。 调用toInt（），toBool（）等方法时，此类转换会自动完成。
  以下强制转换是自动完成的：

  | Type                                                | Automatically Cast To                                        |
  | --------------------------------------------------- | ------------------------------------------------------------ |
  | QMetaType::Bool                                     | `QMetaType::QChar`，`QMetaType::Double`， `QMetaType::Int`，`QMetaType::LongLong`，`QMetaType::QString`，`QMetaType::UInt`，`QMetaType::ULongLong` |
  | [QMetaType::QByteArray](qmetatype.html#Type-enum)   | [QMetaType::Double](qmetatype.html#Type-enum), [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::LongLong](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum), [QMetaType::UInt](qmetatype.html#Type-enum), [QMetaType::ULongLong](qmetatype.html#Type-enum), [QMetaType::QUuid](qmetatype.html#Type-enum) |
  | [QMetaType::QChar](qmetatype.html#Type-enum)        | [QMetaType::Bool](qmetatype.html#Type-enum), [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::UInt](qmetatype.html#Type-enum), [QMetaType::LongLong](qmetatype.html#Type-enum), [QMetaType::ULongLong](qmetatype.html#Type-enum) |
  | [QMetaType::QColor](qmetatype.html#Type-enum)       | [QMetaType::QString](qmetatype.html#Type-enum)               |
  | [QMetaType::QDate](qmetatype.html#Type-enum)        | [QMetaType::QDateTime](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum) |
  | [QMetaType::QDateTime](qmetatype.html#Type-enum)    | [QMetaType::QDate](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum), [QMetaType::QTime](qmetatype.html#Type-enum) |
  | [QMetaType::Double](qmetatype.html#Type-enum)       | [QMetaType::Bool](qmetatype.html#Type-enum), [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::LongLong](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum), [QMetaType::UInt](qmetatype.html#Type-enum), [QMetaType::ULongLong](qmetatype.html#Type-enum) |
  | [QMetaType::QFont](qmetatype.html#Type-enum)        | [QMetaType::QString](qmetatype.html#Type-enum)               |
  | [QMetaType::Int](qmetatype.html#Type-enum)          | [QMetaType::Bool](qmetatype.html#Type-enum), [QMetaType::QChar](qmetatype.html#Type-enum), [QMetaType::Double](qmetatype.html#Type-enum), [QMetaType::LongLong](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum), [QMetaType::UInt](qmetatype.html#Type-enum), [QMetaType::ULongLong](qmetatype.html#Type-enum) |
  | [QMetaType::QKeySequence](qmetatype.html#Type-enum) | [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum) |
  | [QMetaType::QVariantList](qmetatype.html#Type-enum) | [QMetaType::QStringList](qmetatype.html#Type-enum) (if the list's items can be converted to QStrings) |
  | [QMetaType::LongLong](qmetatype.html#Type-enum)     | [QMetaType::Bool](qmetatype.html#Type-enum), [QMetaType::QByteArray](qmetatype.html#Type-enum), [QMetaType::QChar](qmetatype.html#Type-enum), [QMetaType::Double](qmetatype.html#Type-enum), [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum), [QMetaType::UInt](qmetatype.html#Type-enum), [QMetaType::ULongLong](qmetatype.html#Type-enum) |
  | [QMetaType::QPoint](qmetatype.html#Type-enum)       | [QMetaType::QPointF](qmetatype.html#Type-enum)               |
  | [QMetaType::QRect](qmetatype.html#Type-enum)        | [QMetaType::QRectF](qmetatype.html#Type-enum)                |
  | [QMetaType::QString](qmetatype.html#Type-enum)      | [QMetaType::Bool](qmetatype.html#Type-enum), [QMetaType::QByteArray](qmetatype.html#Type-enum), [QMetaType::QChar](qmetatype.html#Type-enum), [QMetaType::QColor](qmetatype.html#Type-enum), [QMetaType::QDate](qmetatype.html#Type-enum), [QMetaType::QDateTime](qmetatype.html#Type-enum), [QMetaType::Double](qmetatype.html#Type-enum), [QMetaType::QFont](qmetatype.html#Type-enum), [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::QKeySequence](qmetatype.html#Type-enum), [QMetaType::LongLong](qmetatype.html#Type-enum), [QMetaType::QStringList](qmetatype.html#Type-enum), [QMetaType::QTime](qmetatype.html#Type-enum), [QMetaType::UInt](qmetatype.html#Type-enum), [QMetaType::ULongLong](qmetatype.html#Type-enum), [QMetaType::QUuid](qmetatype.html#Type-enum) |
  | [QMetaType::QStringList](qmetatype.html#Type-enum)  | [QMetaType::QVariantList](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum) (if the list contains exactly one item) |
  | [QMetaType::QTime](qmetatype.html#Type-enum)        | [QMetaType::QString](qmetatype.html#Type-enum)               |
  | [QMetaType::UInt](qmetatype.html#Type-enum)         | [QMetaType::Bool](qmetatype.html#Type-enum), [QMetaType::QChar](qmetatype.html#Type-enum), [QMetaType::Double](qmetatype.html#Type-enum), [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::LongLong](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum), [QMetaType::ULongLong](qmetatype.html#Type-enum) |
  | [QMetaType::ULongLong](qmetatype.html#Type-enum)    | [QMetaType::Bool](qmetatype.html#Type-enum), [QMetaType::QChar](qmetatype.html#Type-enum), [QMetaType::Double](qmetatype.html#Type-enum), [QMetaType::Int](qmetatype.html#Type-enum), [QMetaType::LongLong](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum), [QMetaType::UInt](qmetatype.html#Type-enum) |
  | [QMetaType::QUuid](qmetatype.html#Type-enum)        | [QMetaType::QByteArray](qmetatype.html#Type-enum), [QMetaType::QString](qmetatype.html#Type-enum) |

- bool canConvert() const

  如果变量可以转换为模板类型T，则返回true，否则返回false。

  ```c++
  QVariant v = 42;
  
  v.canConvert<int>();              // returns true
  v.canConvert<QString>();          // returns true
  
  MyCustomStruct s;
  v.setValue(s);
  
  v.canConvert<int>();              // returns false
  v.canConvert<MyCustomStruct>();   // returns true
  ```

  如果对模板类型T的qobject_cast成功执行，则包含指向从QObject派生类型的指针的QVariant也将为此函数返回true。 请注意，这仅适用于使用Q_OBJECT宏的QObject子类。

- void clear()

- bool convert(int targetTypeId)

- bool isNull() const

- bool isValid() const

- void setValue(const T &value)

- void swap(QVariant &other)

- QBitArray toBitArray() const

- bool toBool() const

- QByteArray toByteArray() const

- QChar toChar() const

- QDate toDate() const

- QDateTime toDateTime() const

- double toDouble(bool *ok = nullptr) const

- QEasingCurve toEasingCurve() const

- float toFloat(bool *ok = nullptr) const

- QHash<QString, QVariant> toHash() const

- int toInt(bool *ok = nullptr) const

- QJsonArray toJsonArray() const

- QJsonDocument toJsonDocument() const

- QJsonObject toJsonObject() const

- QJsonValue toJsonValue() const

- QLine toLine() const

- QLineF toLineF() const

- QList<QVariant> toList() const

- QLocale toLocale() const

- qlonglong toLongLong(bool *ok = nullptr) const

- QMap<QString, QVariant> toMap() const

- QModelIndex toModelIndex() const

- QPersistentModelIndex toPersistentModelIndex() const

- QPoint toPoint() const

- QPointF toPointF() const

- qreal toReal(bool *ok = nullptr) const

- QRect toRect() const

- QRectF toRectF() const

- QRegExp toRegExp() const

- QRegularExpression toRegularExpression() const

- QSize toSize() const

- QSizeF toSizeF() const

- QString toString() const

- QStringList toStringList() const

- QTime toTime() const

- uint toUInt(bool *ok = nullptr) const

- qulonglong toULongLong(bool *ok = nullptr) const

- QUrl toUrl() const

- QUuid toUuid() const

- QVariant::Type type() const

- const char *typeName() const

- int userType() const

- T value() const

- bool operator!=(const QVariant &v) const

- bool operator==(const QVariant &v) const

# 2.Static Public Members

- `QVariant fromStdVariant(const std::variant<Types...> &value)`

  返回具有值的有效变体的类型和值的QVariant。 如果活动类型为std :: monostate，则返回默认的QVariant。
  注意：使用此方法，您不需要将变体注册为Qt元类型，因为std :: variant在存储之前就已解析。 但是，应该注册组件类型。

- **`QVariant fromValue(const T &value)`**

  返回包含值副本的QVariant。 否则，其行为与setValue（）完全相同。
  例：

  ```c++
  MyCustomStruct s;
  return QVariant::fromValue(s);
  ```

  注意：**如果要使用自定义类型，则应使用`Q_DECLARE_METATYPE（）`宏注册您的自定义类型**。

- `QVariant::Type nameToType(const char *name)`

  

- `const char *typeToName(int typeId)`

# 3.Related Non-Members

- `typedef QVariantHash`
- `typedef QVariantList`
- `typedef QVariantMap`
- `T qvariant_cast(const QVariant &value)`
- `bool operator!=(const QVariant &v1, const QVariant &v2)`
- `bool operator==(const QVariant &v1, const QVariant &v2)`

# 4.Detailed Description