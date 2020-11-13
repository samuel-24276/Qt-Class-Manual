# QList

继承者：

- QByteArrayList
- QItemSelection
- QQueue
- QStringList

QLinkedList是它的变种——链表，但已过时，尽量不使用。

## 1.Public Types

- class const_iterator
- class iterator
- typedef ConstIterator
- typedef Iterator
- typedef const_pointer
- typedef const_reference
- typedef const_reverse_iterator
- typedef difference_type
- typedef pointer
- typedef reference
- typedef reverse_iterator
- typedef size_type
- typedef value_type

## 2.Public Functions

### 2.1.增

- void insert(int i, const T &value)

  将value插入列表中的索引位置i。
  如果i == 0，则该值位于列表的前面。 如果i == size（），则将值附加到列表中。

- QList::iterator insert(QList::iterator before, const T &value)

  在迭代器before指向的项目前面插入value。 返回指向插入项的迭代器。 注意，**调用后传递给函数的迭代器将无效。 应该使用返回的迭代器代替**。

- void append(const T &value)

  在列表的末尾插入值。

  这与list.insert（size（），value）相同。
  **如果不共享此列表，则此操作通常非常快（摊销的固定时间）**，因为QList在其内部缓冲区的两侧预先分配了额外的空间，以允许在列表的两端快速增长。

- void append(const QList<T> &value)

- void prepend(const T &value)

  在列表的开头插入值。

  这与list.insert（0，value）相同。
  如果未共享此列表，则此操作通常非常快（摊销的固定时间），因为QList在其内部缓冲区的两侧预分配了额外的空间，以允许在列表的两端快速增长。

- void push_back(const T &value)

  提供此功能是为了实现STL兼容性。 它等效于append（value）。

- void push_front(const T &value)

  提供此功能是为了实现STL兼容性。 它等效于prepend（value）。

### 2.2.删

- void clear()

- QList::iterator erase(QList::iterator pos)

  从列表中删除与迭代器pos关联的项目，并将迭代器返回到列表中的下一个项目（可能是end（））。

- QList::iterator erase(QList::iterator begin, QList::iterator end)

- void pop_back()

- void pop_front()

- int removeAll(const T &value)

  删除列表中所有出现的value的值，并返回删除的条目数。

  此函数要求值类型具有operator ==（）的实现。

- void removeAt(int i)

  删除索引位置i处的项目。 i必须是列表中的有效索引位置（即0 <= i <size（））。

- void removeFirst()

  删除列表中的第一项。 调用此函数等效于调用removeAt（0）。 该列表不能为空。 如果列表可以为空，请在调用此函数之前调用isEmpty（）。

- void removeLast()

  删除列表中的最后一项。 调用此函数等效于调用removeAt（size（）-1）。 该列表不能为空。 如果列表可以为空，请在调用此函数之前调用isEmpty（）。

- bool removeOne(const T &value)

  删除列表中第一个出现的值，并在成功时返回true； 否则返回false。

  此函数要求值类型具有operator ==（）的实现。

- T takeAt(int i)

  删除索引位置i处的项目并返回它。i 必须是列表中的有效索引位置（即0 <= i <size（））。
  **如果不使用返回值，则removeAt（）会更有效**。

- T takeFirst()

- T takeLast()

### 2.3.改

- void move(int from, int to)

  将索引位置from的项目移到索引位置to。

- void swap(QList<T> &other)

- void swapItemsAt(int i, int j)

  将索引位置i处的项目与索引位置j处的项目进行交换。 此函数假定i和j都至少为0但小于size（）。 为避免失败，请测试i和j至少为0并小于size（）。

- void replace(int i, const T &value)

  用value替换索引位置i处的项目。 i必须是列表中的有效索引位置（即0 <= i <size（））。

- void reserve(int alloc)

  为分配元素保留空间。
  如果alloc小于列表的当前大小，则不会发生任何事情。
  如果您可以预测要添加多少个元素，请使用此功能避免重复分配QList内部数据。 请注意，reservation仅适用于内部指针数组。

- QSet<T> toSet() const——过时

- std::list<T> toStdList() const——过时

- QVector<T> toVector() const——过时

### 2.4.查

- const T &at(int i) const

  返回列表中索引位置i处的项目。 i必须是列表中的有效索引位置（即0 <= i <size（））。
  此功能非常快（恒定时间）。

- T &front()

  提供此功能是为了实现STL兼容性。 它等效于first（）。 该列表不能为空。 如果列表可以为空，请在调用此函数之前调用isEmpty（）。

- const T &front() const

- T &back()

  提供此功能是为了实现STL兼容性。 它等效于last（）。 该列表不能为空。 如果列表可以为空，请在调用此函数之前调用isEmpty（）。

- const T &back() const

- T &first()

- const T &first() const

- T &last()

- const T &last() const

- const T &constFirst() const

- const T &constLast() const

