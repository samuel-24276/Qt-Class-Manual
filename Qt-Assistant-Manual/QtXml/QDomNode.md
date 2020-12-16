# QDomNode

继承者：

- QDomAttr
- QDomCharacterData
- QDomDocument
- QDomDocumentFragment
- QDomDocumentType
- QDomElement
- QDomEntity
- QDomEntityReference 
- QDomNotation
- QDomProcessingInstruction

# 1.Public Types

- `enum EncodingPolicy { EncodingFromDocument, EncodingFromTextStream }`
- `enum NodeType { ElementNode, AttributeNode, TextNode, CDATASectionNode, EntityReferenceNode, …, CharacterDataNode }`

# 2.Public Functions

- `QDomNode(const QDomNode &n)`

- `QDomNode() QDomNode &operator=(const QDomNode &n)`

- `~QDomNode()`

- **`QDomNode namedItem(const QString &name) const`**

  返回其nodeName（）等于name的第一个直接子节点**的父节点**（原文档没有的父节点，测试后返回的是父节点）。

  如果不存在这样的直接子代，则返回空节点。

- **`QDomNode appendChild(const QDomNode &newChild)`**

  将newChild追加为节点的最后一个子节点。
  如果newChild是另一个节点的子节点，则将其重新关联到该节点。 如果newChild是此节点的子级，则将更改其在子级列表中的位置。
  如果newChild是QDomDocumentFragment，则将片段的子代从片段中删除并附加。
  如果newChild是QDomElement且此节点是已经具有元素节点作为子节点的QDomDocument，则不会将newChild作为子节点添加，并且返回空节点。
  成功返回对newChild的新引用，失败则返回空节点。
  在空节点（例如，使用默认构造函数创建）上调用此函数不会执行任何操作，并返回空节点。
  DOM规范不允许插入属性节点，但是由于历史原因，QDom仍然接受它们。

- **`QString nodeName() const`**

  返回节点的名称。

  名称的含义取决于子类：

  | Name                      | Meaning                         |
  | ------------------------- | ------------------------------- |
  | QDomAttr                  | 属性的名字                      |
  | QDomCDATASection          | The string "#cdata-section"     |
  | QDomComment               | The string "#comment"           |
  | QDomDocument              | The string "#document"          |
  | QDomDocumentFragment      | The string "#document-fragment" |
  | QDomDocumentType          | 文件类型的名称                  |
  | QDomElement               | 标签名称                        |
  | QDomEntity                | 实体名称                        |
  | QDomEntityReference       | 实体引用的名称                  |
  | QDomNotation              | 注释的名称                      |
  | QDomProcessingInstruction | 处理指令的对象                  |
  | QDomText                  | The string "#text"              |

  **注意**：处理元素和属性节点的名称时，**此函数不考虑名称空间的存在**。 结果，返回的名称可以包含可能出现的任何名称空间前缀。 要获取元素或属性的节点名称，请使用localName（）。 要获取名称空间前缀，请使用namespaceURI（）。

- `QString localName() const`

  如果节点使用名称空间，则此函数返回节点的本地名称；否则返回一个空字符串。

  **只有类型为ElementNode或AttributeNode的节点可以具有名称空间**。 必须在创建时指定名称空间。 之后无法添加名称空间。

  QDomDocument :: createAttributeNS（）

- `QDomNode::NodeType nodeType() const`

  返回节点类型。

- **`QString nodeValue() const`**

  返回节点的值。

  值的含义取决于子类：

  | Name                      | Meaning         |
  | ------------------------- | --------------- |
  | QDomAttr                  | 属性值          |
  | QDomCDATASection          | CDATA部分的内容 |
  | QDomComment               | The comment     |
  | QDomProcessingInstruction | 处理命令的数据  |
  | QDomText                  | The text        |

  

- `QDomNamedNodeMap attributes() const`

  返回所有属性的命名节点映射。 仅为QDomElements提供属性。
  更改地图中的属性还将更改此QDomNode的属性。

