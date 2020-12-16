# QMap

继承者：QMultiMap

## 1.Public Types

- class const_iterator
- class iterator
- class key_iterator
- typedef ConstIterator
- typedef Iterator
- typedef const_key_value_iterator
- typedef difference_type
- typedef key_type
- typedef key_value_iterator
- typedef mapped_type
- typedef size_type

## 2.Public Functions

### 2.1.增

- QMap::iterator insert(const Key &key, const T &value)

  插入带有键和值的新项目。
  **如果已经有一个带有键的项目，则该项目的值将替换为value**。
  如果按键有多个项目，则将最新插入的项目的值替换为value。

- QMap::iterator insert(QMap::const_iterator pos, const Key &key, const T &value)

  插入一个新项目，该项目具有键key和value值，并**带有提示pos，提示在何处进行插入**。
  如果将constBegin（）用作提示，则表明该键小于映射中的任何键，而constEnd（）建议该键（严格）大于映射中的任何键。否则，提示应满足条件（pos-1）.key（）<key <= pos.key（）。如果提示pos错误，则将其忽略并执行常规插入。
  如果已经有一个带有键的项目，则该项目的值将替换为value。
  如果有多个带有键的项目，则其中之一将被值替换。
  如果提示正确，并且map未共享，则插入将按摊销的固定时间执行。
  从排序后的数据创建映射时，首先使用constBegin（）插入最大的密钥比使用constEnd（）进行排序的顺序插入要快，因为constEnd（）-1（需要检查提示是否有效）需要对数时间。
  **注意**：请小心提示。从较旧的共享实例提供迭代器可能会崩溃，但是也有可能使映射和pos映射无提示损坏。

- void insert(const QMap<Key, T> &map)

  将Map中的所有项目插入此Map中。
  如果两个Map共用一个键，则其值将替换为存储在地图中的值。
  **注意：如果map包含具有相同键的多个条目，则键的最终值是不确定的**。

### 2.2.删

- **void clear()**

- QMap::iterator erase(QMap::iterator pos)

  从Map中移除迭代器pos指向的（键，值）对，并将迭代器返回到Map中的下一项。

- **int remove(const Key &key)**

  从Map上删除所有具有key的项目。 返回移除的项数，如果键存在于Map中，则为1，否则为0。

- T take(const Key &key)

  使用key从Map中删除该项目，并返回与之关联的值。
  如果该项目在Map中不存在，则该函数仅返回默认构造的值。 如果Map中有多个key项，则只会删除并返回最近插入的一项。
  **如果不使用返回值，则remove（）效率更高**。

### 2.3.改

- void swap(QMap<Key, T> &other)

  与此Map交换其他Map。 此操作非常快，并且永远不会失败。

- std::map<Key, T> toStdMap() const

  返回与此QMap等效的STL映射。

### 2.4.查

- **bool contains(const Key &key) const**

  如果Map包含带有key的项目，则返回true； 否则返回false。

- **int count(const Key &key) const**

  返回与key关联的项目数。

- int size() const

  返回映射中（键，值）对的数量。

- int count() const

- bool empty() const

  提供此功能是为了实现STL兼容性。 它等效于isEmpty（），如果映射为空，则返回true；否则返回false。

- **QMap::iterator find(const Key &key)**

  返回一个迭代器，该迭代器指向Map中具有键key的项。
  如果Map不包含带有键的项，则该函数返回end（）。
  如果Map包含多个带有键的项，则此函数返回指向最近插入值的迭代器。 其他值可以通过增加迭代器来访问。 例如，下面的代码使用相同的密钥遍历所有项目：

  

  ```c++
    QMap<QString, int> map;
   ...
   QMap<QString, int>::const_iterator i = map.find("HDR");
   while (i != map.end() && i.key() == "HDR") {
       cout << i.value() << Qt::endl;
       ++i;
   }
  ```

- QMap::const_iterator find(const Key &key) const

- T &first()

  返回对映射中第一个值的引用，即映射到最小键的值。 该函数假定映射不为空。
  取消共享（或调用const版本）时，此操作将在固定时间内执行。

- const T &first() const

- const Key &firstKey() const

  返回对地图中最小键的引用。 该函数假定映射不为空。
  这以**恒定的时间**执行。

- T &last()

  返回对映射中最后一个值的引用，即映射到最大键的值。 该函数假定映射不为空。
  当取消共享（或调用const版本）时，此操作将以对数时间执行。

- const T &last() const

- const Key &lastKey() const

  返回对地图中最大键的引用。 该函数假定映射不为空。
  这以**对数时间**执行。

