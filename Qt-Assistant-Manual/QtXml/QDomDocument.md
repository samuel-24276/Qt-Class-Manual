# QDomDocument

继承关系：`QDomDocument`->`QDomNode`

Qt 4具有三个不同的XML解析器：

- QDomDocument——DOM解析器,QtXML的一部分
- QXmlSimpleReader——推送(事件)解析器,是QtXML的一部分
- QXmlStreamReader——Pull解析器,是QtCore的一部分,现在是推荐的解析器

## 1.Public Functions

- QDomDocument(const QDomDocument &x)

- QDomDocument(const QDomDocumentType &doctype)

- QDomDocument(const QString &name)

- QDomDocument()

- QDomDocument &operator=(const QDomDocument &x)

- ~QDomDocument()

- **`QDomAttr createAttribute(const QString &name)`**

  创建一个名为name的新属性，该属性可以插入到元素中，例如 使用QDomElement :: setAttributeNode（）。
  如果name不是有效的XML名称，则此函数的行为由QDomImplementation :: InvalidDataPolicy控制。

- QDomAttr createAttributeNS(const QString &nsURI, const QString &qName)

  创建一个具有名称空间支持的新属性，该属性可以插入到元素中。 该属性的名称为qName，名称空间URI为nsURI。 此函数还将QDomNode :: prefix（）和QDomNode :: localName（）设置为适当的值（取决于qName）。
  如果qName不是有效的XML名称，则此函数的行为由QDomImplementation :: InvalidDataPolicy控制。

- QDomCDATASection createCDATASection(const QString &value)

  为可以插入文档中的字符串值创建一个新的CDATA部分，例如 使用QDomNode :: appendChild（）。
  如果value包含无法存储在CDATA节中的字符，则此函数的行为由QDomImplementation :: InvalidDataPolicy控制。

- QDomComment createComment(const QString &value)

  为可以插入文档中的字符串值创建新注释，例如 使用QDomNode :: appendChild（）。
  如果value包含无法存储在XML注释中的字符，则此函数的行为由QDomImplementation :: InvalidDataPolicy控制。

- QDomDocumentFragment createDocumentFragment()

  创建一个新的文档片段，该片段可用于保存文档的某些部分，例如 在对文档树进行复杂操作时。

- **`QDomElement createElement(const QString &tagName)`**

  创建一个名为tagName的新元素，该元素可以插入DOM树中，例如 使用QDomNode :: appendChild（）。
  如果tagName不是有效的XML名称，则此函数的行为由QDomImplementation :: InvalidDataPolicy控制。

- QDomElement createElementNS(const QString &nsURI, const QString &qName)

  创建一个具有名称空间支持的新元素，可以将其插入DOM树。 元素的名称为qName，名称空间URI为nsURI。 此函数还将QDomNode :: prefix（）和QDomNode :: localName（）设置为适当的值（取决于qName）。
  如果qName是空字符串，则无论是否设置了无效的数据策略，都将返回null元素。

- QDomEntityReference createEntityReference(const QString &name)

  创建一个名为name的新实体引用，该实体引用可以插入文档中，例如 使用QDomNode :: appendChild（）。
  如果name不是有效的XML名称，则此函数的行为由QDomImplementation :: InvalidDataPolicy控制。

- **`QDomProcessingInstruction createProcessingInstruction(const QString &target, const QString &data)`**

  创建可以插入文档的新处理指令，例如 使用QDomNode :: appendChild（）。 该功能将处理指令的目标设置为目标，将数据设置为数据。
如果target不是有效的XML名称，或者data如果包含的字符不能出现在处理指令中，则此函数的行为由QDomImplementation :: InvalidDataPolicy控制。
  
- **`QDomText createTextNode(const QString &value)`**

  为可插入文档树的字符串值创建一个文本节点，例如 使用QDomNode :: appendChild（）。
  如果value包含无法存储为XML文档的字符数据的字符（即使是以字符引用的形式），则此函数的行为由QDomImplementation :: InvalidDataPolicy支配。