- **`QDomNodeList childNodes() const`**

  **返回所有直接子节点的列表**。
  通常，您会在QDomElement对象上调用此函数。
  例如，如果XML文档如下所示：

  ```xml
  <body>
      <h1>Heading</h1>
      <p>Hello <b>you</b></p>
  </body>
  ```

  Then the list of child nodes for the "body"-element will contain the node created by the &lt;h1&gt; tag and the node created by the &lt;p&gt; tag

  列表中的节点未复制； 因此更改列表中的节点也将更改此节点的子级。

- `void clear()`

  将节点转换为空节点； 如果以前不是空节点，则删除其类型和内容

- `QDomNode cloneNode(bool deep = true) const`

  创建QDomNode的深层（而非浅层）副本。
  如果deep为true，则将以递归方式进行克隆，这意味着所有节点的子节点也将被深度复制。 如果deep为false，则仅复制节点本身，并且该副本将没有子节点。

- `int columnNumber() const`

  对于由QDomDocument :: setContent（）创建的节点，此函数返回XML文档中解析该节点的列号。 否则，返回-1。

- `QDomNode firstChild() const`

  返回节点的第一个孩子。 如果没有子节点，则返回一个空节点。 更改返回的节点也将更改文档树中的节点。

- `QDomElement firstChildElement(const QString &tagName = QString()) const`

  如果tagName为非空，则返回带有标签名tagName的第一个子元素。 否则返回第一个子元素。 如果不存在此类子元素，则返回null元素。

- `bool hasAttributes() const`

  如果节点具有属性，则返回true；否则，返回false。 否则返回false。

- `bool hasChildNodes() const`

  如果节点有一个或多个子节点，则返回true；否则，返回true。 否则返回false。

- `QDomNode insertAfter(const QDomNode &newChild, const QDomNode &refChild)`

  在子节点refChild之后插入节点newChild。 refChild必须是此节点的直接子级。 如果refChild为null，则将newChild附加为该节点的最后一个子级。
  如果newChild是另一个节点的子节点，则将其重新关联到该节点。 如果newChild是此节点的子级，则将更改其在子级列表中的位置。
  如果newChild是QDomDocumentFragment，则将片段的子代从片段中删除并插入refChild之后。
  成功返回对newChild的新引用，失败则返回空节点。
  DOM规范不允许插入属性节点，但是由于历史原因，QDom仍然接受它们。

- `QDomNode insertBefore(const QDomNode &newChild, const QDomNode &refChild)`

  在子节点refChild之前插入节点newChild。 refChild必须是此节点的直接子级。 如果refChild为null，则将newChild作为节点的第一个孩子插入。
  如果newChild是另一个节点的子节点，则将其重新关联到该节点。 如果newChild是此节点的子级，则将更改其在子级列表中的位置。
  如果newChild是QDomDocumentFragment，则将片段的子代从片段中删除并插入refChild之前。
  成功返回对newChild的新引用，失败则返回空节点。
  DOM规范不允许插入属性节点，但是由于历史原因，QDom仍然接受它们。

- `bool isAttr() const`

  如果该节点是一个属性，则返回true； 否则返回false。
  如果此函数返回true，则并不表示此对象是QDomAttribute； 您可以使用toAttribute（）获得QDomAttribute。

- `bool isCDATASection() const`

  如果节点是CDATA节，则返回true；否则，返回false。 
  如果此函数返回true，则并不表示此对象是QDomCDATASection； 您可以使用toCDATASection（）获得QDomCDATASection。

- `bool isCharacterData() const`

  如果该节点是字符数据节点，则返回true；否则返回true。 否则返回false。
  如果此函数返回true，则并不意味着该对象是QDomCharacterData； 您可以使用toCharacterData（）获得QDomCharacterData。

- `bool isComment() const`

  如果该节点是注释，则返回true；否则，返回true。 否则返回false。
  如果此函数返回true，则并不意味着该对象是QDomComment； 您可以通过toComment（）获得QDomComment。