- bool isEmpty() const

- const Key key(const T &value, const Key &defaultKey = Key()) const

  **返回具有值value的第一个键**，如果Map不包含具有value值的项，则返回defaultKey。 如果未提供defaultKey，则该函数将返回默认构造的键。
  **此功能可能很慢（线性时间）**，因为QMap的内部数据结构已针对通过键而不是通过值进行快速查找进行了优化。

- **QList<Key> keys() const**

  返回一个列表，其中包含Map中所有键的升序排列。 在映射中多次出现的键（因为该方法在QMultiMap上运行）在列表中也多次出现。
  该顺序保证与values（）使用的顺序相同。

- QList<Key> keys(const T &value) const

  返回一个列表，其中包含与值value升序关联的所有键。
  此功能可能很慢（线性时间），因为QMap的内部数据结构已针对通过键而不是通过值进行快速查找进行了优化。

- **const T value(const Key &key, const T &defaultValue = T()) const**

  返回与key关联的值。
  如果Map不包含带有key的项，则该函数返回defaultValue。 如果未指定defaultValue，则该函数返回默认构造的值。 如果映射中有多个键项，则返回最近插入的一项的值。

- **QList<T> values() const**

  以键的升序返回一个列表，其中包含映射中的所有值。 **如果一个键与多个值相关联，则其所有值将在列表中，而不仅仅是最近插入的一个**。

### 2.5.运算符

- bool operator!=(const QMap<Key, T> &other) const
- bool operator==(const QMap<Key, T> &other) const
- T &operator[](const Key &key)
- const T operator[](const Key &key) const

### 2.6.迭代器

- QMap::const_iterator constBegin() const

  返回指向Map中第一项的const STL样式迭代器。

- QMap::const_iterator constEnd() const

  返回指向Map中最后一项的const STL样式迭代器。

- QMap::const_iterator constFind(const Key &key) const

  返回指向映射中具有键key的项的const迭代器。
  如果地图不包含带有键的项，则该函数返回constEnd（）。

- QMap::const_key_value_iterator constKeyValueBegin() const

  返回指向映射中第一个条目的const STL样式的迭代器。

- QMap::const_key_value_iterator constKeyValueEnd() const

  返回指向映射中最后一个条目的const STL样式的迭代器。

- QMap::iterator begin()

- QMap::const_iterator begin() const

- QMap::iterator end()

- QMap::const_iterator end() const

- QMap::const_iterator cbegin() const

- QMap::const_iterator cend() const

- QMap::key_iterator keyBegin() const

- QMap::key_iterator keyEnd() const

- QMap::key_value_iterator keyValueBegin()

- QMap::const_key_value_iterator keyValueBegin() const

- QMap::key_value_iterator keyValueEnd()

- QMap::const_key_value_iterator keyValueEnd() const

- QMap::iterator lowerBound(const Key &key)

- QMap::const_iterator lowerBound(const Key &key) const

- QMap::iterator upperBound(const Key &key)

- QMap::const_iterator upperBound(const Key &key) const

- QPair<QMap::iterator, QMap::iterator> equal_range(const Key &key)

  返回一对迭代器，它们定义存储在key下的值的范围（[first，second]）。

- QPair<QMap::const_iterator, QMap::const_iterator> equal_range(const Key &key) const

### 2.7.构造析构

- QMap(const typename std::map<Key, T> &other)
- QMap(QMap<Key, T> &&other)
- QMap(const QMap<Key, T> &other)
- QMap(std::initializer_list<std::pair<Key, T> > list)
- QMap()
- QMap<Key, T> & operator=(QMap<Key, T> &&other)
- QMap<Key, T> & operator=(const QMap<Key, T> &other)
- ~QMap()

## 3.Related Non-Members

- QDataStream &operator<<(QDataStream &out, const QMap<Key, T> &map)
- QDataStream &operator>>(QDataStream &in, QMap<Key, T> &map)

## 4.Detailed Description

QMap <Key，T>是Qt的通用容器类之一。 它**存储（键，值）对**，并**提供与键关联的值的快速查找**。
QMap和QHash提供了非常相似的功能。 不同之处在于：

- **QHash提供比QMap平均更快的查找**。 （有关详细信息，请参见算法复杂性。）
- 在QHash上迭代时，可以任意订购这些项目。 **使用QMap，项目始终按键排序**。
- QHash的键类型必须提供operator ==（）和全局qHash（Key）函数。 QMap的键类型必须提供operator <（）来指定总的顺序。 从Qt 5.8.1开始，即使基础运算符<（）不提供总顺序，也可以安全地使用指针类型作为键。