- bool contains(const T &value) const

  如果列表包含出现的值，则返回true； 否则返回false。
  此函数要求值类型具有operator ==（）的实现。

- int count(const T &value) const

  返回列表中value出现的次数。
  此函数要求值类型具有operator ==（）的实现。

- int count() const

- int length() const

- int size() const

- bool empty() const

- bool isEmpty() const

- bool startsWith(const T &value) const

  如果此列表不为空并且其第一项等于value，则返回true； 否则返回false。

- bool endsWith(const T &value) const

  如果此列表不为空并且其最后一项等于value，则返回true； 否则返回false。

- int indexOf(const T &value, int from = 0) const

  返回列表中第一个出现的value的索引位置，从索引位置from开始向前搜索。 如果没有匹配项，则返回-1。

  此函数要求值类型具有operator ==（）的实现。
  请注意，QList使用基于0的索引，就像C ++数组一样。 除上述值外，不支持负索引。

- int lastIndexOf(const T &value, int from = -1) const

  返回列表中最后一次出现的值的索引位置，从索引位置from开始向后搜索。 如果from为-1（默认值），则搜索从最后一项开始。 如果没有匹配项，则返回-1。

  此函数要求值类型具有operator ==（）的实现。
  请注意，QList使用基于0的索引，就像C ++数组一样。 除上述值外，不支持负索引。

- **`QList<T> mid(int pos, int length = -1) const`**

  返回一个子列表，其中包括该列表中的元素（从位置pos开始）。 如果length为-1（默认值），则包括pos中的所有元素；否则为false。 否则，将包括长度元素（如果长度少于元素，则包括所有其余元素）。

- T value(int i) const

  返回列表中索引位置i处的值。
  如果索引i超出范围，则该函数将返回默认构造的值。 如果确定索引将在范围内，则可以使用at（）来代替，这会稍微快一些。

- T value(int i, const T &defaultValue) const

### 2.5.构造析构

- QList(InputIterator first, InputIterator last)
- QList(std::initializer_list<T> args)
- QList(QList<T> &&other)
- QList(const QList<T> &other)
- QList()
- QList<T> &operator=(QList<T> &&other)
- QList<T> &operator=(const QList<T> &other)
- ~QList()

### 2.6.迭代器

- QList::iterator begin()
- QList::const_iterator begin() const
- QList::iterator end()
- QList::const_iterator end() const
- QList::const_iterator cbegin() const
- QList::const_iterator cend() const
- QList::const_iterator constBegin() const
- QList::const_iterator constEnd() const
- QList::reverse_iterator rbegin()
- QList::const_reverse_iterator rbegin() const
- QList::reverse_iterator rend()
- QList::const_reverse_iterator rend() const
- QList::const_reverse_iterator crbegin() const
- QList::const_reverse_iterator crend() const

### 2.7.运算符

- bool operator!=(const QList<T> &other) const
- QList<T> operator+(const QList<T> &other) const
- QList<T> &operator+=(const QList<T> &other)
- QList<T> &operator+=(const T &value)
- QList<T> &operator<<(const QList<T> &other)
- QList<T> &operator<<(const T &value)
- bool operator==(const QList<T> &other) const
- T &operator[](int i)
- const T &operator[](int i) const

## 3.Static Public Members

QList<T> fromSet(const QSet<T> &set)
QList<T> fromStdList(const std::list<T> &list)
QList<T> fromVector(const QVector<T> &vector)

## 4.Related Non-Members

- uint qHash(const QList<T> &key, uint seed = 0)
- bool operator<(const QList<T> &lhs, const QList<T> &rhs)
- QDataStream &operator<<(QDataStream &out, const QList<T> &list)
- bool operator<=(const QList<T> &lhs, const QList<T> &rhs)
- bool operator>(const QList<T> &lhs, const QList<T> &rhs)
- bool operator>=(const QList<T> &lhs, const QList<T> &rhs)
- QDataStream &operator>>(QDataStream &in, QList<T> &list)

## 5.Detailed Description

QList <T>是Qt的通用容器类之一。它将项目存储在一个列表中，该列表提供了基于索引的快速访问以及基于索引的插入和删除。
QList <T>，QLinkedList <T>和QVector <T>提供类似的API和功能。它们通常是可互换的，但是会带来性能后果。以下是用例的概述：

- **QVector应该是您的默认首选。 QVector <T>通常会提供比QList <T>更好的性能**，因为QVector <T>始终将其项顺序存储在内存中，其中QList <T>会将其项分配在堆上，除非sizeof（T）<= sizeof（void *），并且已使用Q_DECLARE_TYPEINFO将T声明为Q_MOVABLE_TYPE或Q_PRIMITIVE_TYPE。有关说明，请参见使用QList的优缺点。
- 但是，整个Qt API都使用QList来传递参数和返回值。使用QList与这些API交互。
- 如果您需要一个真正的链表，该链表可以保证在列表中插入固定时间并使用迭代器而不是索引，请使用QLinkedList。