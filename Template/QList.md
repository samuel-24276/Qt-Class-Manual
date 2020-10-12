# QList

继承者：

- QByteArrayList
- QItemSelection
- QQueue
- QStringList

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

- QList(InputIterator first, InputIterator last)
- QList(std::initializer_list<T> args)
- QList(QList<T> &&other)
- QList(const QList<T> &other)
- QList()
- QList<T> &operator=(QList<T> &&other)
- QList<T> &operator=(const QList<T> &other)
- ~QList()
- void append(const T &value)
- void append(const QList<T> &value)
- const T &at(int i) const
- T &back()
- const T &back() const
- QList::iterator begin()
- QList::const_iterator begin() const
- QList::const_iterator cbegin() const
- QList::const_iterator cend() const
- void clear()
- QList::const_iterator constBegin() const
- QList::const_iterator constEnd() const
- const T &constFirst() const
- const T &constLast() const
- bool contains(const T &value) const
- int count(const T &value) const
- int count() const
- QList::const_reverse_iterator crbegin() const
- QList::const_reverse_iterator crend() const
- bool empty() const
- QList::iterator end()
- QList::const_iterator end() const
- bool endsWith(const T &value) const
- QList::iterator erase(QList::iterator pos)
- QList::iterator erase(QList::iterator begin, QList::iterator end)
- T &first()
- const T &first() const
- T &front()
- const T &front() const
- int indexOf(const T &value, int from = 0) const
- void insert(int i, const T &value)
- QList::iterator insert(QList::iterator before, const T &value)
- bool isEmpty() const
- T &last()
- const T &last() const
- int lastIndexOf(const T &value, int from = -1) const
- int length() const
- QList<T> mid(int pos, int length = -1) const
- void move(int from, int to)
- void pop_back()
- void pop_front()
- void prepend(const T &value)
- void push_back(const T &value)
- void push_front(const T &value)
- QList::reverse_iterator rbegin()
- QList::const_reverse_iterator rbegin() const
- int removeAll(const T &value)
- void removeAt(int i)
- void removeFirst()
- void removeLast()
- bool removeOne(const T &value)
- QList::reverse_iterator rend()
- QList::const_reverse_iterator rend() const
- void replace(int i, const T &value)
- void reserve(int alloc)
- int size() const
- bool startsWith(const T &value) const
- void swap(QList<T> &other)
- void swapItemsAt(int i, int j)
- T takeAt(int i)
- T takeFirst()
- T takeLast()
- QSet<T> toSet() const
- std::list<T> toStdList() const
- QVector<T> toVector() const
- T value(int i) const
- T value(int i, const T &defaultValue) const
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