- QDomDocumentType doctype() const

  返回此文档的文档类型。

- **QDomElement documentElement() const**

  返回文档的根元素。

- QDomElement elementById(const QString &elementId)

  返回其ID等于elementId的元素。 如果未找到具有ID的元素，则此函数返回空元素。
  由于QDomClasses不知道哪些属性是元素ID，因此此函数始终返回空元素。 这可能会在将来的版本中更改。

- QDomNodeList elementsByTagName(const QString &tagname) const

  返回一个QDomNodeList，它包含文档中所有名称为tagname的元素。 节点列表的顺序是在元素树的预遍历中遇到它们的顺序。

- QDomNodeList elementsByTagNameNS(const QString &nsURI, const QString &localName)

  返回一个QDomNodeList，它包含文档中所有具有本地名称localName和名称空间URI nsURI的元素。 节点列表的顺序是在元素树的预遍历中遇到它们的顺序。

- QDomImplementation implementation() const

  返回一个QDomImplementation对象。

- **QDomNode importNode(const QDomNode &importedNode, bool deep)**

  将节点importedNode从另一个文档导入到此文档。 ImportedNode保留在原始文档中； 此功能创建可在本文档中使用的副本。
  此函数返回属于此文档的导入节点。 返回的节点没有父节点。 无法导入QDomDocument和QDomDocumentType节点。 在那种情况下，此函数返回一个空节点。
  如果importedNode是一个空节点，则返回一个空节点。
  如果deep为true，则此函数不仅导入节点importedNode，还导入整个子树； 如果为false，则仅导入importedNode。 deep参数对QDomAttr和QDomEntityReference节点没有影响，因为QDomAttr节点的后代始终被导入，而QDomEntityReference节点的后代则永远不被导入。
  根据节点类型，此功能的行为略有不同：

  | Node Type                 | Behavior                                                     |
  | ------------------------- | ------------------------------------------------------------ |
  | QDomAttr                  | owner元素设置为0，并且在生成的属性中将指定标志设置为true。 始终为属性节点导入importedNode的整个子树：deep无效。 |
  | QDomDocument              | 无法导入文档节点。                                           |
  | QDomDocumentFragment      | 如果deep为true，则此函数导入整个文档片段； 否则，它只会生成一个空文档片段。 |
  | QDomDocumentType          | 文档类型节点无法导入。                                       |
  | QDomElement               | QDomAttr :: specified（）为true的属性也将导入，而其他属性则不会导入。 如果deep为true，则此函数还导入importedNode的子树； 否则，它仅导入元素节点（以及一些属性，请参见上文）。 |
  | QDomEntity                | 可以导入实体节点，但是由于文档类型在DOM级别2中是只读的，因此目前无法使用它们。 |
  | QDomEntityReference       | 实体引用节点的后代永远不会被导入：Deep无效。                 |
  | QDomNotation              | 可以导入符号节点，但是由于文档类型在DOM级别2中是只读的，因此目前无法使用它们。 |
  | QDomProcessingInstruction | 处理指令的目标和值将复制到新节点。                           |
  | QDomText                  | 文本将复制到新节点。                                         |
  | QDomCDATASection          | 文本将复制到新节点。                                         |
  | QDomComment               | 文本将复制到新节点。                                         |

  

- QDomNode::NodeType nodeType() const

  返回 DocumentNode.

