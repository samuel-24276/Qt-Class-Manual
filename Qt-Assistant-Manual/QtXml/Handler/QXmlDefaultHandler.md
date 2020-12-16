# QXmlDefaultHandler

继承自以下几个处理类：

-  QXmlContentHandler
- QXmlErrorHandler
- QXmlDTDHandler
- QXmlEntityResolver
- QXmlLexicalHandler
- QXmlDeclHandler

## 1.Public Functions

- QXmlDefaultHandler ()
- virtual	~QXmlDefaultHandler ()

## 2.Reimplemented Public Functions

- virtual bool	attributeDecl ( const QString & eName, const QString & aName, const QString & type, const QString & valueDefault, const QString & value )
- virtual bool	characters ( const QString & ch )
- virtual bool	comment ( const QString & ch )
- virtual bool	startCDATA ()
- virtual bool	startDTD ( const QString & name, const QString & publicId, const QString & systemId )
- virtual bool	startDocument ()
- virtual bool	startElement ( const QString & namespaceURI, const QString & localName, const QString & qName, const QXmlAttributes & atts )
- virtual bool	startEntity ( const QString & name )
- virtual bool	startPrefixMapping ( const QString & prefix, const QString & uri )
- virtual bool	endCDATA ()
- virtual bool	endDTD ()
- virtual bool	endDocument ()
- virtual bool	endElement ( const QString & namespaceURI, const QString & localName, const QString & qName )
- virtual bool	endEntity ( const QString & name )
- virtual bool	endPrefixMapping ( const QString & prefix )
- virtual bool	error ( const QXmlParseException & exception )
- virtual QString	errorString () const
- virtual bool	externalEntityDecl ( const QString & name, const QString & publicId, const QString & systemId )
- virtual bool	fatalError ( const QXmlParseException & exception )
- virtual bool	ignorableWhitespace ( const QString & ch )
- virtual bool	internalEntityDecl ( const QString & name, const QString & value )
- virtual bool	notationDecl ( const QString & name, const QString & publicId, const QString & systemId )
- virtual bool	processingInstruction ( const QString & target, const QString & data )
- virtual bool	resolveEntity ( const QString & publicId, const QString & systemId, QXmlInputSource *& ret )
- virtual void	setDocumentLocator ( QXmlLocator * locator )
- virtual bool	skippedEntity ( const QString & name )
- virtual bool	unparsedEntityDecl ( const QString & name, const QString & publicId, const QString & systemId, const QString & notationName )
- virtual bool	warning ( const QXmlParseException & exception )

## 3.Detailed Description

QXmlDefaultHandler类提供所有XML处理程序类的默认实现。

此类汇集了专用处理程序类的功能，使其成为为QXmlReader的子类（尤其是QXmlSimpleReader）实现自定义处理程序时的方便起点。每个基类的虚函数都在该类中重新实现，从而为许多常见情况提供了明智的默认行为。通过对该类进行子类化并覆盖这些功能，您可以集中精力实现与应用程序相关的处理程序部分。

**必须告知XML阅读器在解析期间对不同类型的事件使用哪个处理程序**。这意味着，尽管QXmlDefaultHandler提供了从其所有基类继承的函数的默认实现，但对于特定类型的事件，我们仍然可以使用专门的处理程序。

例如，QXmlDefaultHandler子类化了QXmlContentHandler和QXmlErrorHandler，因此通过子类化，我们可以为以下两个阅读器功能使用相同的处理程序：

```c++
     xmlReader.setContentHandler(handler);
     xmlReader.setErrorHandler(handler);
```

由于读者会将解析错误通知处理程序，因此，例如，如果我们想在发生此类错误时停止解析，则有必要重新实现QXmlErrorHandler :: fatalError（）：

```c++
 bool Handler::fatalError (const QXmlParseException & exception)
 {
     qWarning() << "Fatal error on line" << exception.lineNumber()
                << ", column" << exception.columnNumber() << ":"
                << exception.message();

     return false;
 }
```

上面的函数返回false，告诉读者停止解析。 要继续使用相同的阅读器，必须创建一个新的处理程序实例，并设置阅读器以上述方式使用它。

检查某些由QXmlDefaultHandler继承的功能，并考虑为什么可能在自定义处理程序中重新实现它们，这很有用。 自定义处理程序通常将重新实现QXmlContentHandler :: startDocument（）以为新内容准备处理程序。 通过重新实现QXmlContentHandler :: startElement（），QXmlContentHandler :: endElement（）和QXmlContentHandler :: characters（），可以处理文档元素及其中的文本。 **您可能想重新实现QXmlContentHandler :: endDocument（）以在完全阅读文档后对内容执行一些定型或验证**。