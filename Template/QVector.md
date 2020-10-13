# QVector

继承者：

- QPolygon
- QPolygonF
- QStack
- QVulkanInfoVector
- QXmlStreamAttributes

## 1.Public Types

- typedef ConstIterator
- typedef Iterator
- typedef const_iterator
- typedef const_pointer
- typedef const_reference
- typedef const_reverse_iterator
- typedef difference_type
- typedef iterator
- typedef pointer
- typedef reference
- typedef reverse_iterator
- typedef size_type
- typedef value_type

## 2.Public Functions

### 2.1.增

- **void append(const T &value)**

  在向量的末尾插入值。

  这与调用resize（size（）+ 1）并将值分配给向量中的新的最后一个元素相同。
  此操作相对较快，因为QVector通常会分配比必要数量更多的内存，因此它可以增长而不必每次都重新分配整个向量。

- void append(T &&value)

- void append(const QVector<T> &value)

- **void push_back(const T &value)**

  提供此功能是为了实现STL兼容性。 它等效于append（value）。

- void push_back(T &&value)

- void push_front(T &&value)

- void prepend(T &&value)

- **void prepend(const T &value)**

  在向量的开头插入值。

  这与vector.insert（0，value）相同。
  对于大向量，此操作可能很慢（线性时间），因为它需要将向量中的所有项目在内存中进一步移动一个位置。 如果要使用提供快速prepend（）函数的容器类，请改用QList或QLinkedList。

- **void push_front(const T &value)**

  提供此功能是为了实现STL兼容性。 它等效于prepend（value）。

- void insert(int i, T &&value)

- **void insert(int i, const T &value)**

  将值插入向量中的索引位置i。 如果i为0，则该值位于向量的前面。 如果i为size（），则将值附加到向量。

  对于大向量，此操作可能会很慢（线性时间），因为它需要将索引i和更高位置的所有项目进一步移动到内存中的一个位置。 如果要使用提供快速insert（）函数的容器类，请改用QLinkedList。

- void insert(int i, int count, const T &value)

- QVector::iterator insert(QVector::iterator before, int count, const T &value)

- QVector::iterator insert(QVector::iterator before, const T &value)

- QVector::iterator insert(QVector::iterator before, T &&value)

### 2.2.删

- **void clear()**

  从向量中删除所有元素。
  注意：在Qt 5.6之前，这也释放了向量使用的内存。 从Qt 5.7开始，将保留容量。 要释放所有容量，请使用默认构造的向量交换：

  ```C++
  QVector<T> v ...;
  QVector<T>().swap(v);
  Q_ASSERT(v.capacity() == 0);
  ```

  或者调用squeeze()。

- **QVector::iterator erase(QVector::iterator pos)**

  从向量中移除迭代器pos指向的项目，并将迭代器返回到向量中的下一项（可能是end（））。

- **QVector::iterator erase(QVector::iterator begin, QVector::iterator end)**

  从开始到（但不包括）结束删除所有项目。 将迭代器返回到调用之前结束引用的同一项目。

- **void pop_back()**

  提供此功能是为了实现STL兼容性。 它等效于removeLast（）。

- **void pop_front()**

  提供此功能是为了实现STL兼容性。 它等效于removeFirst（）。

- **void remove(int i)**

  删除索引位置i处的元素。

- **void remove(int i, int count)**

  从索引位置i开始，从向量的中间删除计数元素。

- **int removeAll(const T &t)**

  从向量中删除所有等于t的元素。 返回删除的元素数（如果有）。
  提供与QList的兼容性。

- **void removeAt(int i)**

- **void removeFirst()**

- **void removeLast()**

- **bool removeOne(const T &t)**

  从向量中删除比较等于t的**第一个**元素。 返回实际上是否删除了一个元素。
  提供与QList的兼容性。

- **T takeAt(int i)**

  删除索引位置i处的元素并返回它。

  提供与QList的兼容性。

- **T takeFirst()**

  移除向量中的第一项并返回它。 此函数假定向量不为空。 为避免失败，请在调用此函数之前调用isEmpty（）。

- **T takeLast()**

  删除列表中的最后一项并返回。 此函数假定向量不为空。 为避免失败，请在调用此函数之前调用isEmpty（）。
  如果不使用返回值，则removeLast（）会更有效。

### 2.3.改

- **void move(int from, int to)**

  将索引位置的项目从移到索引位置。
  提供与QList的兼容性。

- **void replace(int i, const T &value)**

  用值替换索引位置i处的项目。
  必须是向量中的有效索引位置（即0 <= i <size（））。

- **void reserve(int size)**

  尝试为至少size个元素分配内存。如果事先知道向量的大小，则应调用此函数以防止重新分配和内存碎片。
  如果size被低估，那么最糟糕的情况就是QVector会变慢。如果大小被高估，则您可能使用了比正常QVector增长策略分配的内存更多的内存，或者您使用的内存更少。
  reserve（）的替代方法是调用resize（）。是否快于reserve（）取决于元素类型，因为resize（）默认构造所有元素，并且需要分配给现有条目，而不是调用copy（）或move-constructs的append（）。对于简单类型（例如int或double），resize（）通常更快，但是对于更复杂的类型，您应该首选reserve（）。
  警告：如果传递给resize（）的大小被低估了，则会耗尽分配的空间，并导致未定义的行为。 reserve（）不存在此问题，因为它将大小仅作为提示。

