# QXmlDTDHandler

继承者：QXmlDefaultHandler

## 1.Public Functions

- virtual	~QXmlDTDHandler ()

- virtual QString	errorString () const = 0

  如果任何处理程序函数返回false，则读者将调用此函数以获取错误字符串。

- virtual bool	notationDecl ( const QString & name, const QString & publicId, const QString & systemId ) = 0

  读者在解析符号声明时调用此函数。

  参数名称是符号名称，publicId是符号的公共标识符，systemId是符号的系统标识符。

  如果此函数返回false，则阅读器停止解析并报告错误。 读者使用函数errorString（）获取错误消息。

- virtual bool	unparsedEntityDecl ( const QString & name, const QString & publicId, const QString & systemId, const QString & notationName ) = 0

  读者在找到未解析的实体声明时调用此函数。

  参数名称是未解析实体的名称，publicId是实体的公共标识符，systemId是实体的系统标识符，notationName是关联符号的名称。

  如果此函数返回false，则阅读器停止解析并报告错误。 读者使用函数errorString（）获取错误消息。

## 2.Detailed Description

QXmlDTDHandler类提供了一个接口，用于报告XML数据的DTD内容。

如果应用程序需要有关符号和未解析实体的信息，则可以实现此接口并向QXmlReader :: setDTDHandler（）注册实例。

请注意，此接口仅包含XML建议要求处理器报告的DTD事件，即分别使用notationDecl（）和unparsedEntityDecl（）的符号和未解析的实体声明。