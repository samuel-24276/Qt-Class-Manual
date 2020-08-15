# QSqlDatabase

# 1.Detailed Description

QSqlDatabase类提供了用于通过连接访问数据库的接口。 QSqlDatabase的实例(instance)表示连接。该连接通过受支持的数据库驱动程序之一（从QSqlDriver派生）提供对数据库的访问。或者，您可以从QSqlDriver继承您自己的数据库驱动程序。
通过调用静态`addDatabase（）`函数创建连接（即QSqlDatabase的实例），在**其中您指定要使用的驱动程序或驱动程序类型（取决于数据库的类型）和连接名称**。通过连接本身的名称而不是通过连接数据库的名称来知道连接。您可以与一个数据库建立多个连接。 QSqlDatabase还支持默认连接的概念，即未命名的连接。若要创建默认连接，请在调用addDatabase（）时不要传递连接名称参数。随后，如果您在不指定连接名称的情况下调用任何静态成员函数，则将采用默认连接。以下代码段显示了如何创建和打开与PostgreSQL数据库的默认连接：

```c++
QSqlDatabase db=QSqlDatabase::addDatabase("QPSQL");
db.setHostName("acidalia");
db.setDatabaseName("customdb");
db.setUserName("mojito");
db.setPassword("J0a1m8");
bool ok = db.open();
```

QSqlDatabase是一个value class。**通过一个QSqlDatabase实例对数据库连接所做的更改将影响代表相同连接的其他QSqlDatabase实例**。使用cloneDatabase（）基于现有的数据库连接创建独立的数据库连接。
**警告：强烈建议您不要保留QSqlDatabase的副本作为类的成员，因为这将导致实例在关闭时无法正确清理。**如果需要访问现有的QSqlDatabase，则应使用database（）访问它。如果选择使用QSqlDatabase成员变量，则需要在删除QCoreApplication实例之前将其删除，否则可能导致未定义的行为。

# 2.Some utility methods:

- tables()
  returns the list of tables
- primaryIndex()
  returns a table's primary index
- record()
  returns meta-information about a table's fields
- transaction()
  starts a transaction
- commit()
  saves and completes a transaction
- rollback()
  cancels a transaction
- hasFeature()
  checks if a driver supports transactions
- lastError()
  returns information about the last error
- drivers()
  returns the names of the available SQL drivers
- isDriverAvailable()
  checks if a particular driver is available
- registerSqlDriver()
  registers a custom-made driver

注意：使用事务(transaction)时，必须在创建查询之前启动事务。



多线程里使用数据库操作，容易出现以下错误：

```
QSqlDatabasePrivate::database: requested database does not belong to the calling thread.
QSqlQuery::prepare: database not open
```

意思是请求的数据库不属于调用线程， 子线程调用主线程创建的数据库连接 ，数据库未打开。

解决方法：将数据库的创建、表的创建放在主线程（如构造函数）里，在子线程里打开连接，执行一系列操作后关闭数据库连接即可。这样只有一个连接，节省资源。

`[static] QSqlDatabase QSqlDatabase::addDatabase(const QString &type, const QString &connectionName = QLatin1String(defaultConnection))`

使用driver type和连接名称connectionName将数据库添加到数据库连接列表中。如果已经存在一个名为connectionName的数据库连接，则将删除该连接。

数据库连接由connectionName引用。 返回新添加的数据库连接。
如果type不可用或无法加载，则isValid（）返回false。
如果未指定connectionName，则新连接将成为应用程序的默认连接，并且随后对不带连接名称参数的database（）的调用将返回默认连接。 如果此处提供了connectionName，请使用database（connectionName）检索连接。



