# QDomDocumentFragment

继承关系：`QDomDocumentFragment`->`QDomNode`

## 1.Public Functions

- QDomDocumentFragment ()
- QDomDocumentFragment ( const QDomDocumentFragment & x )
- QDomNode::NodeType	nodeType () const
- QDomDocumentFragment &	operator= ( const QDomDocumentFragment & x )

## 2.Detailed Description

QDomDocumentFragment类是QDomNodes的树，通常不是完整的QDomDocument。

如果要执行**复杂的树操作**，则有一个轻量级的类来存储节点及其关系非常**有用**。 QDomDocumentFragment**存储文档的子树，它不一定代表格式正确的XML文档**。

如果要对列表中的多个节点进行分组并将它们作为某个节点的子节点一起插入，QDomDocumentFragment也很有用。 **在这些情况下，QDomDocumentFragment可用作此子列表的临时容器**。

QDomDocumentFragment的最重要特征是QDomNode :: insertAfter（），QDomNode :: insertBefore（），QDomNode :: replaceChild（）和QDomNode :: appendChild（）以特殊方式对其进行处理，而不是自己插入片段 ，将插入所有片段的子代。