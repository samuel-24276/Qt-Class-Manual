# QDomComment

继承关系：`QDomComment`->`QDomCharacterData`->`QDomNode`

## 1.Public Functions

- QDomComment ()
- QDomComment ( const QDomComment & x )
- QDomNode::NodeType	nodeType () const
- QDomComment &	operator= ( const QDomComment & x )

## 2.Detailed Description

QDomComment类表示XML注释。

解析的XML中的注释，例如：

```xml
 <!-- this is a comment -->
```

由解析的Dom树中的QDomComment对象表示。

