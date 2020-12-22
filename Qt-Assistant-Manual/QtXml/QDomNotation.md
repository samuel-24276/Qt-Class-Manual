# QDomNotation

继承关系：`QDomNotation`->`QDomNode`

## 1.Public Functions

- QDomNotation ()
- QDomNotation ( const QDomNotation & x )
- QDomNode::NodeType	nodeType () const
- QString	publicId () const
- QString	systemId () const
- QDomNotation &	operator= ( const QDomNotation & x )

## 2.Detailed Description

QDomNotation类表示XML注释。

注释可以通过名字声明未解析实体的格式（请参阅XML 1.0规范的4.7节），或用于处理指令目标的正式声明（请参阅XML 1.0规范的2.6节）。

DOM不支持编辑符号节点。 因此，它们是只读的。

注释节点没有任何父代。

您可以从符号节点中检索publicId（）和systemId（）。