# QDomCharacterData

继承关系：`QDomCharacterData`->`QDomNode`

继承者： 

- QDomComment
- QDomText

## 1.Public Functions

- QDomCharacterData ()

- QDomCharacterData ( const QDomCharacterData & x )

- void	appendData ( const QString & arg )

  将字符串arg追加到存储的字符串。

- QString	data () const

- void	deleteData ( unsigned long offset, unsigned long count )

  从位置offset中删除长度为count的子串。

- void	insertData ( unsigned long offset, const QString & arg )

  将字符串arg插入位置offset的存储字符串中。

- uint	length () const

  返回存储字符串的长度。

- QDomNode::NodeType	nodeType () const

- void	replaceData ( unsigned long offset, unsigned long count, const QString & arg )

  用字符串arg替换从位置offset开始的长度为count的串。

- void	setData ( const QString & v )

  将此对象的字符串设置为v。

- QString	substringData ( unsigned long offset, unsigned long count )

  从位置offset返回长度为count 的子串。

- QDomCharacterData &	operator= ( const QDomCharacterData & x )

## 2.Detailed Description

QDomCharacterData类表示DOM中的**通用字符串**。

XML中使用的字符数据指定了通用数据字符串。 此类的更专门的版本是QDomText，QDomComment和QDomCDATASection。

数据字符串由setData（）设置，并由data（）检索。 您可以使用substringData（）检索数据字符串的一部分。 可以使用appendData（）附加额外的数据，也可以使用insertData（）插入额外的数据。 数据字符串的某些部分可以用deleteData（）删除，也可以用replaceData（）替换。 数据字符串的长度由length（）返回。

包含此字符数据的节点的节点类型由nodeType（）返回。