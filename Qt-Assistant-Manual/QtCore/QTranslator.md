# QTranslator

继承关系：`QTranslator`->`QObject`

## 1.Public Functions

- QTranslator ( QObject * parent = 0 )

- ~QTranslator ()

- virtual bool	isEmpty () const

  如果此转换器为空，则返回true，否则返回false。 此功能适用于已剥离和未剥离的翻译文件。

- `bool	load ( const QString & filename, const QString & directory = QString(), const QString & search_delimiters = QString(), const QString & suffix = QString() )`

  加载filename+suffix（如果未指定后缀，则为“ .qm”），这可以是绝对文件名，也可以是相对于目录的后缀。 如果翻译成功加载，则返回true；否则，返回false。 

  如果未指定目录，则使用应用程序可执行文件的目录（即，作为applicationDirPath（））。

  该翻译器对象的先前内容将被丢弃。

  如果文件名不存在，则按以下顺序尝试其他文件名：

  - 不带后缀的文件名。
  - 去除了search_delimiters中的字符后带有文本的文件名（如果为空字符串，则“ _。”是search_delimiters的默认值）和后缀。
  - 删除文件名，不附加后缀。
  - 文件名进一步剥离，等等。

  例如，在fr_CA语言环境（讲法语的加拿大）中运行的应用程序可能会调用load（“ foo.fr_ca”，“ / opt / foolib”）。 然后load（）将尝试从此列表中打开第一个现有的可读文件：

  - 1./opt/foolib/foo.fr_ca.qm
  - 2./opt/foolib/foo.fr_ca
  - 3./opt/foolib/foo.fr.qm
  - 4./opt/foolib/foo.fr
  - 5./opt/foolib/foo.qm
  - 6./opt/foolib/foo

- `bool	load ( const QLocale & locale, const QString & filename, const QString & prefix = QString(), const QString & directory = QString(), const QString & suffix = QString() )`

  加载filename+prefix + ui language name +suffix（如果未指定后缀，则为“ .qm”），这可以是绝对文件名，也可以是相对于目录的。 如果翻译加载成功，则返回true；否则返回false。

  该翻译器对象的先前内容将被丢弃。

  如果文件名不存在，则按以下顺序尝试其他文件名：

  - /opt/foolib/foo.es.qm
  - /opt/foolib/foo.es
  - /opt/foolib/foo.fr_CA.qm
  - /opt/foolib/foo.fr_CA
  - /opt/foolib/foo.de.qm
  - /opt/foolib/foo.de
  - /opt/foolib/foo.fr.qm
  - /opt/foolib/foo.fr
  - /opt/foolib/foo.qm
  - /opt/foolib/foo.
  - /opt/foolib/foo

  在文件系统区分大小写的操作系统上，QTranslator也尝试加载语言环境名称的小写版本。

- `bool	load ( const uchar * data, int len )`

  将长度为len的QM文件数据数据加载到转换器中。

  数据不被复制。 调用者必须能够保证不会删除或修改数据。

- `virtual QString	translate ( const char * context, const char * sourceText, const char * disambiguation = 0 ) const`

  返回键的翻译（上下文，sourceText，歧义消除）。 如果没有找到，也尝试（上下文，sourceText，“”）。 如果仍然失败，则返回一个空字符串。

  如果您需要以编程方式将翻译插入到QTranslator中，则可以重新实现此功能。

- `QString	translate ( const char * context, const char * sourceText, const char * disambiguation, int n ) const`

  返回键的翻译（上下文，sourceText，歧义消除）。 如果没有找到，也尝试（上下文，sourceText，“”）。 如果仍然失败，则返回一个空字符串。

  如果n不为-1，则用于选择适当的翻译形式（例如，“找到％n个文件”与“找到％n个文件”）。

## 2.Detailed Description

QTranslator类为文本输出提供国际化支持。

此类的对象包含一组从源语言到目标语言的翻译。 QTranslator提供了在翻译文件中查找翻译的功能。 翻译文件是使用Qt语言学家创建的。

QTranslator的最常见用法是：加载翻译文件，使用QApplication :: installTranslator（）安装它，然后通过QObject :: tr（）使用它。 这是Hello tr（）示例中的main（）函数：

```c++
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);

    QTranslator translator;
    translator.load("hellotr_la");
    app.installTranslator(&translator);

    QPushButton hello(QPushButton::tr("Hello world!"));
    hello.resize(100, 30);

    hello.show();
    return app.exec();
}
```

请注意，**必须在应用程序的widgets之前创建翻译器**。

大多数应用程序永远都不需要对此类进行任何其他操作。 此类提供的其他功能对使用翻译器文件的应用程序很有用。

### Looking up Translations

可以使用translate（）查找翻译（就像tr（）和QApplication :: translate（）一样）。 translate（）函数最多包含三个参数：

- 上下文context-通常是tr（）调用者的类名。
- 源文本source-通常是tr（）的参数。
- 消除歧义disambiguation-可选字符串，有助于消除在相同上下文中相同文本的不同用法。

例如，当程序以波兰语运行时，对话框中的“取消”可能带有“ Anuluj”（在这种情况下，源文本为“取消”）。 上下文（通常）是对话框的类名； 通常不会有任何评论，而翻译后的文本将是“ Anuluj”。

但这并不总是那么简单。 具有双面打印和装订设置的西班牙语对话框的打印机对话框可能需要同时使用“ Activado”和“ Activada”作为“启用”的翻译。 在这种情况下，两种情况下的源文本都将为“启用”，而上下文将为对话框的类名，但是这两项将具有歧义，例如，其中一个使用“双面打印”，另一个使用“绑定”。 歧义消除使翻译人员能够为西班牙语版本选择适当的性别，并使Qt能够区分翻译。

### Using Multiple Translations

**可以在一个应用程序中安装多个翻译文件**。 将按照安装时的**相反顺序搜索翻译**，因此首先搜索最新安装的翻译文件以查找翻译，然后搜索最早的翻译文件。 **一旦找到包含匹配字符串的翻译，搜索就会停止**。

这种机制使“翻译”的选择或相对于其他翻译的优先级成为可能。 只需将翻译器传递到QApplication :: removeTranslator（）函数从应用程序中将其卸载，然后使用QApplication :: installTranslator（）重新安装它即可。 然后它将是第一个要搜索匹配字符串的翻译。