- `bool isDocument() const`

  如果节点是文档，则返回true；否则，返回true。 否则返回false。
  如果此函数返回true，则并不意味着此对象是QDomDocument；否则，它不表示该对象。 您可以使用toDocument（）获得QDomDocument。

- `bool isDocumentFragment() const`

  如果节点是文档片段，则返回true；否则，返回false。 否则返回false。
  如果此函数返回true，则并不表示此对象是QDomDocumentFragment； 您可以使用toDocumentFragment（）获得QDomDocumentFragment。

- `bool isDocumentType() const`

  如果节点是文档类型，则返回true；否则，返回false。
  如果此函数返回true，则并不表示此对象是QDomDocumentType； 您可以使用toDocumentType（）获得QDomDocumentType。

- `bool isElement() const`

  如果节点是一个元素，则返回true；否则返回false。 否则返回false。
  如果此函数返回true，则并不表示此对象是QDomElement； 您可以使用toElement（）获得QDomElement。

- **`bool isEntity() const`**

  如果节点是实体，则返回true； 否则返回false。
  如果此函数返回true，则并不表示此对象是QDomEntity。 您可以使用toEntity（）获得QDomEntity。

- **`QDomEntity toEntity() const`**

  将QDomNode转换为QDomEntity。 如果节点不是实体，则返回的对象将为null。

- **`bool isEntityReference() const`**

  如果节点是实体引用，则返回true；否则返回false。
  如果此函数返回true，则并不表示此对象是QDomEntityReference； 您可以使用toEntityReference（）获得QDomEntityReference。

- **`QDomEntityReference toEntityReference() const`**

  将QDomNode转换为QDomEntityReference。 如果该节点不是实体引用，则返回的对象将为null。

- `bool isNotation() const`

  如果该节点是一种表示法，则返回true；否则，返回true。 否则返回false。
  如果此函数返回true，则并不表示此对象是QDomNotation； 您可以使用toNotation（）获得QDomNotation。

- `bool isNull() const`

  如果此节点为null（即没有类型或内容），则返回true；否则，返回true。 否则返回false。

- `bool isProcessingInstruction() const`

  如果该节点是一条处理指令，则返回true；否则返回true。 否则返回false。
  如果此函数返回true，则并不表示此对象是QDomProcessingInstruction； 您可以使用toProcessingInstruction（）获得QProcessingInstruction。

- `bool isSupported(const QString &feature, const QString &version) const`

  如果DOM实现实现了功能部件功能，并且此节点在版本版本中支持此功能部件，则返回true；否则，返回true。 否则返回false。

- `bool isText() const`

  如果该节点是文本节点，则返回true；否则返回true。 否则返回false。
  如果此函数返回true，则并不表示此对象是QDomText； 您可以使用toText（）获得QDomText。

- `QDomNode lastChild() const`

  返回节点的最后一个子级。 如果没有子节点，则返回一个空节点。 更改返回的节点也将更改文档树中的节点。

- `QDomElement lastChildElement(const QString &tagName = QString()) const`

- `int lineNumber() const`

- `QString namespaceURI() const`

- `QDomNode nextSibling() const`

- `QDomElement nextSiblingElement(const QString &tagName = QString()) const`

- `void normalize()`

- `QDomDocument ownerDocument() const`

- `QDomNode parentNode() const`

- `QString prefix() const`

- `QDomNode previousSibling() const`

- `QDomElement previousSiblingElement(const QString &tagName = QString()) const`

- `QDomNode removeChild(const QDomNode &oldChild)`

- **`QDomNode replaceChild(const QDomNode &newChild, const QDomNode &oldChild)`**

  用newChild替换oldChild。 **oldChild必须是该节点（即调用者）的直接子代**。

  如果newChild是另一个节点的子节点，则将其重新关联到该节点。 如果newChild是此节点的子级，则将更改其在子级列表中的位置。

  如果newChild是QDomDocumentFragment，则oldChild被该片段的所有子代替换。

  成功返回一个对oldChild的新引用，否则返回一个空节点。

