# QSqlDatabase

# 0.常见用法

以SQLite3举例：

- 1.建立数据库连接

  `addDatabase(const QString &type, const QString &connectionName = QLatin1String(defaultConnection))`

  type是数据库类型，常用的有：QSQLITE、QPSQL等，connectionName 是建立的当前连接的名字，不指定的话Qt会提供缺省值。如果进行多次数据库操作，最好指定连接的名字，否则会在程序控制台输出`QSqlDatabasePrivate::addDatabase: duplicate connection name 'qt_sql_default_connection'`的警告。为了防止连接名重复，最好使用有意义的连接名加`QTime::currentTime().toString("hh:mm:ss")`。

- 2.设置数据库名字`setDatabaseName()`，参数为数据库的具体路径，因为SQLite3是文件型数据库。

- 3.打开数据库，这里要进行判断，如果打开失败应该输出错误信息，否则进行其他操作。

- 4.建立关于该连接的查询QSqlQuery对象，有四种方法：

  - 以其他QSqlQuery对象为参数
  - 以数据库连接为参数，之后调用QSqlQuery对象的`prepare()`函数，参数为执行的查询语句，未知变量用问号代替；再借用QSqlQuery对象的`bindValue()函数，第一参数为变量在查询语句的位置，第二参数为变量的值；最后调用QSqlQuery对象的`exec()`函数执行该查询。
  - 以单个查询语句为第一参数，数据库连接为第二参数，可以用于建立表格table
  - 以QSqlResult指针为参数

- 5.关闭该连接`close()`

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

# QSqlQuery

# 1.Public Types

`enum BatchExecutionMode { ValuesAsRows, ValuesAsColumns }`，枚举类型，定义按行查询还是按列查询

# 2.Public Functions

- QSqlQuery(const QSqlQuery &other)
- QSqlQuery(QSqlDatabase db)
- QSqlQuery(const QString &query = QString(), QSqlDatabase db = QSqlDatabase())
- QSqlQuery(QSqlResult *result)
  QSqlQuery &operator=(const QSqlQuery &other)
- ~QSqlQuery()
- void addBindValue(const QVariant &val, QSql::ParamType paramType = QSql::In)
- int at() const
- void bindValue(const QString &placeholder, const QVariant &val, QSql::ParamType paramType = QSql::In)
- void bindValue(int pos, const QVariant &val, QSql::ParamType paramType = QSql::In)
- QVariant boundValue(const QString &placeholder) const
  QVariant boundValue(int pos) const
- QMap<QString, QVariant> boundValues() const
  void clear()
- const QSqlDriver *driver() const
- bool exec(const QString &query)
- bool exec()
- bool execBatch(QSqlQuery::BatchExecutionMode mode = ValuesAsRows)
- QString executedQuery() const
- void finish()
- bool first()
- bool isActive() const
- bool isForwardOnly() const
- bool isNull(int field) const
- bool isNull(const QString &name) const
- bool isSelect() const
- bool isValid() const
- bool last()
- QSqlError lastError() const
- QVariant lastInsertId() const
- QString lastQuery() const
- bool next()
- bool nextResult()
- int numRowsAffected() const
- QSql::NumericalPrecisionPolicy numericalPrecisionPolicy() const
- bool prepare(const QString &query)
- bool previous()
- QSqlRecord record() const
- const QSqlResult *result() const
- bool seek(int index, bool relative = false)
- void setForwardOnly(bool forward)
- void setNumericalPrecisionPolicy(QSql::NumericalPrecisionPolicy precisionPolicy)
- int size() const
- QVariant value(int index) const
- QVariant value(const QString &name) const

# 3.Detailed Description

QSqlQuery封装了从在QSqlDatabase上执行的SQL查询创建，导航和检索数据所涉及的功能。它可以用于执行DML（数据操作语言）语句，例如SELECT，INSERT，UPDATE和DELETE，以及DDL（数据定义语言）语句，例如CREATE TABLE。它也可以用于执行非标准SQL的特定于数据库的命令（例如PostgreSQL的SET DATESTYLE = ISO）。
成功执行的SQL语句将查询的状态设置为活动状态，以便`isActive（）`返回true。否则，查询的状态将设置为非活动状态。无论哪种情况，在执行新的SQL语句时，查询都位于无效记录上。**必须先将活动查询导航到有效记录（以便isValid（）返回true），然后才能检索值**。
对于某些数据库，如果在调用commit（）或rollback（）时存在作为SELECT语句的活动查询，则提交或回滚将失败。有关详细信息，请参见isActive（）。
使用以下功能执行记录导航：

- next()
- previous()
- first()
- last()
- seek()

这些功能允许程序员通过查询返回的记录向前，向后或任意移动。如果只需要向前移动结果（例如使用next（）），则可以使用setForwardOnly（），这将节省大量内存开销并提高某些数据库的性能。一旦将活动查询放置在有效记录上，就可以使用value（）检索数据。使用QVariants从SQL后端传输所有数据。
例如：

```c++
QSqlQuery query("SELECT country FROM artist");
while (query.next()) {
    QString country = query.value(0).toString();
    doSomething(country);
}
```

要访问查询返回的数据，请使用value（int）。 SELECT语句返回的数据中的每个字段都可以通过传递该字段在语句中的位置（从0开始）来访问。这使得使用SELECT *查询是不可取的，因为返回的字段的顺序是不确定的。
为了提高效率，没有按名称访问字段的功能（除非您使用带名称的预准备查询，如下所述）。 要将字段名称转换为索引，请使用record（）。indexOf（），例如：

```c++
QSqlQuery query("SELECT * FROM artist");
int fieldNo = query.record().indexOf("country");
    while (query.next()) {
        QString country = query.value(fieldNo).toString();
        doSomething(country);
}
```

**QSqlQuery支持准备好的查询执行以及参数值与占位符的绑定**。一些数据库不支持这些功能，因此对于这些数据库，Qt会仿真所需的功能。例如，Oracle和ODBC驱动程序具有适当的准备好的查询支持，而Qt则利用了它。但对于不支持此功能的数据库，Qt会自行实现此功能，例如通过在执行查询时用实际值替换占位符。使用numRowsAffected（）查找非SELECT查询影响了多少行，使用size（）查找SELECT检索了多少行。
Oracle数据库通过使用冒号名称语法（例如：name）来识别占位符。 ODBC只是使用？字符。 Qt支持两种语法，但限制是您不能在同一查询中混合使用它们。
您可以使用`boundValues（）`检索单个变量（映射）中所有字段的值。
注意：并非所有的SQL操作都支持绑定值。请参考数据库系统的文档以检查其可用性。

绑定值的方法
下面，我们提供使用四种不同绑定方法中的每一种的相同示例，以及将值绑定到存储过程的一个示例。

- 使用命名占位符的命名绑定：

  ```c++
  QSqlQuery query;
  query.prepare("INSERT INTO person (id, forename, surname) "
                "VALUES (:id, :forename, :surname)");
  query.bindValue(":id", 1001);
  query.bindValue(":forename", "Bart");
  query.bindValue(":surname", "Simpson");
  query.exec();
  ```

- 使用命名占位符的位置绑定：

  ```c++
  QSqlQuery query;
  query.prepare("INSERT INTO person (id, forename, surname) "
  "VALUES (:id, :forename, :surname)");
  query.bindValue(0, 1001);
  query.bindValue(1, "Bart");
  query.bindValue(2, "Simpson");
  query.exec();
  ```

- 使用位置占位符（版本1）绑定值：

  ```c++
  QSqlQuery query;
  query.prepare("INSERT INTO person (id, forename, surname) "
  "VALUES (?, ?, ?)");
  query.bindValue(0, 1001);
  query.bindValue(1, "Bart");
  query.bindValue(2, "Simpson");
  query.exec();
  ```

- 使用位置占位符（版本2）绑定值：

  ```c++
  QSqlQuery query;
  query.prepare("INSERT INTO person (id, forename, surname) "
  "VALUES (?, ?, ?)");
  query.addBindValue(1001);
  query.addBindValue("Bart");
  query.addBindValue("Simpson");
  query.exec();
  ```

- 将值绑定到存储过程：

  此代码调用一个称为AsciiToInt（）的存储过程，通过其in参数向其传递一个字符，并将其结果传递给out参数。

  ```c++
  QSqlQuery query;
  query.prepare("CALL AsciiToInt(?, ?)");
  query.bindValue(0, "A");
  query.bindValue(1, 0, QSql::Out);
  query.exec();
  int i = query.boundValue(1).toInt(); // i is 65
  ```

  请注意，未绑定的参数将保留其值。
  不完全支持使用return语句返回值或返回多个结果集的存储过程。 有关特定的详细信息，请参见SQL数据库驱动程序。
  警告：在创建QSqlQuery之前，您必须加载SQL驱动程序并打开连接。 同样，当查询存在时，连接必须保持打开状态。 否则，QSqlQuery的行为是不确定的。