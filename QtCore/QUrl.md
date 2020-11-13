# QUrl

## 1.Public Types

- `enum	FormattingOption { None, RemoveScheme, RemovePassword, RemoveUserInfo, ..., StripTrailingSlash }`

  格式选项定义了当以文本形式写出时如何格式化URL。

  | Constant                   | Value                                | Description                                               |
  | -------------------------- | ------------------------------------ | --------------------------------------------------------- |
  | `QUrl::None`               | 0x0                                  | URL格式不变                                               |
  | `QUrl::RemoveScheme`       | 0x1                                  | 该方案已从URL中删除。                                     |
  | `QUrl::RemovePassword`     | 0x2                                  | URL中的所有密码都将被删除。                               |
  | `QUrl::RemoveUserInfo`     | RemovePassword \| 0x4                | URL中的所有用户信息都将被删除。                           |
  | `QUrl::RemovePort`         | 0x8                                  | URL中的所有具体端口都将被删除。                           |
  | `QUrl::RemoveAuthority`    | RemoveUserInfo \| RemovePort \| 0x10 |                                                           |
  | `QUrl::RemovePath`         | 0x20                                 | URL的路径被删除，仅保留方案，主机地址和端口（如果存在）。 |
  | `QUrl::RemoveQuery`        | 0x40                                 | URL的查询部分（后跟“？”字符）将被删除。                   |
  | `QUrl::RemoveFragment`     | 0x80                                 |                                                           |
  | `QUrl::StripTrailingSlash` | 0x10000                              | 如果存在斜杠，则将其删除。                                |

  请注意，QUrl遵循的Nameprep中的大小写折叠规则要求始终将主机名转换为小写，而不考虑所使用的Qt :: FormattingOptions。

- `flags	FormattingOptions`

  FormattingOptions类型是QFlags <FormattingOption>的typedef。 它存储FormattingOption值的OR组合。

