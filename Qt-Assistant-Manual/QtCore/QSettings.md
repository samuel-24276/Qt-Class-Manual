# QSettings

继承关系：`QSettings`->`QObject`

# 1.Detailed Description

用户通常希望**应用程序在整个会话中记住其设置（窗口大小和位置，选项等）**。 此信息通常存储在Windows上的系统注册表中，以及macOS和iOS上的属性列表文件中。 **在Unix系统上，在没有标准的情况下，许多应用程序（包括KDE应用程序）都使用INI文本文件**。

QSettings是围绕这些技术的抽象，使您能够以可移植的方式保存和恢复应用程序设置。 它还支持自定义存储格式。

QSettings的API基于QVariant，使您可以省力地保存大多数基于值的类型，例如QString，QRect和QImage。

如果您需要的只是一个基于非持久性内存的结构，请考虑改用QMap <QString，QVariant>。

## 1.1.Basic Usage

创建QSettings对象时，必须传递公司或组织的名称以及应用程序的名称。 例如，如果您的产品称为Star Runner，而您的公司称为MySoft，则可以按以下方式构造QSettings对象：

` QSettings settings("MySoft", "Star Runner");`

QSettings对象可以在堆栈或堆上创建（即使用new）。 构造和销毁QSettings对象非常快。

如果您从应用程序中的许多地方使用QSettings，则可能要使用QCoreApplication :: setOrganizationName（）和QCoreApplication :: setApplicationName（）来指定组织名称和应用程序名称，然后使用默认的QSettings构造函数：

```c++
     QCoreApplication::setOrganizationName("MySoft");
     QCoreApplication::setOrganizationDomain("mysoft.com");
     QCoreApplication::setApplicationName("Star Runner");
     ...
     QSettings settings;
```

（在此，我们还指定了组织的Internet域。设置了Internet域后，它会在macOS和iOS上使用，而不是在组织名称上使用，因为macOS和iOS应用程序通常会使用Internet域来标识自己。如果未设置任何域， 假域名来自组织名称。有关详细信息，请参见下面的“特定于平台的说明”。）
QSettings存储设置。 每个设置都由一个QString和一个QVariant组成，QString指定设置的名称（键），QVariant存储与键相关联的数据。 要编写设置，请使用setValue（）。 例如：

` settings.setValue("editor/wrapMargin", 68);`

如果已经存在具有相同键的设置，则现有值将被新值覆盖。 为了提高效率，所做的更改可能不会立即保存到永久存储中。 （您始终可以调用sync（）提交更改。）

您可以使用value（）获取设置的值：

` int margin = settings.value("editor/wrapMargin").toInt();`

如果没有具有指定名称的设置，则QSettings返回一个空QVariant（可以将其转换为整数0）。 您可以通过将第二个参数传递给value（）来指定另一个默认值：

` int margin = settings.value("editor/wrapMargin", 80).toInt();`

要测试给定密钥是否存在，请调用contains（）。 要删除与键关联的设置，请调用remove（）。 要获取所有键的列表，请调用allKeys（）。 要删除所有键，请调用clear（）。

## 1.2.QVariant and GUI Types

由于QVariant是Qt Core模块的一部分，因此它无法提供对Qt GUI的一部分的数据类型（例如QColor，QImage和QPixmap）的转换功能。 换句话说，在QVariant中没有toColor（），toImage（）或toPixmap（）函数。
相反，您可以使用QVariant :: value（）模板函数。 例如：

```c++
 QSettings settings("MySoft", "Star Runner");
 QColor color = settings.value("DataPump/bgcolor").value<QColor>();
```

对于QVariant支持的所有数据类型，包括与GUI相关的类型，将自动进行逆转换（例如，从QColor到QVariant）：

```c++
 QSettings settings("MySoft", "Star Runner");
 QColor color = palette().background().color();
 settings.setValue("DataPump/bgcolor", color);
```

可以使用QSettings存储使用qRegisterMetaType（）和qRegisterMetaTypeStreamOperators（）注册的自定义类型。

## 1.3.Section and Key Syntax

设置键可以包含任何Unicode字符。 Windows注册表和INI文件使用不区分大小写的键，而macOS和iOS上的CFPreferences API使用不区分大小写的键。 为避免可移植性问题，请遵循以下简单规则：

