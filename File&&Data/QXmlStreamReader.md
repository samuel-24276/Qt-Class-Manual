# QXmlStreamReader

Qt 4具有三个不同的XML解析器：

- QDomDocument——DOM解析器,QtXML的一部分
- QXmlSimpleReader——推送(事件)解析器,是QtXML的一部分
- **QXmlStreamReader**——**Pull解析器**,是QtCore的一部分,**现在是推荐的解析器**

## 1.Public Types

- Error { NoError, CustomError, NotWellFormedError, PrematureEndOfDocumentError, UnexpectedElementError }

- enum	ReadElementTextBehaviour { ErrorOnUnexpectedElement, IncludeChildElements, SkipChildElements }

- enum	TokenType { NoToken, Invalid, StartDocument, EndDocument, ..., ProcessingInstruction }

  | Constant                                | Value | Description                                                  |
  | --------------------------------------- | ----- | ------------------------------------------------------------ |
  | QXmlStreamReader::NoToken               | 0     | 读者尚未阅读任何内容。                                       |
  | QXmlStreamReader::Invalid               | 1     | 发生错误，报告为error（）和errorString（）。                 |
  | QXmlStreamReader::StartDocument         | 2     | 读者在documentVersion（）中报告XML版本号，并在documentEncoding（）中报告XML文档中指定的编码。 如果文档被声明为独立文档，则isStandaloneDocument（）返回true； 否则返回false。 |
  | QXmlStreamReader::EndDocument           | 3     | 读者报告文档的结尾。                                         |
  | QXmlStreamReader::StartElement          | 4     | 读者可以使用namespaceUri（）和name（）报告元素的开始。 空元素也报告为StartElement，然后直接报告为EndElement。 可以调用便捷功能readElementText（）来连接所有内容，直到对应的EndElement。 属性在attribute（）中报告，在namespaceDeclarations（）中报告名称空间。 |
  | QXmlStreamReader::EndElement            | 5     | 读者使用namespaceName Uri（）和name（）报告元素的结尾。      |
  | QXmlStreamReader::Characters            | 6     | 读者报告text（）中的字符。 如果字符都是空白，则isWhitespace（）返回true。 如果字符来自CDATA节，则isCDATA（）返回true。 |
  | QXmlStreamReader::Comment               | 7     | 读者在text（）中报告comment。                                |
  | QXmlStreamReader::DTD                   | 8     | 读者在text（）中报告DTD，在notationDeclarations（）中报告符号声明，并在EntityDeclarations（）中报告实体声明。 DTD声明的详细信息在dtdName（），dtdPublicId（）和dtdSystemId（）中报告。 |
  | QXmlStreamReader::EntityReference       | 9     | 读者报告无法解析的实体引用。 引用的名称在name（）中报告，替换文本在text（）中报告。 |
  | QXmlStreamReader::ProcessingInstruction | 10    | 读取器在processingInstructionTarget（）和processingInstructionData（）中报告一条处理指令。 |

  

## 2.Properties

- namespaceProcessing : bool

  流读取器的名称空间处理标志

  此属性控制流读取器是否处理名称空间。 如果启用，则读取器处理名称空间，否则不处理。

  默认情况下，启用名称空间处理。

## 3.Public Functions

- **`void	setDevice ( QIODevice * device )`**

  将当前设备设置为device 。 设置设备会将流重置为其初始状态。

- QXmlStreamReader ()

- QXmlStreamReader ( QIODevice * device )

- QXmlStreamReader ( const QByteArray & data )

- QXmlStreamReader ( const QString & data )

- QXmlStreamReader ( const char * data )

- ~QXmlStreamReader ()

- **`void	addData ( const QByteArray & data )`**

  添加更多数据供读者阅读。 如果阅读器具有device（），则此函数不执行任何操作。

- void	addData ( const QString & data )

- void	addData ( const char * data )

- void	addExtraNamespaceDeclaration ( const 

- QXmlStreamNamespaceDeclaration & extraNamespaceDeclaration )

- void	addExtraNamespaceDeclarations ( const QXmlStreamNamespaceDeclarations & extraNamespaceDeclarations )

- bool	atEnd () const
  QXmlStreamAttributes	attributes () const

- qint64	characterOffset () const

- void	clear ()

- qint64	columnNumber () const

- QIODevice *	device () const

- QStringRef	documentEncoding () const

- QStringRef	documentVersion () const

- QStringRef	dtdName () const

- QStringRef	dtdPublicId () const

- QStringRef	dtdSystemId () const

- QXmlStreamEntityDeclarations	entityDeclarations () const

- QXmlStreamEntityResolver *	entityResolver () const
  Error	error () const

- QString	errorString () const

- bool	hasError () const

- bool	isCDATA () const

- bool	isCharacters () const

- bool	isComment () const

- bool	isDTD () const

- bool	isEndDocument () const

- bool	isEndElement () const

- bool	isEntityReference () const

- bool	isProcessingInstruction () const

- bool	isStandaloneDocument () const

- bool	isStartDocument () const

- bool	isStartElement () const

  如果tokenType（）等于StartElement，则返回true；否则返回false。

- bool	isWhitespace () const

- qint64	lineNumber () const

- QStringRef	name () const

- QXmlStreamNamespaceDeclarations	namespaceDeclarations () const

- bool	namespaceProcessing () const

- QStringRef	namespaceUri () const

- QXmlStreamNotationDeclarations	notationDeclarations () const

- QStringRef	prefix () const

- QStringRef	processingInstructionData () const

- QStringRef	processingInstructionTarget () const

- QStringRef	qualifiedName () const

- void	raiseError ( const QString & message = QString() )

- QString	readElementText ( ReadElementTextBehaviour behaviour )

- QString	readElementText ()

- TokenType	readNext ()

- bool	readNextStartElement ()

- void	setEntityResolver ( QXmlStreamEntityResolver * resolver )

- void	setNamespaceProcessing ( bool )

- void	skipCurrentElement ()

- QStringRef	text () const

- QString	tokenString () const

- TokenType	tokenType () const