# QXmlQuery

## 1.Public Types

- enum	QueryLanguage { XQuery10, XSLT20 }

## 2.Public Functions

- `QXmlQuery ()`

- `QXmlQuery ( const QXmlQuery & other )`

- `QXmlQuery ( const QXmlNamePool & np )`

- `QXmlQuery ( QueryLanguage queryLanguage, const QXmlNamePool & np = QXmlNamePool() )`

- `~QXmlQuery ()`

- `void	bindVariable ( const QXmlName & name, const QXmlItem & value )`

  将变量名称绑定到值，以便可以在查询中使用$ name引用值。 名称不能为空。 name.isNull（）必须返回false。 如果名称已经被先前的bindVariable（）绑定，则其先前的绑定将被覆盖。 如果value为null，则value.isNull（）返回true，并且name已具有绑定，其作用是删除name的现有绑定。 要绑定QString或QUrl类型的值，请将值包装在QVariant中，以便调用QXmlItem的QVariant构造函数。 查询处理的所有字符串都必须是有效的XQuery字符串，这意味着它们必须仅包含XML 1.0字符。 但是，此要求未选中。 如果查询处理无效的字符串，则该行为是不确定的。

- `void	bindVariable ( const QXmlName & name, QIODevice * device )`

- `void	bindVariable ( const QXmlName & name, const QXmlQuery & query )`

- `void	bindVariable ( const QString & localName, const QXmlItem & value )`

- `void	bindVariable ( const QString & localName, QIODevice * device )`

- `void	bindVariable ( const QString & localName, const QXmlQuery & query )`

- `void	evaluateTo ( QXmlResultItems * result ) const`

- `bool	evaluateTo ( QAbstractXmlReceiver * callback ) const`

- `bool	evaluateTo ( QStringList * target ) const`

- `bool	evaluateTo ( QString * output ) const`

- `bool	evaluateTo ( QIODevice * target ) const`

- `QXmlName	initialTemplateName () const`

- `bool	isValid () const`

- `QAbstractMessageHandler *	messageHandler () const`

- `QXmlNamePool	namePool () const`

- `QNetworkAccessManager *	networkAccessManager () const`

- `QueryLanguage	queryLanguage () const`

- `void	setFocus ( const QXmlItem & item )`

- `bool	setFocus ( const QUrl & documentURI )`

- `bool	setFocus ( QIODevice * document )`

- `bool	setFocus ( const QString & focus )`

- `void	setInitialTemplateName ( const QXmlName & name )`

- `void	setInitialTemplateName ( const QString & localName )`

- `void	setMessageHandler ( QAbstractMessageHandler * aMessageHandler )`

- `void	setNetworkAccessManager ( QNetworkAccessManager * newManager )`

- `void	setQuery ( QIODevice * sourceCode, const QUrl & documentURI = QUrl() )`

- `void	setQuery ( const QUrl & queryURI, const QUrl & baseURI = QUrl() )`

- `void	setQuery ( const QString & sourceCode, const QUrl & documentURI = QUrl() )`

- `void	setUriResolver ( const QAbstractUriResolver * resolver )`

- `const QAbstractUriResolver *	uriResolver () const`

- `QXmlQuery &	operator= ( const QXmlQuery & other )`

## 3.Detailed Description

QXmlQuery类对XML数据或建模看起来像XML的非XML数据执行XQueries。 QXmlQuery类编译并执行以XQuery语言编写的查询。 QXmlQuery通常用于查询XML数据，但它也可以查询已建模为XML的非XML数据。 像下面的代码片段一样，使用QXmlQuery查询XML数据很简单，因为它可以使用内置XML数据模型作为对基础查询引擎的委托来遍历数据。 内置数据模型在XQuery 1.0和XPath 2.0数据模型中指定。

```c++
 QXmlQuery query;
 query.setQuery("doc('index.html')/html/body/p[1]");

 QXmlSerializer serializer(query, myOutputDevice);
 query.evaluateTo(&serializer);
```

该示例使用QXmlQuery来匹配XML文档的第一段，然后将结果作为XML输出到设备。 使用QXmlQuery查询非XML数据需要编写QAbstractXmlNodeModel的子类，以替代内置XML数据模型。 自定义数据模型将能够按照QAbstractXmlNodeModel接口的要求遍历非XML数据。 然后，此定制数据模型的实例成为查询引擎用于遍历非XML数据的委托。 有关如何使用QXmlQuery查询非XML数据的示例，请参见QAbstractXmlNodeModel的文档。

