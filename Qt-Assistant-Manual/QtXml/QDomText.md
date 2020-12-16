# QDomText

继承关系：`QDomText`->`QDomCharacterData`->`QDomNode`

继承者： `QDomCDATASection`

## 1.Public Functions

- QDomText ()

- QDomText ( const QDomText & x )

- QDomNode::NodeType	nodeType () const

  Returns TextNode.

- QDomText	splitText ( int offset )

  将此DOM文本对象拆分为两个QDomText对象。 该对象保留其第一个偏移字符，第二个（新创建的）对象与其余字符一起插入到文档树中。

  该函数返回新创建的对象。

- QDomText &	operator= ( const QDomText & x )

## 2.Detailed Description

QDomText类表示已解析的XML文档中的文本数据。

您可以使用splitText（）将QDomText对象中的文本拆分为两个QDomText objecs。
