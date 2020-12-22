# QDomAttr

继承关系：`QDomAttr`->`QDomNode`

## 1.Public Functions

- QDomAttr ()

- QDomAttr ( const QDomAttr & x )

- QString	name () const

- QDomNode::NodeType	nodeType () const

- QDomElement	ownerElement () const

  返回此属性附加到的元素节点；如果此属性未附加到任何元素，则返回空节点。

- void	setValue ( const QString & v )

- bool	specified () const

  如果用户已使用setValue（）设置了属性，则返回true。 如果未指定或设置值，则返回false。

- QString	value () const

- QDomAttr &	operator= ( const QDomAttr & x )

## 2.Detailed Description

QDomAttr类表示QDomElement的一个属性。

例如，以下XML产生的元素没有子元素，但是有两个属性：

```xml
 <link href="http://qt.nokia.com" color="red" />
```

您可以使用以下代码访问元素的属性：

```c++
 QDomElement e = //...
 //...
 QDomAttr a = e.attributeNode("href");
 cout << a.value() << endl;                // prints "http://qt.nokia.com"
 a.setValue("http://qt.nokia.com/doc"); // change the node's attribute
 QDomAttr a2 = e.attributeNode("href");
 cout << a2.value() << endl;          // prints	"http://qt.nokia.com/doc"
```

此示例还显示，更改从元素接收的属性会更改元素的属性。 **如果不想更改元素属性的值，则必须使用cloneNode（）获得属性的独立副本**。

QDomAttr可以返回属性的name（）和value（）。 使用setValue（）设置属性的值。 如果指定的（）返回true，则使用setValue（）设置值。 此属性附加到的节点（如果有）由ownerElement（）返回。