- **void resize(int size)**

  将向量的大小设置为size。 如果size大于当前大小，则将元素添加到末尾；否则，将添加元素。 新元素将使用默认构造的值进行初始化。 如果size小于当前大小，则从末尾删除元素。
  从Qt 5.6开始，resize（）不再缩小容量。 要释放多余的容量，请使用squeeze（）。

- **void shrink_to_fit()**

  提供此功能是为了实现STL兼容性。 它等效于squeeze（）。

- **void squeeze()**

  释放任何不需要存储项目的内存。
  此功能的唯一目的是提供一种微调QVector的内存使用量的方法。 通常，您几乎不需要调用此函数。

- **void swap(QVector<T> &other)**

  交换其他与此向量。 此操作非常快，并且永远不会失败。

- **void swapItemsAt(int i, int j)**

  将索引位置i处的项目与索引位置j处的项目进行交换。 此函数假定i和j都至少为0但小于size（）。 为避免失败，请测试i和j至少为0并小于size（）。

- **QVector<T> &fill(const T &value, int size = -1)**

  为向量中的所有项目分配值。 如果size与-1（默认值）不同，则将矢量预先调整为size大小。

### 2.4.查

- **bool isEmpty() const**

  如果向量的大小为0，则返回true；否则返回false。

- **bool empty() const**

  提供此功能是为了实现STL兼容性。 它等效于isEmpty（），如果向量为空，则返回true； 否则返回false。

- **const T &at(int i) const**

  返回向量中索引位置i处的项目。
  必须是向量中的有效索引位置（即0 <= i <size（））。

- **`int capacity() const`**

  返回在不强制重新分配的情况下可以存储在向量中的最大项目数。
  此功能的唯一目的是提供一种微调QVector的内存使用量的方法。 通常，您几乎不需要调用此函数。 如果您想知道向量中有多少个项目，请调用size（）。

- **int count(const T &value) const**

  返回向量中值出现的次数。
  此函数**要求值类型具有operator ==（）的实现**。

- int count() const

- **int size() const**

  返回向量中的项目数。

- **int length() const**

  与size（）和count（）相同。
  提供与QList的兼容性。

- QVector::const_iterator constBegin() const

- **const T *constData() const**

  返回指向向量中存储数据的const指针。 指针可用于访问向量中的项目。 只要不重新分配向量，指针就保持有效。
  该函数在将向量传递给接受纯C ++数组的函数时最有用。

- QVector::const_iterator constEnd() const

- const T &constFirst() const

- const T &constLast() const

- **bool contains(const T &value) const**

  如果向量包含出现的值，则返回true；否则返回false。
  **此函数要求值类型具有operator ==（）的实现**。

- **T *data()**

  返回指向向量中存储的数据的指针。 指针可用于访问和修改向量中的项目。

- const T *data() const

- **T value(int i) const**

  返回向量中索引位置i处的值。
  如果索引i超出范围，则该函数将返回默认构造的值。 **如果您确定我在范围之内，则可以改用at（），它稍快一些**。

- **T value(int i, const T &defaultValue) const**

  如果索引i超出范围，则该函数返回defaultValue。

- **bool endsWith(const T &value) const**

  如果此向量不为空并且其最后一项等于value，则返回true；否则，返回true。 否则返回false。

- **bool startsWith(const T &value) const**

  果此向量不为空并且其第一项等于value，则返回true；否则，返回true。 否则返回false。

- **T &first()**

  返回对向量中第一项的引用。 此函数假定向量不为空。

- const T &first() const

- **T &last()**

  返回对向量中最后一项的引用。 此函数假定向量不为空。

- const T &last() const

- **T &front()**

  提供此功能是为了实现STL兼容性。 它等效于first（）。

- QVector::const_reference front() const

- **QVector::reference back()**

  提供此功能是为了实现STL兼容性。 它等效于last（）。

- QVector::const_reference back() const

- **int indexOf(const T &value, int from = 0) const**

  返回向量中值第一次出现的索引位置，从索引位置from开始向前搜索。 如果没有匹配项，则返回-1。

  此函数要求值类型具有operator ==（）的实现。

- **int lastIndexOf(const T &value, int from = -1) const**

  返回向量中最后一次出现的值的索引位置，从索引位置from开始向后搜索。 如果from为-1（默认值），则搜索从最后一项开始。 如果没有匹配项，则返回-1。

- **QVector<T> mid(int pos, int length = -1) const**

  返回一个子向量，该子向量包含从位置pos开始的该向量中的元素。 如果length为-1（默认值），则包括pos之后的所有元素；否则为false。 否则，将包括长度元素（如果长度少于元素，则包括所有其余元素）。

### 2.5.运算符