- `enum	ParsingMode { TolerantMode, StrictMode }`

  解析模式控制QUrl解析字符串的方式。

  | Constant             | Value | Description                                                  |
  | -------------------- | ----- | ------------------------------------------------------------ |
  | `QUrl::TolerantMode` | 0     | QUrl将尝试更正URL中的一些常见错误。 在处理用户输入的URL时，此模式很有用。 |
  | `QUrl::StrictMode`   | 1     | 仅接受有效的URL。 此模式对于常规URL验证很有用。              |

  在TolerantMode中，解析器会更正以下无效输入：

  - 空格和“％20”：如果编码的URL包含空格，它将被替换为“％20”。 如果解码的URL包含“％20”，则在解析URL之前，它将用单个空格替换。
  - 单个“％”字符：任何出现的百分比字符“％”之后不恰好两个十六进制字符（例如，“ 13％coverage.html”）都将替换为“％25”。
  - 保留和未保留的字符：编码的URL应该只包含几个字符作为文字。 所有其他字符都应进行百分比编码。 在TolerantMode中，这些字符将在不允许的位置自动进行百分比编码：space / double-quote /“ <” /“>” /“ [” /“” /“]” /“ ^” /“`” / “ {” /“ |” /“}”

## 2.Public Functions

- QUrl ()

- QUrl ( const QString & url )

  通过解析url构造一个URL。 假定url以人类可读的形式表示，没有百分比编码。 QUrl将自动对URL中不允许的所有字符进行百分比编码。 **默认的解析模式是TolerantMode**。

- QUrl ( const QUrl & other )

- QUrl ( const QString & url, ParsingMode parsingMode )

- ~QUrl ()

- void	addEncodedQueryItem ( const QByteArray & key, const QByteArray & value )

- void	addQueryItem ( const QString & key, const QString & value )

- QList<QByteArray>	allEncodedQueryItemValues ( const QByteArray & key ) const

- QStringList	allQueryItemValues ( const QString & key ) const

- QString	authority () const

- void	clear ()

- QByteArray	encodedFragment () const

- QByteArray	encodedHost () const

- QByteArray	encodedPassword () const

- QByteArray	encodedPath () const

- QByteArray	encodedQuery () const

- QByteArray	encodedQueryItemValue ( const QByteArray & key ) const

- QList<QPair<QByteArray, QByteArray> >	encodedQueryItems () const

- QByteArray	encodedUserName () const

- QString	errorString () const

- QString	fragment () const

- bool	hasEncodedQueryItem ( const QByteArray & key ) const

- bool	hasFragment () const

- bool	hasQuery () const

- bool	hasQueryItem ( const QString & key ) const

- QString	host () const

- bool	isEmpty () const

- bool	isLocalFile () const

- bool	isParentOf ( const QUrl & childUrl ) const

- bool	isRelative () const

- bool	isValid () const

- QString	password () const

- QString	path () const

- int	port () const

- int	port ( int defaultPort ) const

- QString	queryItemValue ( const QString & key ) const

- QList<QPair<QString, QString> >	queryItems () const

- char	queryPairDelimiter () const

- char	queryValueDelimiter () const

- void	removeAllEncodedQueryItems ( const QByteArray & key )

- void	removeAllQueryItems ( const QString & key )

- void	removeEncodedQueryItem ( const QByteArray & key )

- void	removeQueryItem ( const QString & key )

- QUrl	resolved ( const QUrl & relative ) const

- QString	scheme () const

- void	setAuthority ( const QString & authority )

- void	setEncodedFragment ( const QByteArray & fragment )

- void	setEncodedHost ( const QByteArray & host )

- void	setEncodedPassword ( const QByteArray & password )

- void	setEncodedPath ( const QByteArray & path )

- void	setEncodedQuery ( const QByteArray & query )

- void	setEncodedQueryItems ( const QList<QPair<QByteArray, QByteArray> > & query )

- void	setEncodedUrl ( const QByteArray & encodedUrl )

- void	setEncodedUrl ( const QByteArray & encodedUrl, ParsingMode parsingMode )

- void	setEncodedUserName ( const QByteArray & userName )

- void	setFragment ( const QString & fragment )

- void	setHost ( const QString & host )

- void	setPassword ( const QString & password )

- void	setPath ( const QString & path )

- void	setPort ( int port )

- void	setQueryDelimiters ( char valueDelimiter, char pairDelimiter )

- void	setQueryItems ( const QList<QPair<QString, QString> > & query )

- void	setScheme ( const QString & scheme )

- void	setUrl ( const QString & url )

- void	setUrl ( const QString & url, ParsingMode parsingMode )

- void	setUserInfo ( const QString & userInfo )

- void	setUserName ( const QString & userName )

- void	swap ( QUrl & other )

- QByteArray	toEncoded ( FormattingOptions options = None ) const

- QString	toLocalFile () const

- QString	toString ( FormattingOptions options = None ) const

- QString	topLevelDomain () const

- QString	userInfo () const

- QString	userName () const

- bool	operator!= ( const QUrl & url ) const

- QUrl &	operator= ( const QUrl & url )

- QUrl &	operator= ( const QString & url )

- bool	operator== ( const QUrl & url ) const

## 3.Static Public Members

- QString	fromAce ( const QByteArray & domain )
- QUrl	fromEncoded ( const QByteArray & input )
- QUrl	fromEncoded ( const QByteArray & input, ParsingMode parsingMode )
- QUrl	fromLocalFile ( const QString & localFile )
- QString	fromPercentEncoding ( const QByteArray & input )
- QUrl	fromUserInput ( const QString & userInput )
- QStringList	idnWhitelist ()
- void	setIdnWhitelist ( const QStringList & list )
- QByteArray	toAce ( const QString & domain )
- QByteArray	toPercentEncoding ( const QString & input, const QByteArray & exclude = QByteArray(), const QByteArray & include = QByteArray() )

## 4.Related Non-Members

- uint	qHash ( const QUrl & url )
- QDataStream &	operator<< ( QDataStream & out, const QUrl & url )
- QDataStream &	operator>> ( QDataStream & in, QUrl & url )

## 5.Macros

​	`QT_NO_URL_CAST_FROM_STRING`

## 6.Detailed Description

QUrl类提供了使用URL的便捷接口。

它可以**解析和构造编码和未编码形式的URL**。 QUrl还支持国际化域名（IDN）。

使用QUrl的最常见方法是通过构造函数通过传递QString对其进行初始化。否则，也可以使用setUrl（）和setEncodedUrl（）。

URL可以两种形式表示：已编码或未编码。**未编码的表示形式适合显示给用户，但是编码的表示形式通常是您要发送到Web服务器的形式**。例如，未编码的URL“ `http：//bühler.example.com/applicants.xml`”将作为“ `http://xn--bhler-kva.example.com/List%20of%20applicants.xml`”发送到服务器。这可以通过调用toEncoded（）函数进行验证。

也可以通过调用setScheme（），setUserName（），setPassword（），setHost（），setPort（），setPath（），setEncodedQuery（）和setFragment（）来逐个构造URL。还提供了一些便利功能：setAuthority（）设置用户名，密码，主机和端口。 setUserInfo（）一次设置用户名和密码。

调用isValid（）来检查URL是否有效。可以在构造URL的任何时候完成此操作。

**通过使用setQueryItems（），addQueryItem（）和removeQueryItem（），构造查询特别方便**。使用setQueryDelimiters（）定制用于生成查询字符串的定界符。

为了方便生成编码的URL字符串或查询字符串，有两个名为fromPercentEncoding（）和toPercentEncoding（）的静态函数处理QString的百分比编码和解码。

调用isRelative（）将告诉您URL是否是相对的。可以通过将相对URL作为参数传递给resolve（）来解析，该URL返回绝对URL。 isParentOf（）用于确定一个URL是否是另一个URL的父级。

fromLocalFile（）通过解析本地文件路径来构造QUrl。 toLocalFile（）将URL转换为本地文件路径。

URL的可读格式是通过toString（）获取的。此表示形式适合于以未编码形式向用户显示URL。但是，由toEncoded（）返回的编码形式仅供内部使用，传递给Web服务器，邮件客户端等。

QUrl符合RFC 3986（统一资源标识符：通用语法）中的URI规范，并包括RFC 1738（统一资源定位器）中的方案扩展。 QUrl中的大小写折叠规则符合RFC 3491（名称准备：国际化域名（IDN）的Stringprep配置文件）。