# QXmlContentHandler

## 1.Public Functions

- `virtual	~QXmlContentHandler ()`

- `virtual void	setDocumentLocator ( QXmlLocator * locator ) = 0`

  reader在**开始解析文档之前调用此函数**。 参数定位符是指向QXmlLocator的指针，该指针允许应用程序获取文档中的解析位置。

  不要破坏定位器； 当销毁阅读器时，销毁它。 （请勿在读取器损坏后使用定位器）。

- `virtual bool	characters ( const QString & ch ) = 0`

- `virtual bool	startDocument () = 0`

  阅读器开始解析文档时会调用此函数。 读者在调用setDocumentLocator（）之后，在此类或QXmlDTDHandler类中的任何其他函数被调用之前，仅调用一次此函数。

  如果此函数返回false，则阅读器停止解析并报告错误。 读者使用函数errorString（）获取错误消息。

- `virtual bool	startElement ( const QString & namespaceURI, const QString & localName, const QString & qName, const QXmlAttributes & atts ) = 0`

  读取器在解析开始元素标签后调用此函数。

  读取相应的结束元素标记时，将进行相应的endElement（）调用。 startElement（）和endElement（）调用始终正确嵌套。**空元素标签（例如<x />）会导致startElement（）调用紧随endElement（）调用**。

  提供的属性列表仅包含具有显式值的属性。仅当阅读器的namespace-prefix属性为true时，属性列表才包含用于名称空间声明的属性（即以xmlns开头的属性）。

  参数namespaceURI是名称空间URI，如果元素没有名称空间URI或未完成名称空间处理，则为空字符串。 **localName是本地名称（不带前缀）**，如果未执行任何名称空间处理，则为空字符串，**qName是限定名称（带前缀）**，atts是附加到元素的属性。如果没有属性，则atts为空属性对象。

  如果此函数返回false，则阅读器停止分析并报告错误。读者使用函数errorString（）获取错误消息。

- `virtual bool	startPrefixMapping ( const QString & prefix, const QString & uri ) = 0`

  读者调用此函数来**表示前缀URI名称空间映射范围的开始**。 对于正常的名称空间处理，此信息不是必需的，因为阅读器会自动替换元素和属性名称的前缀。

  请注意，不能保证startPrefixMapping（）和endPrefixMapping（）调用相对于彼此正确嵌套：所有startPrefixMapping（）事件在相应的startElement（）事件之前发生，所有endPrefixMapping（）事件在相应的endElement（）事件之后发生。 ，但不能保证它们的顺序。

  参数前缀是要声明的名称空间前缀，参数uri是前缀映射到的名称空间URI。

  如果此函数返回false，则阅读器停止解析并报告错误。 读者使用函数errorString（）获取错误消息。

- `virtual bool	endDocument () = 0`

- `virtual bool	endElement ( const QString & namespaceURI, const QString & localName, const QString & qName ) = 0`

- `virtual bool	endPrefixMapping ( const QString & prefix ) = 0`

- `virtual QString	errorString () const = 0`

  阅读器调用此函数以获取错误字符串，例如 如果任何处理程序函数返回false。

- `virtual bool	ignorableWhitespace ( const QString & ch ) = 0`

  一些读者可能会使用此功能来报告元素内容中的**每个空白**。 空格以ch报告。

  如果此函数返回false，则阅读器停止解析并报告错误。 读者使用函数errorString（）获取错误消息。

- `virtual bool	processingInstruction ( const QString & target, const QString & data ) = 0`

- `virtual bool	skippedEntity ( const QString & name ) = 0`

  如果某些reader没有看到声明，则可能会跳过实体（例如，因为它们在外部DTD中）。 如果这样做，他们报告说他们通过调用此函数跳过了名为name的实体。

  如果此函数返回false，则阅读器停止解析并报告错误。 读者使用函数errorString（）获取错误消息。

## 2.Detailed Description

QXmlContentHandler类提供了一个接口来**报告XML数据的逻辑内容**。

**如果需要通知应用程序基本的解析事件，则可以实现此接口并使用QXmlReader :: setContentHandler（）激活它**。然后，读者可以通过此界面报告与文档相关的基本事件，例如元素的开始和结束以及字符数据。

此界面中事件的顺序非常重要，它反映了文档本身中信息的顺序。例如，所有元素的内容（字符数据，处理指令和子元素）按顺序显示在startElement（）事件和相应的endElement（）事件之间。

QXmlDefaultHandler类为该接口提供了默认实现。如果只想知道某些解析事件，则从QXmlDefaultHandler类的子类化非常方便。

在文档的开头调用startDocument（）函数，在文档的结尾调用endDocument（）。**在开始分析之前，将调用setDocumentLocator（）**。对于每个元素，将调用startElement（），并在每个元素的末尾调用endElement（）。用字符数据块调用character（）函数； ignorableWhitespace（）与大块空白一起调用，processingInstruction（）与处理指令一起调用。如果跳过实体，则将调用skippedEntity（）。在前缀URI范围的开头，将调用startPrefixMapping（）。