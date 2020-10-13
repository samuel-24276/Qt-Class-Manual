# QHash

继承者：QMultiHash

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

- QHash(InputIterator begin, InputIterator end)
- QHash(QHash<K, V> &&other)
- QHash(const QHash<K, V> &other)
- QHash(std::initializer_list<std::pair<Key, T> > list)
- QHash()
- QHash<K, V> &operator=(QHash<K, V> &&other)
- QHash<K, V> &operator=(const QHash<K, V> &other)
- ~QHash()
- QHash::iterator begin()
- QHash::const_iterator begin() const
- int capacity() const
- QHash::const_iterator cbegin() const
- QHash::const_iterator cend() const
- void clear()
- QHash::const_iterator constBegin() const
- QHash::const_iterator constEnd() const
- QHash::const_iterator constFind(const Key &key) const
- QHash::const_key_value_iterator constKeyValueBegin() const
- QHash::const_key_value_iterator constKeyValueEnd() const
- bool contains(const Key &key) const
- int count(const Key &key) const
- int count() const
- bool empty() const
- QHash::iterator end()
- QHash::const_iterator end() const
- QPair<QHash::iterator, QHash::iterator> equal_range(const Key &key)
- QPair<QHash::const_iterator, QHash::const_iterator> equal_range(const Key &key) 
- const
- QHash::iterator erase(QHash::const_iterator pos)
- QHash::iterator erase(QHash::iterator pos)
- QHash::iterator find(const Key &key)
- QHash::const_iterator find(const Key &key) const
- QHash::iterator insert(const Key &key, const T &value)
- void insert(const QHash<K, V> &other)
- bool isEmpty() const
- const Key key(const T &value) const
- const Key key(const T &value, const Key &defaultKey) const
- QHash::key_iterator keyBegin() const
- QHash::key_iterator keyEnd() const
- QHash::key_value_iterator keyValueBegin()
- QHash::const_key_value_iterator keyValueBegin() const
- QHash::key_value_iterator keyValueEnd()
- QHash::const_key_value_iterator keyValueEnd() const
- QList<Key> keys() const
- QList<Key> keys(const T &value) const
- int remove(const Key &key)
- void reserve(int size)
- int size() const
- void squeeze()
- void swap(QHash<K, V> &other)
- T take(const Key &key)
- const T value(const Key &key) const
- const T value(const Key &key, const T &defaultValue) const
- QList<T> values() const
- bool operator!=(const QHash<K, V> &other) const
- bool operator==(const QHash<K, V> &other) const
- T &operator[](const Key &key)
- const T operator[](const Key &key) const

## 3.Related Non-Members

## 4.Detailed Description