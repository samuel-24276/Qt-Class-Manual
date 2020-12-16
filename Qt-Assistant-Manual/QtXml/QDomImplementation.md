# QDomImplementation

## 1.Public Types

- enum	InvalidDataPolicy { AcceptInvalidChars, DropInvalidChars, ReturnNullNode }

## 2.Public Functions

- QDomImplementation ()

- QDomImplementation ( const QDomImplementation & x )

- ~QDomImplementation ()

- QDomDocument	createDocument ( const QString & nsURI, const QString & qName, const QDomDocumentType & doctype )

  创建文档类型为doctype的DOM文档。 此函数还添加了具有限定名称qName和名称空间URI nsURI的根元素节点。

- QDomDocumentType	createDocumentType ( const QString & qName, const QString & publicId, const QString & systemId )

  为名称qName创建一个文档类型节点。

  publicId指定外部子集的公共标识符。如果将空字符串（QString（））指定为publicId，则意味着文档类型没有公共标识符。

  systemId指定外部子集的系统标识符。如果将空字符串指定为systemId，则意味着文档类型没有系统标识符。

  由于没有系统标识符就无法拥有公共标识符，因此如果没有系统标识符，则将公共标识符设置为空字符串。

  DOM 2级不支持任何其他文档类型声明功能。

  **使用创建的文档类型的唯一方法是与createDocument（）函数结合使用，以创建具有此文档类型的QDomDocument**。

  在DOM规范中，这是创建非null文档的唯一方法。由于历史原因，Qt还允许使用默认的空构造函数创建文档。结果文档为null，但在调用工厂函数（例如QDomDocument :: createElement（））时变为非null。调用setContent（）时，文档也将变为非null。

- bool	hasFeature ( const QString & feature, const QString & version ) const

  如果QDom实现了功能的请求版本，则该函数返回true； 否则返回false。

- bool	isNull ()

  如果对象是由QDomDocument :: implementation（）创建的，则返回false。 否则返回true。

- bool	operator!= ( const QDomImplementation & x ) const

- QDomImplementation &	operator= ( const QDomImplementation & x )

- bool	operator== ( const QDomImplementation & x ) const

## 3.Static Public Members

- InvalidDataPolicy	invalidDataPolicy ()

  返回无效数据策略，该策略指定当QDomDocument中的工厂函数传递无效数据时应执行的操作。

  警告：此函数不可重入（reentrant）。

- void	setInvalidDataPolicy ( InvalidDataPolicy policy )

  设置无效数据策略，该策略指定当QDomDocument中的工厂函数传递无效数据时应执行的操作。

  为所有已经存在并将在以后创建的QDomDocument实例设置该策略。

  ```c++
  QDomDocument doc;
  QDomImplementation impl;
  
  // This will create the element, but the resulting XML document will
  // be invalid, because '~' is not a valid character in a tag name.
  impl.setInvalidDataPolicy(QDomImplementation::AcceptInvalidData);
  QDomElement elt1 = doc.createElement("foo~bar");
  
  // This will create an element with the tag name "foobar".
  impl.setInvalidDataPolicy(QDomImplementation::DropInvalidData);
  QDomElement elt2 = doc.createElement("foo~bar");
  
  // This will create a null element.
  impl.setInvalidDataPolicy(QDomImplementation::ReturnNullNode);
  QDomElement elt3 = doc.createElement("foo~bar");
  ```

## 4.Detailed Description

QDomImplementation类提供有关DOM实现功能的信息。

此类描述DOM实现所支持的功能。 当前支持DOM级别1和DOM级别2核心的XML子集。

通常，您将使用函数QDomDocument :: implementation（）获取实现对象。

您可以使用createDocumentType（）创建一个新的文档类型，并使用createDocument（）创建一个新的文档。

有关文档对象模型的更多信息，请参见1级和2级核心。 有关DOM实现的更一般性介绍，请参见QDomDocument文档。

QDom类存在一些与XML规范不一致的问题，这些问题不能在Qt 4中解决而不破坏向后兼容性。 QtXmlPatterns模块以及QXmlStreamReader和QXmlStreamWriter类具有更高的一致性。