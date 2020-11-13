# QDomEntity

继承关系：`QDomEntity`->`QDomNode`

## 1.Detailed Description

QDomEntity类代表一个XML实体。

此类表示XML文档中已解析或未解析的实体。 请注意，这是对实体本身而非实体声明进行建模。

**DOM不支持编辑实体节点**。 如果用户要更改实体的内容，则必须在DOM树中用实体内容的副本**替换**每个相关的QDomEntityReference节点，然后必须对每个副本进行所需的更改。 **实体节点的所有后代都是只读的**。

**实体节点没有任何父节点**。

您可以访问实体的publicId（），systemId（）和notationName（）（如果可用）。

有关文档对象模型的更多信息，请参见1级和2级核心。 有关DOM实现的更一般性介绍，请参见QDomDocument文档。

## 2.public function

QDomEntity ()
QDomEntity ( const QDomEntity & x )
QDomNode::NodeType	nodeType () const
QString	notationName () const
QString	publicId () const
QString	systemId () const
QDomEntity &	operator= ( const QDomEntity & x )