- 始终使用相同的大小写引用
- 相同的键。 例如，如果在代码中的某个位置将键称为“文本字体”，则不要在其他地方将其称为“文本字体”。
- 除大小写外，请避免使用相同的键名。 例如，如果您有一个名为“ MainWindow”的键，请不要尝试将另一个键另存为“ mainwindow”。
- 在节或键名中不要使用斜杠（“ /”和“ \”）； 反斜杠字符用于分隔子键（请参见下文）。 在Windows上，QSettings将“ \”转换为“ /”，从而使它们相同。

您可以使用'/'字符作为分隔符来形成分层键，类似于Unix文件路径。 例如：

```c++
     settings.setValue("mainwindow/size", win->size());
     settings.setValue("mainwindow/fullScreen", win->isFullScreen());
     settings.setValue("outputpanel/visible", panel->isVisible());
```

**如果要保存或恢复具有相同前缀的许多设置，则可以使用beginGroup（）指定前缀，并在末尾调用endGroup（）**。 这再次是相同的示例，但是这次使用组机制：

```c++
settings.beginGroup("mainwindow");
settings.setValue("size", win->size());
settings.setValue("fullScreen", win->isFullScreen());
settings.endGroup();

settings.beginGroup("outputpanel");
settings.setValue("visible", panel->isVisible());
settings.endGroup();
```

如果使用beginGroup（）设置了一个组，则大多数函数的行为都会改变。 可以递归设置组。
除了组之外，QSettings还支持“数组”概念。 有关详细信息，请参见beginReadArray（）和beginWriteArray（）。

## 1.4.Fallback Mechanism后备机制

假设您创建了一个QSettings对象，其组织名称为MySoft，应用程序名称为Star Runner。当您查询一个值时，将最多搜索四个位置：

- Star Runner应用程序的用户特定位置
- MySoft所有应用程序的用户特定位置
- Star Runner应用程序在系统范围内的位置
- MySoft在所有应用程序的系统范围内的位置

（有关Qt支持的不同平台上这些位置的信息，请参阅下面的特定于平台的说明。）

如果在第一个位置找不到密钥，则在第二个位置继续搜索，依此类推。这使您可以存储系统范围或组织范围的设置，并可以基于每个用户或每个应用程序覆盖它们。要关闭此机制，请调用setFallbacksEnabled（false）。

**尽管可以从所有四个位置读取密钥，但是只能访问第一个文件（手头应用程序的用户特定位置）进行写入**。要写入任何其他文件，请省略应用程序名称和/或指定QSettings :: SystemScope（与默认设置QSettings :: UserScope相对）。
让我们看一个例子：

```c++
QSettings obj1("MySoft", "Star Runner");
QSettings obj2("MySoft");
QSettings obj3(QSettings::SystemScope, "MySoft", "Star Runner");
QSettings obj4(QSettings::SystemScope, "MySoft");
```

下表总结了哪些QSettings对象访问哪个位置。 **“ X”表示该位置是与QSettings对象关联的主要位置，并且用于读取和写入**。 “ o”表示该位置在读取时用作备用。

| Locations               | obj1 | obj2 | obj3 | obj4 |
| ----------------------- | ---- | ---- | ---- | ---- |
| 1. User, Application    | X    |      |      |      |
| 2. User, Organization   | o    | X    |      |      |
| 3. System, Application  | o    |      | X    |      |
| 4. System, Organization | o    | o    | o    | X    |

这种机制的优点在于，它可以在Qt支持的所有平台上运行，并且仍然为您提供了很大的灵活性，而无需您指定任何文件名或注册表路径。

如果要在所有平台上使用INI文件而不是本机API，则可以将QSettings :: IniFormat作为第一个参数传递给QSettings构造函数，然后是范围，组织名称和应用程序名称：

```c++
QSettings settings(QSettings::IniFormat, QSettings::UserScope,
                        "MySoft", "Star Runner");
```

请注意，从INI文件读取设置时不会保留类型信息。 所有值将作为QString返回。

设置编辑器示例可让您尝试不同的设置位置以及启用或禁用后备广告。

## 1.5.Restoring the State of a GUI Application恢复GUI应用程序的状态

QSettings通常用于存储GUI应用程序的状态。 下面的示例说明如何使用QSettings保存和还原应用程序主窗口的几何。

