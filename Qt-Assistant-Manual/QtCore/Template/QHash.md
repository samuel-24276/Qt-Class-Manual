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

### 2.1.增

- **`QHash::iterator insert(const Key &key, const T &value)`**

  **插入具有键key和值value的新项目**。
  如果已经有一个带有键的项目，则该项目的值将替换为value。
  如果键有多个项目，则将最新插入的项目的值替换为value。

- **`void insert(const QHash<K, V> &other)`**

  **将另一个哈希中的所有项目插入此哈希中**。
  如果两个哈希共用一个密钥，则其值将替换为另一个中存储的值。
  注意：如果other包含具有相同键的多个条目，则该键的最终值是不确定的。

### 2.2.删

- **QHash::iterator erase(QHash::const_iterator pos)**

  从哈希中删除与迭代器pos相关联的（键，值）对，并将迭代器返回到哈希中的下一项。
  与remove（）和take（）不同，**此函数从不导致QHash重新哈希其内部数据结构。** 这意味着可以在迭代时安全地调用它，并且不会影响哈希中各项的顺序。 例如：

- QHash::iterator erase(QHash::iterator pos)

- void clear()

- **int remove(const Key &key)**

  **从哈希中删除所有具有key的项**。 返回删除的项数，如果键在哈希中，则为1，否则为0。

- T take(const Key &key)

  从哈希中删除带有键的项，并返回与之关联的值。
  如果该项目不存在于哈希中，则该函数仅返回默认构造的值。 如果哈希中有多个密钥项，则仅删除最近插入的项。
  如果不使用返回值，则remove（）效率更高。

### 2.3.改

- void reserve(int size)

  确保QHash的内部哈希表至少由存储桶的size组成。
  此功能对于需要构建巨大哈希值并希望避免重复分配的代码很有用。

  理想情况下，大小应略大于哈希中预期的最大项目数。 大小不必是素数，因为QHash无论如何都会在内部使用素数。 如果size被低估，则最糟糕的情况是QHash会慢一些。
  通常，您几乎不需要调用此函数。 QHash的内部哈希表会自动缩小或增长以提供良好的性能，而不会浪费太多内存。

- void squeeze()

  减小QHash内部哈希表的大小以节省内存。
  此功能的唯一目的是提供一种微调QHash内存使用情况的方法。 通常，您几乎不需要调用此函数。

- void swap(QHash<K, V> &other)

  使用此哈希交换其他哈希。 此操作非常快，并且永远不会失败。

### 2.4.查

- bool contains(const Key &key) const

  如果散列包含带有键的项目，则返回true； 否则返回false。

- int count(const Key &key) const

  返回哈希表包含的key的数量。

- int count() const

- int capacity() const

  返回QHash内部哈希表中的存储桶（bucket）数。
  此功能的唯一目的是提供一种微调QHash内存使用情况的方法。 通常，您几乎不需要调用此函数。 如果您想知道哈希中有多少个项目，请调用size（）。

- int size() const

- bool empty() const

- bool isEmpty() const

- QHash::iterator find(const Key &key)

  返回一个哈希值指向该项目的迭代器。
  如果哈希表不包含带有key的项目，则该函数返回end（）。
  如果哈希表包含多个带有key的项，则此函数返回指向最近插入值的迭代器。 其他值可以通过增加迭代器来访问。 例如，下面的代码使用相同的密钥遍历所有项目：

  

  ```c++
  QHash<QString, int> hash; 
  ...
   QHash<QString, int>::const_iterator i = hash.find("HDR");
   while (i != hash.end() && i.key() == "HDR") {
       cout << i.value() << Qt::endl;
       ++i;
   }
  ```

- QHash::const_iterator find(const Key &key) const

- const T value(const Key &key) const

  返回与key关联的值。
  如果哈希表中不包含带有key的项目，则该函数将返回默认构造的值。 如果哈希中有多个项，则返回最近插入的项的值。

- const T value(const Key &key, const T &defaultValue) const

- QList<T> values() const

  以**任意顺序**返回包含哈希值中所有值的列表。 如果一个键与多个值相关联，则其所有值都将在列表中，而不仅仅是最近插入的一个。
  *该顺序保证与keys（）使用的顺序相同*。

- const Key key(const T &value) const

  返回映射到key的第一个键。
  如果散列中不包含带有该key的项目，则该函数返回默认构造的键。
  此功能可能很慢（线性时间），因为QHash的内部数据结构已针对通过键而不是通过值进行快速查找进行了优化。