- `void save(QTextStream &stream, int indent, QDomNode::EncodingPolicy encodingPolicy = QDomNode::EncodingFromDocument) const`

- `void setNodeValue(const QString &v)`

- `void setPrefix(const QString &pre)`

- `QDomAttr toAttr() const`

- `QDomCDATASection toCDATASection() const`

- `QDomCharacterData toCharacterData() const`

- `QDomComment toComment() const`

- `QDomDocument toDocument() const`

- `QDomDocumentFragment toDocumentFragment() const`

- `QDomDocumentType toDocumentType() const`

- `QDomElement toElement() const`

- `QDomNotation toNotation() const`

- `QDomProcessingInstruction toProcessingInstruction() const`

- `QDomText toText() const`

- `bool operator!=(const QDomNode &n) const`

- `bool operator==(const QDomNode &n) const`

# 3.Related Non-Members

- QTextStream &operator<<(QTextStream &str, const QDomNode &node)

# 4.Detailed Description

**DOM中的许多函数都返回一个QDomNode。**

找出节点的类型：

- isAttr（）
- isCDATASection（）
- isDocumentFragment（）
- isDocument（）
- isDocumentType（）
- isElement（）
- isEntityReference（）
- isText（）
- isEntity（）
- isNotation（）
- isProcessingInstruction（）
- isCharacterData（）
- isComment（）

将QDomNode转换为其子类之一：

- toAttr（）
- toCDATASection（）
- toDocumentFragment（）
- toDocument（）
- toDocumentType（）
- toElement（）
- toEntityReference（）
- toText（）
- toEntity（）
- toNotation（）
-  ，toProcessingInstruction（）
- ，toCharacterData（）
- toComment（）

将节点转换为空节点：

- clear（）

QDomNode类的副本使用**显式共享**来共享其数据。这意味着**修改一个节点将更改所有副本**。结合返回QDomNode的函数（例如，第一个孩子（）。您可以使用cloneNode（）制作节点的独立（深层）副本。
QDomNode可以为null，就像nullptr一样。创建空节点的副本将导致另一个空节点。无法修改空节点，但是可以为其分配另一个（可能是非空）节点。在这种情况下，空节点的副本将保持为空。您可以通过调用isNull（）来检查QDomNode是否为null。 QDomNode（或任何派生类）的空构造函数创建一个空节点。
使用insertBefore（），insertAfter（）或appendChild（）插入节点。您可以使用replaceChild（）将一个节点替换为另一个节点，并使用removeChild（）删除节点。
要遍历节点，请使用firstChild（）获取节点的第一个子节点（如果有），然后使用nextSibling（）进行遍历。 QDomNode还提供了lastChild（），previousSibling（）和parentNode（）。要查找具有特定节点名称的第一个子节点，请使用namedItem（）。
要找出节点是否有子节点，请使用hasChildNodes（）并使用childNodes（）来获取节点所有子节点的列表。
节点的名称和值（其含义因其类型而异）分别由nodeName（）和nodeValue（）返回。节点的类型由nodeType（）返回。可以使用setNodeValue（）设置节点的值。
节点所属的文档由ownerDocument（）返回。
可以使用normalize（）将相邻的QDomText节点合并到单个节点中。
QDomElement节点具有可以使用attribute（）检索的属性。
QDomElement和QDomAttr节点可以具有可以使用namespaceURI（）检索的名称空间。使用localName（）检索其本地名称，并使用prefix（）检索其前缀。可以使用setPrefix（）设置前缀。
您可以使用save（）将节点的XML表示形式写入文本流。
下面的示例在XML文档中查找第一个元素，并打印作为其直接子元素的所有元素的名称。

```c++
QDomDocument d;
d.setContent(someXML);
QDomNode n = d.firstChild();
while (!n.isNull()) {
if (n.isElement()) {
QDomElement e = n.toElement();
    cout << "Element name: " << e.tagName() << Qt::endl;
    break;
}
	n = n.nextSibling();
}
```