```c++
 void MainWindow::writeSettings()
 {
     QSettings settings("Moose Soft", "Clipper");

     settings.beginGroup("MainWindow");
     settings.setValue("size", size());
     settings.setValue("pos", pos());
     settings.endGroup();
 }

 void MainWindow::readSettings()
 {
     QSettings settings("Moose Soft", "Clipper");

     settings.beginGroup("MainWindow");
     resize(settings.value("size", QSize(400, 400)).toSize());
     move(settings.value("pos", QPoint(200, 200)).toPoint());
     settings.endGroup();
 }
```

有关为什么最好调用QWidget :: resize（）和QWidget :: move（）而不是QWidget :: setGeometry（）来恢复窗口几何的讨论，请参见窗口几何。

必须从主窗口的构造函数和close事件处理程序中调用readSettings（）和writeSettings（）函数，如下所示：

```C++
MainWindow::MainWindow()
{
	...
	readSettings();
}

void MainWindow::closeEvent(QCloseEvent *event)
{
	if (userReallyWantsToQuit()) {
		writeSettings();
		event->accept();
	} else {
		event->ignore();
    }
}
```

## 1.6.Accessing Settings from Multiple Threads or Processes Simultaneously同时从多个线程或进程访问设置

QSettings是可重入的。这意味着您可以同时在不同的线程中使用不同的QSettings对象。即使QSettings对象引用磁盘上的相同文件（或系统注册表中的相同条目），该保证仍然有效。如果通过一个QSettings对象修改了设置，则该更改将立即在任何在同一位置运行且处于同一进程中的其他QSettings对象中可见。

只要满足某些条件，就可以从不同的进程（可以是同时运行的应用程序的不同实例，也可以是完全不同的应用程序）安全地使用QSettings来读写相同的系统位置。对于QSettings :: IniFormat，它使用咨询文件锁定和智能合并算法来确保数据完整性。工作的条件是可写配置文件必须是常规文件，并且必须位于当前用户可以在其中创建新的临时文件的目录中。如果不是这种情况，则必须使用setAtomicSyncRequired（）关闭安全装置。

请注意，sync（）导入其他进程所做的更改（除了从此QSettings写入更改之外）。

# 2.Public Types

- enum Format { NativeFormat, Registry32Format, 

  Registry64Format, IniFormat, InvalidFormat }

  此枚举类型指定QSettings使用的存储格式。

  | Constant                    | Value | Description                                                  |
  | --------------------------- | ----- | ------------------------------------------------------------ |
  | QSettings::NativeFormat     | 0     | **使用最适合平台的存储格式存储设置**。 在Windows上，这意味着系统注册表。 在macOS和iOS上，这意味着CFPreferences API； 在Unix上，这意味着INI格式的文本配置文件。 |
  | QSettings::Registry32Format | 2     | **仅限Windows：从在64位Windows上运行的64位应用程序显式访问32位系统注册表**。 在32位Windows上或从64位Windows上的32位应用程序中，其作用与指定NativeFormat相同。 |
  | QSettings::Registry64Format | 3     | **仅限Windows：从在64位Windows上运行的32位应用程序显式访问64位系统注册表**。 在32位Windows上或从64位Windows上的64位应用程序中，其工作原理与指定NativeFormat相同。 |
  | QSettings::IniFormat        | 1     | **将设置存储在INI文件中**。 请注意，从INI文件读取设置时不会保留类型信息。 所有值将作为QString返回。 |
  | QSettings::InvalidFormat    | 16    | registerFormat（）返回的特殊值。                             |

  在Unix上，NativeFormat和IniFormat含义相同，不同之处在于文件扩展名不同（.conf用于NativeFormat，.ini用于IniFormat）。
  INI文件格式是Qt在所有平台上都支持的Windows文件格式。在没有INI标准的情况下，我们尝试遵循Microsoft的操作，但以下情况除外：
  如果您存储QVariant无法转换为QString的类型（例如QPoint，QRect和QSize），则Qt使用基于@的语法对类型进行编码。例如：
   `pos = @Point（100 100）`

  为了最大程度地减少**兼容性问题**，任何未出现在值的第一个位置或其后没有Qt类型（Point, Rect, Size, etc.）的@均被视为普通字符。
  尽管反斜杠是INI文件中的特殊字符，但是大多数Windows应用程序都不会在文件路径中转义反斜杠（\）：
   `windir= C：\ Windows`
  **QSettings始终将反斜杠视为特殊字符，并且不提供用于读取或写入此类条目的API**。
  INI文件格式对键的语法有严格的限制。 **Qt通过使用％作为键中的转义字符来解决此问题**。此外，如果您保存一个顶级设置（其中没有反斜杠的键，例如“ someKey”），它将显示在INI文件的“常规”部分中。为避免覆盖其他键，如果您使用诸如“ General / someKey”之类的键来保存内容，则该键将位于“％General”部分，而不是“ General”部分。
  遵循我们应该在**接受内容时保持自由和在生成内容时保持保守**的理念，QSettings将接受Latin-1编码的INI文件，但生成纯ASCII文件，其中非ASCII值使用标准INI转义序列进行编码。**为了使INI文件更具可读性（但兼容性可能较低），请调用setIniCodec（）**。