- const Key key(const T &value, const Key &defaultKey) const

- QList<Key> keys() const

  返回以**任意顺序**包含哈希中所有键的列表。 在哈希中多次出现的键（因为该方法在QMultiHash上操作）在列表中也多次出现。
  *该顺序保证与values（）使用的顺序相同*。

- QList<Key> keys(const T &value) const

  返回一个列表，该列表以任意顺序包含与value值关联的所有键。
  此功能可能很慢（线性时间），因为QHash的内部数据结构已针对通过键而不是通过值进行快速查找进行了优化。

- QHash::key_iterator keyBegin() const

  返回一个STL样式的迭代器，该迭代器指向哈希中的第一个条目。

- QHash::key_iterator keyEnd() const

  返回一个STL样式的迭代器，该迭代器指向哈希中的最后一个条目。

- QHash::key_value_iterator keyValueBegin()

  返回指向哈希表中第一个条目的const STL样式迭代器。

- QHash::key_value_iterator keyValueEnd()

  返回指向哈希表中最后一个条目的const STL样式迭代器。

- QHash::const_iterator constFind(const Key &key) const

  返回一个哈希值指向该项目的迭代器。
  如果哈希表中不包含带有key的项，则该函数返回constEnd（）。

- QPair<QHash::iterator, QHash::iterator> equal_range(const Key &key)

  返回一对迭代器，该迭代器定义存储在key下的值范围（first，second）。 如果范围为空，则两个迭代器都将等于end（）。

- QPair<QHash::const_iterator, QHash::const_iterator> equal_range(const Key &key) const

### 2.5.构造析构

- QHash(InputIterator begin, InputIterator end)
- QHash(QHash<K, V> &&other)
- QHash(const QHash<K, V> &other)
- QHash(std::initializer_list<std::pair<Key, T> > list)
- QHash()
- ~QHash()

### 2.6.迭代器

- QHash::iterator begin()
- QHash::const_iterator begin() const
- QHash::iterator end()
- QHash::const_iterator end() const
- QHash::const_iterator cbegin() const
- QHash::const_iterator cend() const
- QHash::const_iterator constBegin() const
- QHash::const_iterator constEnd() const
- QHash::const_key_value_iterator keyValueBegin() const
- QHash::const_key_value_iterator keyValueEnd() const
- QHash::const_key_value_iterator constKeyValueBegin() const
- QHash::const_key_value_iterator constKeyValueEnd() const

### 2.7.运算符

- QHash<K, V> &operator=(QHash<K, V> &&other)
- QHash<K, V> &operator=(const QHash<K, V> &other)
- bool operator!=(const QHash<K, V> &other) const
- bool operator==(const QHash<K, V> &other) const
- T &operator[](const Key &key)
- const T operator[](const Key &key) const

## 3.Related Non-Members

- int qGlobalQHashSeed()

  返回当前的全局QHash种子。
  种子设置在任何新创建的QHash中。 

- uint qHash(const QSslDiffieHellmanParameters &dhparam, uint seed)

  将此QSslDiffieHellmanParameters与其他交换。 此功能非常快捷，不会失败。

- uint qHash(const QUrl &url, uint seed = 0)

  返回URL的哈希值。 如果指定，则使用seed初始化哈希。

- uint qHash(const QOcspResponse &response, uint seed)

- uint qHash(const QHash<Key, T> &key, uint seed = 0)

- uint qHash(const QBitArray &key, uint seed = 0)

- uint qHash(char key, uint seed = 0)

- uint qHash(const QDateTime &key, uint seed = 0)

- uint qHash(QSslEllipticCurve curve, uint seed)

- uint qHash(QLatin1String key, uint seed = 0)

- uint qHash(uchar key, uint seed = 0)

- uint qHash(const QDate &key, uint seed = 0)

- uint qHash(signed char key, uint seed = 0)

- uint qHash(const QTime &key, uint seed = 0)

- uint qHash(const QSet<T> &key, uint seed = 0)

- uint qHash(const T *key, uint seed = 0)

- uint qHash(ushort key, uint seed = 0)

- uint qHash(short key, uint seed = 0)

- uint qHash(uint key, uint seed = 0)

- uint qHash(const QPair<T1, T2> &key, uint seed = 0)

- uint qHash(int key, uint seed = 0)

- uint qHash(const std::pair<T1, T2> &key, uint seed = 0)

