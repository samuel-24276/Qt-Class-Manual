# QVector

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

- QVector(InputIterator first, InputIterator last)

- QVector(std::initializer_list<T> args)

- QVector(QVector<T> &&other)

- QVector(const QVector<T> &other)

- QVector(int size, const T &value)

- QVector(int size)

- QVector()

- QVector<T> &operator=(QVector<T> &&other)

- QVector<T> &operator=(const QVector<T> &other)

- ~QVector()

- void append(const T &value)

- void append(T &&value)

- void append(const QVector<T> &value)

- const T &at(int i) const

- QVector::reference back()

- QVector::const_reference back() const

- QVector::iterator begin()

- QVector::const_iterator begin() const

- `int capacity() const`

  返回在不强制重新分配的情况下可以存储在向量中的最大项目数。
  此功能的唯一目的是提供一种微调QVector的内存使用量的方法。 通常，您几乎不需要调用此函数。 如果您想知道向量中有多少个项目，请调用size（）。

- QVector::const_iterator cbegin() const

- QVector::const_iterator cend() const

- void clear()

- QVector::const_iterator constBegin() const

- const T *constData() const

- QVector::const_iterator constEnd() const

- const T &constFirst() const

- const T &constLast() const

- bool contains(const T &value) const

- int count(const T &value) const

- int count() const

- QVector::const_reverse_iterator crbegin() const

- QVector::const_reverse_iterator crend() const

- T *data()

- const T *data() const

- bool empty() const

- QVector::iterator end()

- QVector::const_iterator end() const

- bool endsWith(const T &value) const

- QVector::iterator erase(QVector::iterator pos)

- QVector::iterator erase(QVector::iterator begin, QVector::iterator end)

- QVector<T> &fill(const T &value, int size = -1)

- T &first()

- const T &first() const

- T &front()

- QVector::const_reference front() const

- int indexOf(const T &value, int from = 0) const

- void insert(int i, T &&value)

- void insert(int i, const T &value)

- void insert(int i, int count, const T &value)

- QVector::iterator insert(QVector::iterator before, int count, const T &value)

- QVector::iterator insert(QVector::iterator before, const T &value)

- QVector::iterator insert(QVector::iterator before, T &&value)

- bool isEmpty() const

- T &last()

- const T &last() const

- int lastIndexOf(const T &value, int from = -1) const

- int length() const

- QVector<T> mid(int pos, int length = -1) const

- void move(int from, int to)

- void pop_back()

- void pop_front()

- void prepend(T &&value)

- void prepend(const T &value)

- void push_back(const T &value)

- void push_back(T &&value)

- void push_front(T &&value)

- void push_front(const T &value)

- QVector::reverse_iterator rbegin()

- QVector::const_reverse_iterator rbegin() const

- void remove(int i)

- void remove(int i, int count)

- int removeAll(const T &t)

- void removeAt(int i)

- void removeFirst()

- void removeLast()

- bool removeOne(const T &t)

- QVector::reverse_iterator rend()

- QVector::const_reverse_iterator rend() const

- void replace(int i, const T &value)

- void reserve(int size)

  尝试为至少size个元素分配内存。如果事先知道向量的大小，则应调用此函数以防止重新分配和内存碎片。
  如果size被低估，那么最糟糕的情况就是QVector会变慢。如果大小被高估，则您可能使用了比正常QVector增长策略分配的内存更多的内存，或者您使用的内存更少。
  reserve（）的替代方法是调用resize（）。是否快于reserve（）取决于元素类型，因为resize（）默认构造所有元素，并且需要分配给现有条目，而不是调用copy（）或move-constructs的append（）。对于简单类型（例如int或double），resize（）通常更快，但是对于更复杂的类型，您应该首选reserve（）。
  警告：如果传递给resize（）的大小被低估了，则会耗尽分配的空间，并导致未定义的行为。 reserve（）不存在此问题，因为它将大小仅作为提示。

- void resize(int size)

- void shrink_to_fit()

- int size() const

- void squeeze()

- bool startsWith(const T &value) const

- void swap(QVector<T> &other)

- void swapItemsAt(int i, int j)

- T takeAt(int i)

- T takeFirst()

- T takeLast()

- QList<T> toList() const

- std::vector<T> toStdVector() const

- T value(int i) const

- T value(int i, const T &defaultValue) const

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