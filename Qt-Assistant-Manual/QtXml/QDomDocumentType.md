# QDomDocumentType

继承关系：`QDomDocumentType`->`QDomNode`

## 1.Public Functions

- QDomDocumentType ()
- QDomDocumentType ( const QDomDocumentType & n )
- QDomNamedNodeMap	entities () const
- QString	internalSubset () const
- QString	name () const
- QDomNode::NodeType	nodeType () const
- QDomNamedNodeMap	notations () const
- QString	publicId () const
- QString	systemId () const
- QDomDocumentType &	operator= ( const QDomDocumentType & n )

## 2.Detailed Description

QDomDocumentType类是文档树中DTD（文档类型定义）的表示。

QDomDocumentType类允许对DTD中的一些数据结构进行只读访问:它可以返回所有实体()和符号()的映射。此外，函数name()返回文档类型名称<!DOCTYPE name> tag.

这个类还提供了publicId()、systemId()和internal子集()函数。