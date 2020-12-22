# QSet

## 1.Public Types

- class const_iterator
- class iterator
- typedef ConstIterator
- typedef Iterator
- typedef const_pointer
- typedef const_reference
- typedef difference_type
- typedef key_type
- typedef pointer
- typedef reference
- typedef size_type
- typedef value_type

## 2.Public Functions

### 2.1.增

- QSet::iterator insert(const T &value)

  如果集合中尚未包含value，则将其插入集合中，并返回指向插入项的迭代器。

### 2.2.删

- void clear()

  清除集合的所有元素。

- **`QSet::iterator erase(QSet::const_iterator pos)`**

  从集合中删除迭代器位置pos的项目，并返回位于集合中下一个项目的迭代器。
  **与remove（）不同，此函数从不导致QSet重新哈希其内部数据结构**。 这意味着可以在迭代时安全地调用它，并且不会影响集合中项目的顺序。

- QSet::iterator erase(QSet::iterator pos)

- bool remove(const T &value)

  从集合中删除所有出现的item value。 如果实际删除了一个项目，则返回true； 否则返回false。

### 2.3.改

- void reserve(int size)

  确保集合的内部哈希表至少包含buckets的大小size。

  理想情况下，大小应略大于集合中预期的最大元素数量。 size不必是素数，因为QSet无论如何都会在内部使用素数。 如果size被低估，则最糟糕的情况是QSet会变慢。

  通常，您几乎不需要调用此函数。 QSet的内部哈希表会自动缩小或增长以提供良好的性能，而不会浪费太多内存。

- void squeeze()

  减小集合的内部哈希表的大小以节省内存。
  此功能的唯一目的是提供一种微调QSet内存使用情况的方法。 通常，您几乎不需要调用此函数。

- void swap(QSet<T> &other)

  将此集合与其他集合交换。 此操作非常快，并且永远不会失败。

- QList<T> toList() const

  返回包含集合中元素的新QList。 QList中元素的顺序未定义。过时

  **注意**：从Qt 5.14开始，范围构造函数可用于Qt的通用容器类，并且应代替此方法使用。

- QSet<T> &unite(const QSet<T> &other)——合并集合数据到此集合

  另一个集合中尚未包含在该集合中的每个项目都插入到该集合中。 返回对此集合的引用。

- QSet<T> &intersect(const QSet<T> &other)——寻找公共子集

  从该集合中删除另一个集合中未包含的所有项目。 返回对此集合的引用。

- QSet<T> &subtract(const QSet<T> &other)——去除公共子集

  从该集合中删除另一个集合中包含的所有项目。 返回对此集合的引用。

### 2.4.查

- int capacity() const

- QSet::const_iterator constFind(const T &value) const

  返回位于集合中项目值为value处的const迭代器。 如果集合中不包含任何项目值，则该函数返回constEnd（）。

- **`bool contains(const T &value) const`**

  如果集合包含项目值，则返回true； 否则返回false。

- **`bool contains(const QSet<T> &other) const`**

  如果集合包含另一个集合中的所有项目，则返回true； 否则返回false。

- int count() const

- bool empty() const

- QSet::const_iterator find(const T &value) const

  返回位于集合中项目值为value处的const迭代器。 如果集合中不包含任何项目值，则该函数返回constEnd（）。

- QSet::iterator find(const T &value)

  返回位于集合中项目值为value处的非常量迭代器。 如果集合中不包含任何项目值，则该函数返回end（）。

- bool isEmpty() const

- int size() const

- QList<T> values() const

  返回包含集合中元素的新QList。 QList中元素的顺序未定义。过时
  这与toList（）相同。
  注意：从Qt 5.14开始，范围构造函数可用于Qt的通用容器类，并且应代替此方法使用。

- bool intersects(const QSet<T> &other) const——判断是否有公共子集

  如果此集合具有至少一个与其他项相同的项，则返回true。

### 2.5.构造函数

- QSet(InputIterator first, InputIterator last)
- QSet(std::initializer_list<T> list)
- QSet()

### 2.6.运算符

- bool operator!=(const QSet<T> &other) const
- QSet<T> operator&(const QSet<T> &other) const
- QSet<T> &operator&=(const QSet<T> &other)
- QSet<T> &operator&=(const T &value)
- QSet<T> operator+(const QSet<T> &other) const
- QSet<T> &operator+=(const QSet<T> &other)
- QSet<T> &operator+=(const T &value)
- QSet<T> operator-(const QSet<T> &other) const
- QSet<T> &operator-=(const QSet<T> &other)
- QSet<T> &operator-=(const T &value)
- QSet<T> &operator<<(const T &value)
- bool operator==(const QSet<T> &other) const
- QSet<T> operator|(const QSet<T> &other) const
- QSet<T> &operator|=(const QSet<T> &other)
- QSet<T> &operator|=(const T &value)

### 2.7.迭代器

- QSet::const_iterator begin() const
- QSet::iterator begin()
- QSet::const_iterator cbegin() const
- QSet::const_iterator cend() const
- QSet::const_iterator constBegin() const
- QSet::const_iterator constEnd() const
- QSet::const_iterator end() const
- QSet::iterator end()

## 3.Static Public Members

- QSet<T> fromList(const QList<T> &list)

  返回一个新的QSet对象，其中包含列表中包含的数据。 由于QSet不允许重复，因此生成的QSet可能小于列表，因为QList可以包含重复项。

## 4.Related Non-Members

- QDataStream &operator<<(QDataStream &out, const QSet<T> &set)

  将集合写入流中。
  此函数需要值类型T来实现operator <<（）。

- QDataStream &operator>>(QDataStream &in, QSet<T> &set)

  从流中读取集合到集合中。
  此函数需要值类型T来实现operator <<（）。

## 5.Detailed Description

QSet <T>是Qt的通用容器类之一。 它以未指定的顺序存储值，并提供非常快速的值查找。 **在内部，QSet <T>被实现为QHash**。

QSet的value数据类型必须是可分配的数据类型。 例如，您不能将QWidget存储为值。 而是存储一个QWidget *。 此外，该类型必须提供operator ==（），并且还必须有一个全局qHash（）函数，该函数返回键类型的参数的哈希值。 请参阅QHash文档以获取qHash（）支持的类型列表。

在内部，QSet使用哈希表执行查找。 哈希表会自动增长和收缩，以提供快速查找而不会浪费内存。 如果您已经知道QSet大约包含多少个元素，仍然可以通过调用reserve（）来控制哈希表的大小，但这对于获得良好的性能不是必需的。 您还可以调用Capacity（）来检索哈希表的大小。