- bool setContent(const QByteArray &data, bool namespaceProcessing, QString *errorMsg = nullptr, int *errorLine = nullptr, int *errorColumn = nullptr)

  此函数从字节数组数据中解析XML文档，并将其设置为文档的内容。它尝试检测XML规范要求的文档编码。
  如果namespaceProcessing为true，则解析器将识别XML文件中的名称空间，并将前缀名称，本地名称和名称空间URI设置为适当的值。如果namespaceProcessing为false，则解析器在读取XML文件时不进行名称空间处理。
  如果发生解析错误，则此函数返回false并将错误消息放置在* errorMsg中，* errorLine中的行号和* errorColumn中的列号（除非关联的指针设置为0）；否则，此函数返回true。 QXmlParseException类文档中描述了各种错误消息。请注意，如果您想将这些错误消息显示给应用程序的用户，除非明确翻译，否则它们将以英文显示。
  如果namespaceProcessing为true，则函数QDomNode :: prefix（）返回所有元素和属性的字符串。如果元素或属性没有前缀，则返回一个空字符串。
  仅包含空格的文本节点将被删除，并且不会出现在QDomDocument中。如果不需要此行为，则可以使用setContent（）重载，该重载允许提供QXmlReader。
  如果namespaceProcessing为false，则函数QDomNode :: prefix（），QDomNode :: localName（）和QDomNode :: namespaceURI（）返回空字符串。

  实体引用的处理方式如下：

  - 包括对内容中出现的内部通用实体和字符实体的引用。 结果是QDomText节点，其中引用被其对应的实体值替换。
  - 包括对内部子集中出现的参数实体的引用。 结果是QDomDocumentType节点，其中包含实体和表示法声明，并用相应的实体值替换了引用。
  - 内部子集中未定义但在内容中出现的任何常规已解析实体引用都表示为QDomEntityReference节点。
  - 内部子集中未定义但在内容外部出现的所有已解析实体引用都将替换为空字符串。
  - 任何未解析的实体引用都将替换为空字符串。

- bool setContent(const QString &text, bool namespaceProcessing, QString *errorMsg = nullptr, int *errorLine = nullptr, int *errorColumn = nullptr)

  该函数从字符串文本中读取XML文档，如果内容已成功解析，则返回true； 否则返回false。 由于文本已经是Unicode字符串，因此不会进行编码检测。

- bool setContent(QIODevice *dev, bool namespaceProcessing, QString *errorMsg = nullptr, int *errorLine = nullptr, int *errorColumn = nullptr)

  此函数从IO设备开发人员读取XML文档，如果内容已成功解析，则返回true；否则，返回true。 否则返回false。

- bool setContent(const QByteArray &buffer, QString *errorMsg = nullptr, int *errorLine = nullptr, int *errorColumn = nullptr)

  该函数从字节数组缓冲区中读取XML文档，如果内容已成功解析，则返回true；否则，返回true。 否则返回false。
  不执行名称空间处理。

- bool setContent(const QString &text, QString *errorMsg = nullptr, int *errorLine = nullptr, int *errorColumn = nullptr)

  该函数从字符串文本中读取XML文档，如果内容已成功解析，则返回true；否则，返回true。 否则返回false。 由于文本已经是Unicode字符串，因此不会执行编码检测。
  也不执行名称空间处理。

- bool setContent(QXmlStreamReader *reader, bool namespaceProcessing, QString *errorMsg = nullptr, int *errorLine = nullptr, int *errorColumn = nullptr)

  此函数从QXmlStreamReader阅读器读取XML文档并进行解析。 如果内容已成功解析，则返回true；否则，返回true。 否则返回false。
  如果namespaceProcessing为true，则解析器将识别XML文件中的名称空间，并将前缀名称，本地名称和名称空间URI设置为适当的值。 如果namespaceProcessing为false，则解析器在读取XML文件时不进行名称空间处理。
  如果发生解析错误，则错误消息将放置在* errorMsg中，行号将放置在* errorLine中，列号将放置在* errorColumn中（除非关联的指针设置为0）。

- QByteArray toByteArray(int indent = 1) const

  将已解析的文档转换回其文本表示形式，并返回一个QByteArray，其中包含编码为UTF-8的数据。
  此函数使用缩进作为缩进子元素的空间量。

- QString toString(int indent = 1) const

  将已解析的文档转换回其文本表示形式。
  此函数使用缩进作为缩进子元素的空间量。
  如果indent为-1，则根本不添加空格。

## 2.Detailed Description

