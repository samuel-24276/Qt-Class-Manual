# QSettings

# 1.Detailed Description

用户通常希望应用程序在整个会话中记住其设置（窗口大小和位置，选项等）。 此信息通常存储在Windows上的系统注册表中，以及macOS和iOS上的属性列表文件中。 在Unix系统上，在没有标准的情况下，许多应用程序（包括KDE应用程序）都使用INI文本文件。
QSettings是围绕这些技术的抽象，使您能够以可移植的方式保存和恢复应用程序设置。 它还支持自定义存储格式。
QSettings的API基于QVariant，使您可以省力地保存大多数基于值的类型，例如QString，QRect和QImage。
如果您需要的只是一个基于非持久性内存的结构，请考虑改用QMap <QString，QVariant>。

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
  INI文件格式对键的语法有严格的限制。 Qt通过使用％作为键中的转义字符来解决此问题。此外，如果您保存一个顶级设置（其中没有反斜杠的键，例如“ someKey”），它将显示在INI文件的“常规”部分中。为避免覆盖其他键，如果您使用诸如“ General / someKey”之类的键来保存内容，则该键将位于“％General”部分，而不是“ General”部分。
  遵循我们应该在接受内容时保持自由和在生成内容时保持保守的理念，QSettings将接受Latin-1编码的INI文件，但生成纯ASCII文件，其中非ASCII值使用标准INI转义序列进行编码。为了使INI文件更具可读性（但兼容性可能较低），请调用setIniCodec（）。

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
- `QSettings(QSettings::Format format, QSettings::Scope scope, const QString &organization, const QString &application = QString(), QObject *parent = nullptr)`
- `QSettings(QSettings::Scope scope, const QString &organization, const QString &application = QString(), QObject *parent = nullptr)`
- `QSettings(const QString &organization, const QString &application = QString(), QObject *parent = nullptr)`
- `virtual ~QSettings()`
- `QStringList allKeys() const`
- `QString applicationName() const`
- `void beginGroup(const QString &prefix)`
- `int beginReadArray(const QString &prefix)`
- `void beginWriteArray(const QString &prefix, int size = -1)`
- `QStringList childGroups() const`
- `QStringList childKeys() const`
- `void clear()`
- `bool contains(const QString &key) const`
- `void endArray()`
- `void endGroup()`
- `bool fallbacksEnabled() const`
- `QString fileName() const`
- `QSettings::Format format() const`
- `QString group() const`
- `QTextCodec *iniCodec() const`
- `bool isAtomicSyncRequired() const`
- `bool isWritable() const`
- `QString organizationName() const`
- `void remove(const QString &key)`
- `QSettings::Scope scope() const`
- `void setArrayIndex(int i)`
- `void setAtomicSyncRequired(bool enable)`
- `void setFallbacksEnabled(bool b)`
- `void setIniCodec(QTextCodec *codec)`
- `void setIniCodec(const char *codecName)`
- `void setValue(const QString &key, const QVariant &value)`
- `QSettings::Status status() const`
- `void sync()`
- `QVariant value(const QString &key, const QVariant &defaultValue = QVariant()) const`

# 4.Static Public Members

- `QSettings::Format defaultFormat()`
- `QSettings::Format registerFormat(const QString &extension, QSettings::ReadFunc readFunc, QSettings::WriteFunc writeFunc, Qt::CaseSensitivity caseSensitivity = Qt::CaseSensitive)`
- `void setDefaultFormat(QSettings::Format format)`
- `void setPath(QSettings::Format format, QSettings::Scope scope, const QString &path)`

# 5.Reimplemented Protected Functions

- `virtual bool event(QEvent *event) override`