# QTextCodec编码类

## 1.Public Types

- class	ConverterState
- enum	ConversionFlag { DefaultConversion, ConvertInvalidToNull, IgnoreHeader }
- flags	ConversionFlags

## 2.Public Functions

- virtual QList<QByteArray>	aliases () const
- bool	canEncode ( QChar ch ) const
- bool	canEncode ( const QString & s ) const
- QByteArray	fromUnicode ( const QString & str ) const
- QByteArray	fromUnicode ( const QChar * input, int number, ConverterState * state = 0 ) const
- QTextDecoder *	makeDecoder () const
- QTextDecoder *	makeDecoder ( ConversionFlags flags ) const
- QTextEncoder *	makeEncoder () const
- QTextEncoder *	makeEncoder ( ConversionFlags flags ) const
- virtual int	mibEnum () const = 0
- virtual QByteArray	name () const = 0
- QString	toUnicode ( const QByteArray & a ) const
- QString	toUnicode ( const char * input, int size, ConverterState * state = 0 ) const
- QString	toUnicode ( const char * chars ) const

## 3.Static Public Members

- QList<QByteArray>	availableCodecs ()

- QList<int>	availableMibs ()

- QTextCodec *	codecForCStrings ()

- QTextCodec *	codecForHtml ( const QByteArray & ba, QTextCodec * defaultCodec )

- QTextCodec *	codecForHtml ( const QByteArray & ba )

- QTextCodec *	codecForLocale ()

- QTextCodec *	codecForMib ( int mib )

- **`QTextCodec *	codecForName ( const QByteArray & name )`**

  搜索所有已安装的QTextCodec对象，并返回最匹配名称的对象； 匹配不区分大小写。 如果找不到与名称匹配的编解码器，则返回0。

- QTextCodec *	codecForName ( const char * name )

  搜索所有已安装的QTextCodec对象，并返回最匹配名称的对象； 匹配不区分大小写。 如果找不到与名称匹配的编解码器，则返回0。

- QTextCodec *	codecForTr ()

- QTextCodec *	codecForUtfText ( const QByteArray & ba, QTextCodec * defaultCodec )

- QTextCodec *	codecForUtfText ( const QByteArray & ba )

- void	setCodecForCStrings ( QTextCodec * codec )

- void	setCodecForLocale ( QTextCodec * c )

- void	setCodecForTr ( QTextCodec * c )

## 4.Protected Functions

- QTextCodec ()
- virtual	~QTextCodec ()
- virtual QByteArray	convertFromUnicode ( const QChar * input, int number, ConverterState * state ) const = 0
- virtual QString	convertToUnicode ( const char * chars, int len, ConverterState * state ) const = 0

## 5.Detailed Description

QTextCodec类提供文本编码之间的转换。

Qt使用Unicode来存储，绘制和处理字符串。 在许多情况下，您可能希望处理使用不同编码的数据。 例如，大多数日文文档仍存储在Shift-JIS或ISO 2022-JP中，而俄罗斯用户经常将其文档存储在KOI8-R或Windows-1251中。

Qt提供了一组QTextCodec类，以帮助将非Unicode格式与Unicode相互转换。 您也可以创建自己的编解码器类。

支持的编码为：

- Apple Roman
- Big5
- Big5-HKSCS
- CP949
- EUC-JP
- EUC-KR
- GB18030-0
- IBM 850
- IBM 866
- IBM 874
- ISO 2022-JP
- ISO 8859-1 to 10
- ISO 8859-13 to 16
- Iscii-Bng, Dev, Gjr, Knd, Mlm, Ori, Pnj, Tlg, and Tml
- JIS X 0201
- JIS X 0208
- KOI8-R
- KOI8-U
- MuleLao-1
- ROMAN8
- Shift-JIS
- TIS-620
- TSCII
- UTF-8
- UTF-16
- UTF-16BE
- UTF-16LE
- UTF-32
- UTF-32BE
- UTF-32LE
- Windows-1250 to 1258
- WINSAMI2