- typedef ReadFunc

  Typedef指向具有以下签名的函数的指针：

  ` bool myReadFunc(QIODevice &device, QSettings::SettingsMap &map);`

  ReadFunc在registerFormat（）中用作指向读取一组键/值对的函数的指针。 ReadFunc应该一次性读取所有选项，并返回SettingsMap容器中的所有设置，该容器最初为空。

- enum Scope { UserScope, SystemScope }

  该枚举指定设置是用户特定的还是由同一系统的所有用户共享的。

  | Constant               | Value | Description                                                  |
  | ---------------------- | ----- | ------------------------------------------------------------ |
  | QSettings::UserScope   | 0     | 将设置存储在特定于当前用户的位置（例如，在用户的主目录中）。 |
  | QSettings::SystemScope | 1     | 将设置存储在全局位置，以便同一台计算机上的所有用户都可以访问同一组设置。 |

  

- typedef SettingsMap

  Typedef for **QMap<QString, QVariant)>**

- enum Status { NoError, AccessError, FormatError }

  以下状态值是可能的：

  - QSettings::NoError
  - QSettings::AccessError
  - QSettings::FormatError

- typedef WriteFunc

  Typedef指向具有以下签名的函数的指针：

  `bool myWriteFunc(QIODevice &device, const QSettings::SettingsMap &map);`

  WriteFunc在registerFormat（）中用作指向写入一组键/值对的函数的指针。 WriteFunc仅被调用一次，因此您需要一次性输出设置。

# 3.Public Functions

- `QSettings(QSettings::Scope scope, QObject *parent = nullptr)`

- `QSettings(QObject *parent = nullptr)`

- `QSettings(const QString &fileName, QSettings::Format format, QObject *parent = nullptr)`

  参数format指定QSettings使用的存储格式。

- `QSettings(QSettings::Format format, QSettings::Scope scope, const QString &organization, const QString &application = QString(), QObject *parent = nullptr)`

- `QSettings(QSettings::Scope scope, const QString &organization, const QString &application = QString(), QObject *parent = nullptr)`

- `QSettings(const QString &organization, const QString &application = QString(), QObject *parent = nullptr)`

- `virtual ~QSettings()`

- **`QStringList allKeys() const`**

  返回可以使用QSettings对象读取的所有键（包括子键）的列表。

  ```c++
  QSettings settings;
  settings.setValue("fridge/color", Qt::white);
  settings.setValue("fridge/size", QSize(32, 96));
  settings.setValue("sofa", true);
  settings.setValue("tv", false);
  
  QStringList keys = settings.allKeys();
  // keys: ["fridge/color", "fridge/size", "sofa", "tv"]
  ```

  如果使用beginGroup（）设置了一个组，则仅返回该组中的键，而没有组前缀：

  ```c++
  settings.beginGroup("fridge");
  keys = settings.allKeys();
  // keys: ["color", "size"]
  ```

