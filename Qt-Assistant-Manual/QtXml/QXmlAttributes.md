# QXmlAttributes

## 1.Public Functions

- `QXmlAttributes ()`
- `virtual	~QXmlAttributes ()`
- `void	append ( const QString & qName, const QString & uri, const QString & localPart, const QString & value )`
- `void	clear ()`
- `int	count () const`
- `int	index ( const QString & qName ) const`
- `int	index ( const QLatin1String & qName ) const`
- `int	index ( const QString & uri, const QString & localPart ) const`
- `int	length () const`
- `QString	localName ( int index ) const`
- `QString	qName ( int index ) const`
- `QString	type ( int index ) const`
- `QString	type ( const QString & qName ) const`
- `QString	type ( const QString & uri, const QString & localName ) const`
- `QString	uri ( int index ) const`
- `QString	value ( int index ) const`
- `QString	value ( const QString & qName ) const`
- `QString	value ( const QLatin1String & qName ) const`
- `QString	value ( const QString & uri, const QString & localName ) const`

## 2.Detailed Description

QXmlAttributes类提供XML属性。

如果属性由QXmlContentHandler :: startElement（）报告，则该类用于传递属性值。

使用index（）查找属性在列表中的位置，使用count（）检索属性的数量，并使用clear（）删除属性。 可以使用append（）添加新属性。 使用type（）获取属性的类型，使用value（）获取其值。 该属性的名称可从localName（）或qName（）获得，其名称空间URI可从uri（）获得。