### 3.1.Running XQueries

要运行使用QXmlQuery设置的查询，请调用评估功能之一。

- 使用指向XML接收器的指针来调用evaluateTo（QAbstractXmlReceiver *），该接收器以一系列回调的形式接收查询结果。 接收者回调类类似于用于转换SAX解析器的输出的回调类。 例如，QXmlSerializer是一个接收器回调类，用于转换回调序列以输出为未格式化的XML文本。
- 使用指向迭代器的指针来调用evaluateTo（QXmlResultItems *），该迭代器用于查询结果项的空序列。 类似Java的迭代器允许顺序访问查询结果。 
- evaluateTo（QStringList *）类似于evaluateTo（QXmlResultItems *），但是查询必须计算为字符串序列。

### 3.2.Running XPath Expressions

XPath语言是XQuery语言的子集，因此运行XPath表达式与运行XQuery查询相同。 使用setQuery（）将XPath表达式传递给QXmlQuery。

### 3.3.Running XSLT stylesheets

运行XSLT样式表与运行XQuery相似，不同之处在于，在构造QXmlQuery时，必须传递QXmlQuery :: XSLT20来告诉QXmlQuery将来自setQuery（）的内容解释为XSLT样式表而不是XQuery。 您还必须通过调用setFocus（）来设置输入文档。

```c++
     QXmlQuery query(QXmlQuery::XSLT20);
     query.setFocus(QUrl("myInput.xml"));
     query.setQuery(QUrl("myStylesheet.xsl"));
     query.evaluateTo(out);
```

注意：当前，使用XSLT时，必须在setQuery（）之前调用setFocus（）。 运行XSLT样式表的另一种方法是使用xmlpatterns命令行实用程序。

```c++
xmlpatterns myStylesheet.xsl myInput.xml
```

注意：对于当前版本，应将XSLT支持视为实验性的。 有关详细信息，请参见XSLT一致性部分。 样式表参数使用bindVariable（）绑定。

### 3.4.Binding A Query To A Starting Node

当对XML数据运行查询时，如上面的代码片段所示，doc（）函数返回内置数据模型中的节点，查询评估将在该节点上开始。 但是，当在包含非XML数据的定制节点模型上运行查询时，必须调用bindVariable（）函数之一，以将变量名绑定到定制模型中的起始节点。 在XQuery文本中使用$ variable引用来访问定制模型中的起始节点。 不必在查询中声明外部变量名。 请参阅QAbstractXmlNodeModel文档中的示例。

### 3.5.Reentrancy and Thread-Safety

**QXmlQuery是可重入的，但不是线程安全的**。 使用QxmlQuery副本构造函数创建查询副本并多次运行同一查询是安全的。 在后台，QXmlQuery将尽可能地重用资源，例如打开的文件和已编译的查询。 但是在多个线程中使用相同的QXmlQuery实例并不安全。

### 3.6.Error Handling

查询评估期间可能会发生错误。 示例包括类型错误和文件加载错误。 发生错误时： 错误消息将发送到messageHandler（）。 QXmlResultItems :: hasError（）将返回true，或者evaluateTo（）将返回false； 评估结果不确定。

### 3.7.Resource Management

当查询运行时，它将解析文档，分配内部数据结构来保存它们，并且它可能会通过网络加载其他资源。 它会在可能的情况下重用这些分配的资源，以避免必须重新加载和重新解析它们。 调用setQuery（）时，查询文本将编译为内部数据结构并进行优化。 然后可以将优化的表单重新用于查询的多个评估。 由于编译和优化过程可能会很昂贵，因此应通过为每个查询文本使用单独的QXmlQuery实例来避免针对同一查询重复该过程。 解析文档后，其内部表示形式将保留在QXmlQuery实例中，并在多个QXmlQuery实例之间共享。 **必须先存在QCoreApplication实例，然后才能使用QXmlQuery**。

### 3.8.Event Handling

当QXmlQuery访问资源（例如，调用fn：doc（）加载文件或通过绑定变量访问设备）时，将使用事件循环，这意味着将处理事件。 **为了避免在QXmlQuery访问资源时处理事件，请在单独的线程中创建QXmlQuery实例**。