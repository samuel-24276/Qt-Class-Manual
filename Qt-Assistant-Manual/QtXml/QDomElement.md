# QDomElement

继承关系：`QDomElement`->`QDomNode`

## 1.Public Functions

- QDomElement(const QDomElement &x)

- QDomElement()

- QDomElement &operator=(const QDomElement &x)

- QString attribute(const QString &name, const QString &defValue = QString()) const

  返回名为name的属性。 如果该属性不存在，则返回defValue。

- QDomAttr attributeNode(const QString &name)

  返回与名为name的属性相对应的**QDomAttr对象**。 如果不存在这样的属性，则返回null属性。

- QDomNamedNodeMap attributes() const

  **返回包含该元素所有属性的QDomNamedNodeMap**。

- **QDomNodeList elementsByTagName(const QString &tagname) const**

  返回一个QDomNodeList，它包含在以该元素为根的元素子树的预遍历过程中遇到的，名为tagname的该元素的所有后代。 返回列表中元素的顺序是在遍历顺序时遇到的顺序。

- bool hasAttribute(const QString &name) const

  如果此元素具有名为name的属性，则返回true；否则返回false。
  注意：此函数不考虑名称空间的存在。 结果，将针对完全限定的属性名称（包括可能存在的任何名称空间前缀）测试指定的名称。

- QDomNode::NodeType nodeType() const

  返回ElementNode.

- void removeAttribute(const QString &name)

  从此元素中删除名为name的属性。

- QDomAttr removeAttributeNode(const QDomAttr &oldAttr)

  从元素中删除属性oldAttr并返回它。

- void setAttribute(const QString &name, const QString &value)

  添加一个名为name的属性，其值为value。 如果存在具有相同名称的属性，则其值将替换为value。

- void setAttribute(const QString &name, qlonglong value)

- void setAttribute(const QString &name, qulonglong value)

- void setAttribute(const QString &name, int value)

- void setAttribute(const QString &name, uint value)

- void setAttribute(const QString &name, float value)

- void setAttribute(const QString &name, double value)

- QDomAttr setAttributeNode(const QDomAttr &newAttr)

  **将属性newAttr添加到此元素**。
  如果元素具有与newAttr同名的另一个属性，则此函数将替换该属性并返回它； 否则，该函数返回null属性。

- void setTagName(const QString &name)

  将此元素的标签名称设置为name。

- QString tagName() const

  返回此元素的标签名称。 对于这样的XML元素：
    <img src =“ myimg.png”>
  标记名将返回“ img”。

- QString text() const

  返回元素的文本或空字符串。

  此功能将忽略注释。 它仅评估QDomText和QDomCDATASection对象。

- QString attributeNS(const QString nsURI, const QString &localName, const QString &defValue = QString()) const

  返回具有本地名称localName和名称空间URI nsURI的属性。 如果该属性不存在，则返回defValue。

- QDomAttr attributeNodeNS(const QString &nsURI, const QString &localName)

  返回与本地名称localName和名称空间URI nsURI的属性对应的QDomAttr对象。 如果不存在这样的属性，则返回null属性。

- QDomNodeList elementsByTagNameNS(const QString &nsURI, const QString &localName) const

  返回一个QDomNodeList，它包含此元素的所有后代，具有本地名称localName和在以该元素为根的元素子树的预遍历过程中遇到的名称空间URI nsURI。 返回列表中元素的顺序是在遍历顺序时遇到的顺序。

- bool hasAttributeNS(const QString &nsURI, const QString &localName) const

- void removeAttributeNS(const QString &nsURI, const QString &localName)

- void setAttributeNS(const QString nsURI, const QString &qName, const QString &value)

- void setAttributeNS(const QString nsURI, const QString &qName, int value)

- void setAttributeNS(const QString nsURI, const QString &qName, uint value)

- void setAttributeNS(const QString nsURI, const QString &qName, qlonglong value)

- void setAttributeNS(const QString nsURI, const QString &qName, qulonglong value)

- void setAttributeNS(const QString nsURI, const QString &qName, double value)

- QDomAttr setAttributeNodeNS(const QDomAttr &newAttr)

## 2.Detailed Description

QDomElement类表示DOM树中的一个元素。

元素具有tagName（）以及与之关联的零个或多个属性。 可以使用setTagName（）更改标签名称。

元素属性由QDomAttr对象表示，可以使用attribute（）和attributeNode（）函数进行查询。 您可以使用setAttribute（）和setAttributeNode（）函数设置属性。 可以使用removeAttribute（）删除属性。 这些函数有名称空间感知的等效项，即setAttributeNS（），setAttributeNodeNS（）和removeAttributeNS（）。

如果您要访问节点的文本，请使用text（），例如

```c++
 QDomElement e = //...
 //...
 QString s = e.text()
```

text（）函数以递归方式查找文本（因为并非所有元素都包含文本）。 如果要在节点的所有子节点中查找所有文本，请遍历子节点以查找QDomText节点，例如

```c++
QString text;
QDomElement element = doc.documentElement();
for(QDomNode n = element.firstChild(); !n.isNull(); n = n.nextSibling())
{
    QDomText t = n.toText();
    if (!t.isNull())
    	text += t.data();
}
```

请注意，我们尝试将每个节点转换为文本节点，并**直接在节点上使用text（）**而不是使用firstChild().toText().data()或n.toText().data()，因为该节点可能 不是文字元素。

您可以使用elementsByTagName（）或elementsByTagNameNS（）获得具有指定标签名称的元素的所有后代的列表。

要浏览dom文档的元素，请使用firstChildElement（），lastChildElement（），nextSiblingElement（）和previousSiblingElement（）。 例如，要在称为“数据库”的根元素中遍历所有称为“入口”的子元素，可以使用：

```c++
QDomDocument doc = // ...
QDomElement root = doc.firstChildElement("database");
QDomElement elt = root.firstChildElement("entry");
for (; !elt.isNull(); elt = elt.nextSiblingElement("entry")) 
{
	// ...
}
```