- uint qHash(const QVersionNumber &key, uint seed = 0)

- uint qHash(ulong key, uint seed = 0)

- uint qHash(long key, uint seed = 0)

- uint qHash(quint64 key, uint seed = 0)

- uint qHash(qint64 key, uint seed = 0)

- uint qHash(float key, uint seed = 0)

- uint qHash(double key, uint seed = 0)

- uint qHash(long double key, uint seed = 0)

- uint qHash(const QChar key, uint seed = 0)

- uint qHash(const QByteArray &key, uint seed = 0)

- uint qHash(const QString &key, uint seed = 0)

- uint qHash(const QStringRef &key, uint seed = 0)

- uint qHashBits(const void *p, size_t len, uint seed = 0)

  返回由p指向的大小为len的内存块的哈希值，使用种子来为计算提供种子。
  仅将此功能用于为您自己的自定义类型实现qHash（）。 例如，这是为std :: vector <int>实现qHash（）重载的方法：

  ```c++
   inline uint qHash(const std::vector<int> &key, uint seed = 0)
   {
       if (key.empty())
           return seed;
       else
           return qHashBits(&key.front(), key.size() * sizeof(int), seed);
   }
  ```

  这利用了std :: vector连续布置其数据这一事实。 如果不是这种情况，或者所包含的类型具有填充，则应该改用qHashRange（）。
  需要重复的是，qHashBits（）的实现（如Qt提供的qHash（）重载）可能随时更改。 您不能依赖于这样的事实，即qHashBits（）在不同的Qt版本中将给出相同的结果（对于相同的输入）。