- **`void beginGroup(const QString &prefix)`**

  将prefix附加到当前组。

  当前组将自动添加到QSettings指定的所有键之前。 此外，诸如childGroups（），childKeys（）和allKeys（）之类的查询功能均基于该组。 默认情况下，未设置任何组。

  组对于避免重复输入相同的设置路径很有用。 例如：

  ```c++
  settings.beginGroup("mainwindow");
  settings.setValue("size", win->size());
  settings.setValue("fullScreen", win->isFullScreen());
  settings.endGroup();
  
  settings.beginGroup("outputpanel");
  settings.setValue("visible", panel->isVisible());
  settings.endGroup();
  ```

  这将设置三个设置的值：

  - mainwindow/size
  - mainwindow/fullScreen
  - outputpanel/visible

  调用endGroup（）以将当前组重置为相应的beginGroup（）调用之前的状态。 组可以嵌套。

- **`void endGroup()`**

  将组重置为相应的beginGroup（）调用之前的状态。

- **`void setValue(const QString &key, const QVariant &value)`**

  将设置key的值设置为value。 如果key已经存在，则先前的值将被覆盖。

  请注意，**Windows注册表和INI文件使用不区分大小写的键**，而Mac OS X上的Carbon偏好设置API使用区分大小写的键。 为避免可移植性问题，请参见“部分”和“关键语法”规则。

- **`QVariant value(const QString &key, const QVariant &defaultValue = QVariant()) const`**

  返回设置key的值。 如果该设置不存在，则返回defaultValue。

  如果未指定默认值，则返回默认的QVariant。

  请注意，Windows注册表和INI文件使用不区分大小写的键，而Mac OS X上的Carbon偏好设置API使用区分大小写的键。 为避免可移植性问题，请参见“部分”和“关键语法”规则。

- **`bool contains(const QString &key) const`**

  如果存在称为key的设置，则返回true；否则返回false。

  **如果使用beginGroup（）设置了一个组，则将键视为相对于该组的**键。

  请注意，Windows注册表和INI文件使用不区分大小写的键，而Mac OS X上的Carbon偏好设置API使用区分大小写的键。 为避免可移植性问题，请参见“部分”和“关键语法”规则。

- **`void remove(const QString &key)`**

  删除设置key和key的任何子设置。只删除同名key的第一个。

  ```c++
  QSettings settings;
  settings.setValue("ape");
  settings.setValue("monkey", 1);
  settings.setValue("monkey/sea", 2);
  settings.setValue("monkey/doe", 4);
  
  settings.remove("monkey");
  QStringList keys = settings.allKeys();
  // keys: ["ape"]
  ```

  请注意，如果后备位置之一包含具有相同键的设置，则在调用remove（）之后该设置将可见。

  **如果key为空字符串，则将删除当前group（）中的所有键**。 例如：

  ```c++
  QSettings settings;
  settings.setValue("ape");
  settings.setValue("monkey", 1);
  settings.setValue("monkey/sea", 2);
  settings.setValue("monkey/doe", 4);
  
  settings.beginGroup("monkey");
  settings.remove("");
  settings.endGroup();
  
  QStringList keys = settings.allKeys();
  // keys: ["ape"]
  ```

  请注意，Windows注册表和INI文件使用不区分大小写的键，而Mac OS X上的Carbon偏好设置API使用区分大小写的键。 为避免可移植性问题，请参见“部分”和“关键语法”规则。

- **`QStringList childGroups() const`**

  返回所有包含可以使用QSettings对象读取的键的**键顶级组的列表**。

  ```c++
  QSettings settings;
  settings.setValue("fridge/color", Qt::white);
  settings.setValue("fridge/size", QSize(32, 96));
  settings.setValue("sofa", true);
  settings.setValue("tv", false);
  
  QStringList groups = settings.childGroups();
  // groups: ["fridge"]
  ```

  如果使用beginGroup（）设置了一个组，则返回该组中的第一级键，但不带组前缀。

  ```c++
  settings.beginGroup("fridge");
  groups = settings.childGroups();
  // groups: []
  ```

  您可以**递归地使用childKeys（）和childGroups（）浏览整个设置层次结构**。

- **`QStringList childKeys() const`**

  返回可以使用QSettings对象读取的所有**顶级键的列表**。

  ```c++
  QSettings settings;
  settings.setValue("fridge/color", Qt::white);
  settings.setValue("fridge/size", QSize(32, 96));
  settings.setValue("sofa", true);
  settings.setValue("tv", false);
  
  QStringList keys = settings.childKeys();
  // keys: ["sofa", "tv"]
  ```

  如果使用beginGroup（）设置了一个组，则返回该组中的顶级键，但不带组前缀：

  ```c++
  settings.beginGroup("fridge");
  keys = settings.childKeys();
  // keys: ["color", "size"]
  ```

