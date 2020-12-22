# QXmlParseException

## 1.Public Functions

- QXmlParseException ( const QString & name = QString(), int c = -1, int l = -1, const QString & p = QString(), const QString & s = QString() )

- QXmlParseException ( const QXmlParseException & other )

- ~QXmlParseException ()

- int	columnNumber () const

- int	lineNumber () const

- QString	message () const

- QString	publicId () const

  返回发生错误的公共标识符。

- QString	systemId () const

  返回发生错误的系统标识符。

## 2.Detailed Description

QXmlParseException类用于**报告QXmlErrorHandler接口的错误**。

XML子系统在检测到错误时会构造此类的实例。 您可以使用systemId（），publicId（），lineNumber（）和columnNumber（）以及错误message（）来检索发生错误的位置。 可能的错误消息是：

- "no error occurred"
- "error triggered by consumer"
- "unexpected end of file"
- "more than one document type definition"
- "error occurred while parsing element"
- "tag mismatch"
- "error occurred while parsing content"
- "unexpected character"
- "invalid name for processing instruction"
- "version expected while reading the XML declaration"
- "wrong value for standalone declaration"
- "encoding declaration or standalone declaration expected while reading the XML declaration"
- "standalone declaration expected while reading the XML declaration"
- "error occurred while parsing document type definition"
- "letter is expected"
- "error occurred while parsing comment"
- "error occurred while parsing reference"
- "internal general entity reference not allowed in DTD"
- "external parsed general entity reference not allowed in attribute value"
- "external parsed general entity reference not allowed in DTD"
- "unparsed entity reference n wrong context"
- "recursive entities"
- "error in the text declaration of an external entity"

请注意，如果您想将这些错误消息显示给应用程序的用户，除非明确翻译，否则它们将以英文显示。