- bool operator!=(const QVector<T> &other) const
- QVector<T> operator+(const QVector<T> &other) const
- QVector<T> &operator+=(const QVector<T> &other)
- QVector<T> &operator+=(const T &value)
- QVector<T> &operator+=(T &&value)
- QVector<T> &operator<<(const T &value)
- QVector<T> &operator<<(const QVector<T> &other)
- QVector<T> &operator<<(T &&value)
- QVector<T> &operator=(std::initializer_list<T> args)
- bool operator==(const QVector<T> &other) const
- T &operator[](int i)
- const T &operator[](int i) const

### 2.6.迭代器

- QVector::iterator begin()
- QVector::const_iterator begin() const
- QVector::iterator end()
- QVector::const_iterator end() const
- QVector::reverse_iterator rbegin()
- QVector::const_reverse_iterator rbegin() const
- QVector::reverse_iterator rend()
- QVector::const_reverse_iterator rend() const
- QVector::const_reverse_iterator crbegin() const
- QVector::const_reverse_iterator crend() const
- QVector::const_iterator cbegin() const
- QVector::const_iterator cend() const

### 2.7.构造析构

- QVector(InputIterator first, InputIterator last)
- QVector(std::initializer_list<T> args)
- QVector(QVector<T> &&other)——**双引用为左值引用？**
- QVector(const QVector<T> &other)
- QVector(int size, const T &value)
- QVector(int size)
- QVector()
- QVector<T> &operator=(QVector<T> &&other)
- QVector<T> &operator=(const QVector<T> &other)
- ~QVector()

### 2.8.转换为

- QList<T> toList() const

  返回带有此QVector中包含的数据的QList对象，过时。

  **注意：从Qt 5.14开始，范围构造函数可用于Qt的通用容器类，并且应代替此方法使用。**

- std::vector<T> toStdVector() const

  返回带有此QVector中包含的数据的std :: vector对象，过时。

  **注意：从Qt 5.14开始，范围构造函数可用于Qt的通用容器类，并且应代替此方法使用。**

## 3.Static Public Members

- QVector<T> fromList(const QList<T> &list)

  返回带有List中包含的数据的QVector对象，过时。

  **注意：从Qt 5.14开始，范围构造函数可用于Qt的通用容器类，并且应代替此方法使用。**

- QVector<T> fromStdVector(const std::vector<T> &vector)

  返回带有Vector中包含的数据的QVector对象，过时。 QVector中元素的顺序与向量中的顺序相同。

  **注意：从Qt 5.14开始，范围构造函数可用于Qt的通用容器类，并且应代替此方法使用。**

## 4.Related Non-Members

- uint qHash(const QVector<T> &key, uint seed = 0)
- bool operator<(const QVector<T> &lhs, const QVector<T> &rhs)
- QDataStream &operator<<(QDataStream &out, const QVector<T> &vector)
- bool operator<=(const QVector<T> &lhs, const QVector<T> &rhs)
- bool operator>(const QVector<T> &lhs, const QVector<T> &rhs)
- bool operator>=(const QVector<T> &lhs, const QVector<T> &rhs)
- QDataStream &operator>>(QDataStream &in, QVector<T> &vector)

## 5.Detailed Description

QVector <T>是Qt的通用容器类之一。它将项目**存储在相邻的内存位置**，并提供**基于索引的快速访问**。
QList <T>，QLinkedList <T>，QVector <T>和QVarLengthArray <T>提供相似的API和功能。它们通常是可互换的，但是会带来性能后果。以下是用例的概述：

- QVector应该是您的默认首选。 **QVector <T>通常会提供比QList <T>更好的性能**，因为QVector <T>始终将其项顺序存储在内存中，其中QList <T>会将其项分配在堆上，除非sizeof（T）<= sizeof（void *），并且已使用Q_DECLARE_TYPEINFO将T声明为Q_MOVABLE_TYPE或Q_PRIMITIVE_TYPE。有关说明，请参见使用QList的优缺点。
- 但是，整个Qt API都使用QList来传递参数和返回值。使用QList与这些API交互。
- 如果您需要一个真正的链表，该链表可以保证在列表中插入固定时间并使用迭代器而不是索引，请使用QLinkedList。

**注意：**QVector和QVarLengthArray都保证C兼容的数组布局。 QList没有。如果您的应用程序必须与C API接口，则这可能很重要。
**注意：**只要被引用的项目保留在容器中，对QLinkedList的迭代器和对分配堆的QList的引用将保持有效。对于迭代器以及对QVector和非堆分配QList的引用，情况并非如此。

### Maximum size and out-of-memory conditions

当前版本的QVector的大小被限制在2 GB（2 ^ 31字节）以下。 确切的值取决于体系结构，因为它取决于管理数据块所需的开销，但不超过32个字节。 可以存储在QVector中的元素数量是该大小除以每个元素的大小。
万一内存分配失败，QVector将使用Q_CHECK_PTR宏，如果正在使用异常支持编译应用程序，则它将抛出std :: bad_alloc异常。 如果禁用了异常，则内存不足是未定义的行为。
请注意，操作系统可能会对持有大量已分配内存（尤其是大的连续块）的应用程序施加进一步的限制。 这些考虑因素，此类行为的配置或任何缓解措施均不在Qt API的范围之内。