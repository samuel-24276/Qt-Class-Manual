# QDomProcessingInstruction

继承关系：`QDomProcessingInstruction`->`QDomNode`

## 1.Public Functions

- `QDomProcessingInstruction ()`
- `QDomProcessingInstruction ( const QDomProcessingInstruction & x )`
- `QString	data () const`
- `QDomNode::NodeType	nodeType () const`
- `void	setData ( const QString & d )`
- `QString	target () const`
- `QDomProcessingInstruction &	operator= ( const QDomProcessingInstruction & x )`

## 2.Detailed Description

QDomProcessingInstruction类表示XML处理指令。

在XML中使用处理指令将特定于处理器的信息保留在文档的文本中。

QDom将出现在XML文档顶部的XML声明（通常<？xml version ='1.0'encoding ='UTF-8'？>）作为处理指令。不幸的是，因为XML声明不是处理指令；因此，请参见。除其他差异外，无法将其插入文档中的第一行。

不要使用此函数来创建xml声明，因为尽管它具有与处理指令相同的语法，但事实并非如此，并且QDom可能不会将其视为这样。

使用data（）检索处理指令的内容，并使用setData（）进行设置。使用target（）检索处理指令的目标。

有关文档对象模型的更多信息，请参见1级和2级核心。有关DOM实现的更一般性介绍，请参见QDomDocument文档。