- uint qHashRange(InputIterator first, InputIterator last, uint seed = 0)

  通过将qHash（）依次应用于每个元素并将哈希值合并为一个值，使用种子将计算的种子返回到[first，last）范围的哈希值。
  此函数的返回值取决于范围中元素的顺序。 那意味着[0,1,2]和[1,2,0]将返回不同的哈希值。如果顺序无关紧要，例如哈希表，则使用qHashRangeCommutative（）。 如果要哈希原始内存，请使用qHashBits（）。

  **仅将此功能用于为您自己的自定义类型实现qHash（）**。 例如，这是为std :: vector <int>实现qHash（）重载的方法：

  ```c++
   inline uint qHash(const std::vector<int> &key, uint seed = 0)
   {
       return qHashRange(key.begin(), key.end(), seed);
   }
  ```

  需要重复的是，qHashRange（）的实现（如Qt提供的qHash（）重载）可能随时更改。 即使元素类型的qHash（）可以使用，您也不能依赖qHashRange（）在不同的Qt版本上会给出相同的结果（对于相同的输入）。

- uint qHashRangeCommutative(InputIterator first, InputIterator last, uint seed = 0)

  子返回到[first，last）范围的哈希值。
  此函数的返回值取决于范围中元素的顺序。 那意味着[0,1,2]和[1,2,0]将返回不同的哈希值。如果顺序很重要，例如对于向量和数组，请改用qHashRange（）。 如果要哈希原始内存，请使用qHashBits（）。

  **仅将此功能用于为您自己的自定义类型实现qHash（）**。 例如，这是为std :: unordered_set <int>实现qHash（）重载的方法：

  ```c++
  inline uint qHash(const std::unordered_set<int> &key, uint seed = 0)
  {
      return qHashRangeCommutative(key.begin(), key.end(), seed);
  }
  ```

  需要重申的是，qHashRangeCommutative（）的实现（如Qt提供的qHash（）重载）可能随时更改。 即使元素类型的qHash（）也可以，qHashRangeCommutative（）可以在不同的Qt版本中提供相同的结果（对于相同的输入），这一点绝对不能依赖。

- void qSetGlobalQHashSeed(int newSeed)

  将全局QHash种子设置为newSeed。
  当需要对QHash进行确定性和可重现的行为时，应仅出于测试和调试目的而手动设置全局QHash种子值。 我们不建议在生产代码中执行此操作，因为它会使您的应用程序容易受到算法复杂性攻击。
  从Qt 5.10起，唯一允许的值为0和-1。 传递值-1会将全局QHash种子重新初始化为随机值，而值0则用于请求C ++基本类型类型（如int）和字符串类型（QString，QByteArray）的稳定算法。
  种子设置在任何新创建的QHash中。 
  如果设置了环境变量QT_HASH_SEED，则调用此函数将导致无操作。

- QDataStream &operator<<(QDataStream &out, const QHash<Key, T> &hash)

- QDataStream &operator>>(QDataStream &in, QHash<Key, T> &hash)

## 4.Detailed Description

QHash <Key，T>是Qt的通用容器类之一。它存储（键，值）对，并提供与键关联的值的快速查找。
QHash提供与QMap非常相似的功能。不同之处在于：

- QHash提供比QMap更快的查找。 （有关详细信息，请参见算法复杂度。）
- 在QMap上进行迭代时，项始终按键排序。使用QHash，项目任意排序。
- QMap的键类型必须提供operator <（）。 QHash的键类型必须提供operator ==（）和称为qHash（）的全局哈希函数（请参阅qHash）。

### qHash（）哈希函数
QHash的键类型除了是可分配的数据类型外，还具有其他要求：它必须提供operator ==（），并且该类型的名称空间中还必须有一个qHash（）函数，该函数返回键类型的参数的哈希值。

qHash（）函数根据一个键计算一个数值。只要给定相同的参数，它总是返回相同的值，它就可以使用任何可以想象的算法。换句话说，如果e1 == e2，则qHash（e1）== qHash（e2）也必须成立。但是，为了获得良好的性能，qHash（）函数应尝试尽可能最大程度地为不同的键返回不同的哈希值。

**对于密钥类型K，qHash函数必须具有以下签名之一**：

```c++
 uint qHash(K key);
 uint qHash(const K &key);

 uint qHash(K key, uint seed);
 uint qHash(const K &key, uint seed);
```

包含两个参数的重载采用一个无符号整数，该整数应用于散列哈希函数的计算。 QHash提供此种子是为了防止一系列算法复杂性攻击。 如果为键类型同时定义了一个参数的重载和两个参数的重载，则QHash将使用后者（请注意，您可以简单地定义两个参数的版本，并使用默认值作为seed参数）。

这是可以用作QHash中的键的C ++和Qt类型的部分列表：任何整数类型（char，unsigned long等），任何指针类型，QChar，QString和QByteArray。 对于所有这些，<QHash>标头定义了一个qHash（）函数，该函数计算适当的哈希值。 许多其他Qt类也为其类型声明了qHash重载。 请参阅每个课程的文档。
如果要使用其他类型作为键，请确保提供operator ==（）和qHash（）实现。

```c++
 #ifndef EMPLOYEE_H
 #define EMPLOYEE_H

 class Employee
 {
 public:
     Employee() {}
     Employee(const QString &name, QDate dateOfBirth);
     ...

 private:
     QString myName;
     QDate myDateOfBirth;
 };

 inline bool operator==(const Employee &e1, const Employee &e2)
 {
     return e1.name() == e2.name()
            && e1.dateOfBirth() == e2.dateOfBirth();
 }

 inline uint qHash(const Employee &key, uint seed)
 {
     return qHash(key.name(), seed) ^ key.dateOfBirth().day();
 }

 #endif // EMPLOYEE_H
```

在上面的示例中，我们依靠Qt的全局qHash（const QString＆，uint）为我们提供员工姓名的哈希值，并在他们出生的那一天对其进行XOR处理，以帮助为具有相同名称的人生成唯一的哈希。
请注意，Qt提供的qHash（）重载的实现可能随时更改。 您不能依赖于这样的事实，即qHash（）在不同的Qt版本之间会给出相同的结果（对于相同的输入）。

### Algorithmic complexity attacks

所有哈希表都容易受到特定类别的拒绝服务攻击的攻击，在这种拒绝服务攻击中，攻击者会仔细预先计算将要在哈希表的同一存储桶中哈希的一组不同的密钥（甚至具有完全相同的哈希值）。攻击旨在将数据馈入表时获得最坏情况的算法行为（用O（n）而不是摊销的O（1），有关详细信息，请参见算法复杂性）。
为了避免出现这种最坏情况的行为，可以使用随机种子对qHash（）进行的哈希值计算进行加密(salted)，从而使攻击的范围无效。该种子由QHash每个进程自动生成一次，然后由QHash传递，作为qHash（）函数的两个参数重载的第二个参数。
QHash的这种随机化默认情况下处于启用状态。即使程序从不应该依赖于特定的QHash顺序，在某些情况下，您有时还是需要确定性的行为，例如用于调试或回归测试。要禁用随机化，请将环境变量QT_HASH_SEED定义为值为0。或者，可以调用值为0的qSetGlobalQHashSeed（）函数。