# QXmlReader

继承者： QXmlSimpleReader

## 1.Public Functions

- virtual	~QXmlReader ()
- virtual QXmlDTDHandler *	DTDHandler () const = 0
- virtual QXmlContentHandler *	contentHandler () const = 0
- virtual QXmlDeclHandler *	declHandler () const = 0
- virtual QXmlEntityResolver *	entityResolver () const = 0
- virtual QXmlErrorHandler *	errorHandler () const = 0
- virtual bool	feature ( const QString & name, bool * ok = 0 ) const = 0
- virtual bool	hasFeature ( const QString & name ) const = 0
- virtual bool	hasProperty ( const QString & name ) const = 0
- virtual QXmlLexicalHandler *	lexicalHandler () const = 0
- virtual bool	parse ( const QXmlInputSource * input ) = 0
- virtual void *	property ( const QString & name, bool * ok = 0 ) const = 0
- virtual void	setContentHandler ( QXmlContentHandler * handler ) = 0
- virtual void	setDTDHandler ( QXmlDTDHandler * handler ) = 0
- virtual void	setDeclHandler ( QXmlDeclHandler * handler ) = 0
- virtual void	setEntityResolver ( QXmlEntityResolver * handler ) = 0
- virtual void	setErrorHandler ( QXmlErrorHandler * handler ) = 0
- virtual void	setFeature ( const QString & name, bool value ) = 0
- virtual void	setLexicalHandler ( QXmlLexicalHandler * handler ) = 0
- virtual void	setProperty ( const QString & name, void * value ) = 0

## 2.Detailed Description

QXmlReader类为XML阅读器（即解析器）提供了一个接口。

这个抽象类为Qt的所有XML读取器提供了一个接口。当前，Qt的XML模块中仅包含一种阅读器的实现：QXmlSimpleReader。在将来的版本中，可能会有更多具有不同属性的阅读器（例如，验证解析器）。

XML类的设计遵循SAX2 Java接口，其名称适用于Qt命名约定。对于使用SAX2的任何人来说，开始使用Qt XML类都应该非常容易。

**所有阅读器都使用QXmlInputSource类读取输入文档。由于通常您对XML文档中的特定内容感兴趣，因此阅读器通过特殊的处理程序类（QXmlDTDHandler，QXmlDeclHandler，QXmlContentHandler，QXmlEntityResolver，QXmlErrorHandler和QXmlLexicalHandler）报告内容，如果要处理内容，则必须将其子类化**。

由于处理程序类仅描述接口，因此必须实现所有功能。我们提供了QXmlDefaultHandler类来简化此过程：它为所有函数实现了默认行为（不执行任何操作），因此您可以将其子类化，而仅实现您感兴趣的函数。

可以分别通过setFeature（）和setProperty（）设置阅读器的功能和属性。您可以将阅读器设置为通过setEntityResolver（），setDTDHandler（），setContentHandler（），setErrorHandler（），setLexicalHandler（）和setDeclHandler（）使用自己的子类。解析本身以对parse（）的调用开始。