- **`void setIniCodec(QTextCodec *codec)`**

  设置用于访问INI文件（包括Unix上的.conf文件）的编解码器。 编解码器用于解码从INI文件读取的任何数据，以及编码写入该文件的任何数据。 默认情况下，不使用编解码器，并且使用标准INI转义序列对非ASCII字符进行编码。

  警告：在创建QSettings对象之后，必须在访问任何数据之前立即设置编解码器。

  此功能在Qt 4.5中引入。

- `void setIniCodec(const char *codecName)`

  将用于访问INI文件（包括Unix上的.conf文件）的编解码器设置为QTextCodec，以使用codecName指定的编码。 codecName的常用值包括“ ISO 8859-1”，“ UTF-8”和“ UTF-16”。 如果无法识别编码，则不会发生任何事情。

  此功能在Qt 4.5中引入。

- `QString applicationName() const`

  返回用于存储设置的应用程序名称。

- `int beginReadArray(const QString &prefix)`

  将前缀添加到当前组并开始从数组读取。 返回数组的大小。

  ```c++
  struct Login {
      QString userName;
      QString password;
  };
  QList<Login> logins;
  ...
  
  QSettings settings;
  int size = settings.beginReadArray("logins");
  for (int i = 0; i < size; ++i) {
      settings.setArrayIndex(i);
      Login login;
      login.userName = settings.value("userName").toString();
      login.password = settings.value("password").toString();
      logins.append(login);
  }
  settings.endArray();
  ```

- `void beginWriteArray(const QString &prefix, int size = -1)`

  在当前组中添加前缀，并开始写入一个大小为size的数组。 如果size为-1（默认值），则会根据所写条目的索引自动确定大小。

  如果您多次出现某组键，则可以使用数组来简化生活。 例如，假设您要保存一个可变长度的用户名和密码列表。 然后，您可以编写：

  ```c++
  struct Login {
      QString userName;
      QString password;
  };
  QList<Login> logins;
  ...
  
  QSettings settings;
  settings.beginWriteArray("logins");
  for (int i = 0; i < logins.size(); ++i) {
      settings.setArrayIndex(i);
      settings.setValue("userName", list.at(i).userName);
      settings.setValue("password", list.at(i).password);
  }
  settings.endArray();
  ```

  The generated keys will have the form

  - logins/size
  - logins/1/userName
  - logins/1/password
  - logins/2/userName
  - logins/2/password
  - logins/3/userName
  - logins/3/password
  - ...

- `void endArray()`

  关闭使用beginReadArray（）或beginWriteArray（）启动的数组。

- `void setArrayIndex(int i)`

  将当前数组索引设置为i。 对setValue（），value（），remove（）和contains（）之类的函数的调用将在该索引处的数组条目上进行。

  **必须先调用beginReadArray（）或beginWriteArray（），然后才能调用此函数**。

- `void clear()`

  **删除与此QSettings对象关联的主要位置中的所有条目**。

  后备位置的条目不会被删除。

  如果只想删除当前group（）中的条目，请改用remove（“”）。

- `bool fallbacksEnabled() const`

- `QString fileName() const`

- `QSettings::Format format() const`

- `QString group() const`

- `QTextCodec *iniCodec() const`

- `bool isAtomicSyncRequired() const`

- `bool isWritable() const`

- `QString organizationName() const`

- `QSettings::Scope scope() const`

- `void setAtomicSyncRequired(bool enable)`

- `void setFallbacksEnabled(bool b)`

- `QSettings::Status status() const`

- `void sync()`

# 4.Static Public Members

- `QSettings::Format defaultFormat()`
- `QSettings::Format registerFormat(const QString &extension, QSettings::ReadFunc readFunc, QSettings::WriteFunc writeFunc, Qt::CaseSensitivity caseSensitivity = Qt::CaseSensitive)`
- `void setDefaultFormat(QSettings::Format format)`
- `void setPath(QSettings::Format format, QSettings::Scope scope, const QString &path)`

# 5.Reimplemented Protected Functions

- `virtual bool event(QEvent *event) override`

