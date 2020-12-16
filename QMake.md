# 一、QMake使用

QMake提供了一个用于管理应用程序、库、其它组件的构建过程的面向工程系统。
QMake扩展了每个工程文件的信息，生成一个执行编译和链接过程的必须命令的MakeFile。

### 1、描述工程

工程文件.pro描述了工程信息。工程文件信息会被qmake用于生成包含构建过程中所需的所有命令的MakeFile。工程文件通常包含一系列头文件和源文件，通用配置信息以及音乐程序指定的细节，如应用程序的链接库、搜索路径。
工程文件包含一定数量的**不同元素**，*如注释、变量声明、内置函数以及简单的控制结构*。在大多数简单的工程中，只需要声明使用简单配置选项构建工程的源文件和头文件即可。

### 2、构建工程

对于简单的工程，只需要在工程的顶层目录运行qmake。默认情况下，qmake会生成一个构建工程的MakeFile，此时可以运行平台相关的make工具构建工程。
qmake也能用于生成工程文件。

### 3、预编译头文件

在大型工程中，可以利用预编译头文件的优势加速构建过程。

## 二、QMake工程文件

### 1、工程文件基本元素

工程文件包含qmake构建应用、库、插件的所有必须信息。工程使用的资源通常使用一系列声明指定，但支持用于描述不同平台和环境的不同构建过程的简单编程结构。
qmake使用的工程文件格式支持简单和相对复杂的构建系统。简单工程文件使用直接声明风格，定义标准变量指明工程需要的头文件和源文件。复杂工程可能需要使用流控制结构微调构建过程。
工程文件中不同类型的元素如下：
A、变量
工程文件中，变量用于保存字符串列表。简单工程中，变量会告诉qmake使用的配置选项，提供在构建过程中使用的文件名和路径。
qmake会在工程文件中查找某些变量，变量的内容将决定哪些内容会生成到MakeFile。例如，HEADERS和SOURCES变量的列表值会告诉qmake相关的头文件和源文件（工程文件所在目录）。
变量可以用于存储临时的列表值，覆写存在的列表值或是扩展新的值。下列代码显示了如何赋值列表值给变量：
`HEADERS = mainwindow.h paintwidget.h`
注意：第一种赋值方法只包括同一行指定的值。第二种赋值方法会使用“\”字符分隔列表值的项。
变量的列表值可以使用如下方式扩展：

```
SOURCES = main.cpp mainwindow.cpp \
          paintwidget.cpp
CONFIG += qt
```

CONFIG是一个qmake生成MakeFile文件时的特殊变量。
qmake会识别下列变量的值，并描述变量的内容。
CONFIG：通用工程配置选项
DESTDIR：可执行文件或库文件的输出目录
FORMS：由uic处理的UI文件列表
HEADERS：构建工程使用的头文件列表
QT：Qt相关配置选项
RESOURCES：包含到最终工程的资源文件列表
SOURCES：用于构建工程的源文件列表
TEMPLATE：构建工程的模板，决定构建过程输出一个应用，一个库或是一个插件
变量的内容可以通过在变量名称前加“$$”符号来访问，用于将一个变量的内容赋值给另一个变量。
`TEMP_SOURCES = $$SOURCES`
$$操作符可以被扩展用于操作字符串和值列表的内置函数中。
通常，变量用于包含空格分隔符的值列表，但有时需要指定包含空格的值，必须使用双引号包含。
`DEST = "Program Files"`
引号内的文本在值列表内作为单个值对待。类似的方法可以用于处理包含空格的路径，尤其是在Windows平台定义INCLUDEPATH和LIBS变量。

```
win32:INCLUDEPATH += "C:/mylibs/extra headers"
unix:INCLUDEPATH += "/home/user/extra headers"
```

B、注释
可以在工程文件中增加注释。注释需要#符号开头，直到#所在行结束。

```
# Comments usually start at the beginning of a line, but they
# can also follow other content on the same line.
```

为了在变量赋值中包括#，必须使用内置变量LITERAL_HASH。
C、内置函数和控制流
qmake提供了多个内置函数用于处理变量内容。在简单工程中，最常使用的函数是使用一个文件名作为参数的include函数。在工程文件中，给定文件的内容会被包含在include函数调用的位置。include函数最常用于包含其它工程文件.pro。
`include(other.pro)`
通过代码块作用域可以实现类似编程语言中IF语句的行为，支持条件控制结构。

```
win32 {
        SOURCES += paintwidget_win.cpp}
```

只有条件为true时，括号内的赋值才会有效。在这个例子中，特殊变量win32必须被设置。在 Windows平台上，win32会自动设置。当在其它平台上，通过运行带-win32参数选项的qmake可以指定win32。左括号必须与条件在同一行。
使用for函数通过遍历列表值可以构建一个简单的循环。下列代码会在目录存在的情况下增加目录到SUBDIRS变量。

```
EXTRAS = handlers tests docsfor(dir, EXTRAS) {
        exists($$dir) {
        SUBDIRS += $$dir
        }}
```

对变量进行更复杂的操作可以通过内置函数find、unique、count。内置函数可以提供对字符串、路径的操作，支持用户输入，并调用其它外部工具。

### 2、工程模板

TEMPLATE变量用于定义构建的工程的类型。如果工程文件中没有声明TEMPLATE变量，qmake会默认构建一个应用程序，并生成一个MakeFile文件。
下列时可用工程类型：
app：创建一个构建应用程序的MakeFile
lib：创建一个构建库的MakeFile
subdirs：创建一个包含使用SUBDIRS变量指定子目录的规则的MakeFile，每个子目录必须包含自己的工程文件。
vcapp：创建一个构建应用程序的Visual Studio平台的工程文件
vclib：创建一个构建库的Visual Studio平台的工程文件
vcsubdirs：创建一个在子目录构建工程的Visual Studio平台的解决方案文件
当使用subdirs模板时，qmake会生成一个MakeFile检查每个子目录，处理查找到的任何工程文件。并且在新生成的MakeFile上运行平台的make工具。SUBDIRS变量用于包含要处理的子目录列表。

### 3、通用配置

CONFIG变量用于指定编译器使用的选项和属性以及链接库。CONFIG变量可以增加任何选项，但是本节所述选项会被qmake内部识别。
下列选项控制用于构建工程的编译器选项：
release：工程使用release模式构建，如果debug也被指定会被忽略。
debug：工程使用debug模式构建
debug_and_release：工程使用debug和release两种模式构建
debug_and_release_target：工程使用debug和release两种模式构建，目标会被构建到debug和release两个目录下
build_all：如果指定debug_and_release，工程默认使用debug和release两种模式构建
autogen_precompile_source：自动生成.cpp文件，包含在.pro文件中指定的预编译头文件
ordered：当使用subdirs模板时，本选项会指定按照列出的目录给定的顺序处理
warn_on：编译器会尽可能多输出警告信息，如果指定warn_off，警告信息会被忽略
warn_off：编译器尽可能少的输出警告信息
copy_dir_files：打开要复制目录安装规则，而不只复制文件
debug_and_release选项是一个特殊选项，会开启工程的debug和release两种版本构建。qmake生成的MakeFile文件会包含两种版本的构建规则，使用下列方式进行调用：
`make all`
增加build_all选项到CONFIG变量会生成构建工程的默认规则，并且创建debug和release版本的安装目标。
注意：CONFIG变量指定每个选项可以用于条件作用域。可以使用CONFIG内置函数测试某个配置选项的表现。下列代码将展示CONFIG函数作为作用域的条件，测试opengl选项是否在用。

```
CONFIG(opengl) {
        message(Building with OpenGL support.)} else {
        message(OpenGL support is not available.)}
```

下列选项会定义构建工程的类型，注意，某些选项只有在特定平台才会生效。
qt：工程是一个Qt应用程序，会链接Qt库。可以使用QT变量控制应用程序需要的任何附加Qt模块
thread：工程是一个多线程应用程序
x11：工程是一个X11应用程序或库
当使用应用程序或库的工程模板时，很多配置选项用于微调构建过程。例如，如果应用程序使用Qt库，并且在debug模式构建多线程应用时，工程文件如下：
`CONFIG += qt thread debug`
注意：必须使用“+=”而不是“=”，否则qmake不会使用Qt配置决定工程需要的设置。

### 4、声明Qt库

如果CONFIG变量包含qt，qmake对Qt应用程序的支持会开启，这会使微调应用程序的Qt模块变得可能。用于声明需要扩展模块的QT变量可以实现微调。例如，可以使用下列代码开启XML和network模块：

```
CONFIG += qt
QT += network xml
```

注意QT默认包含core和gui模块，上述代码会增加network和xml模块到默认值列表。下列代码将会忽略默认模块，这会导致应用程序源码编译时错误。
`QT = network xml # This will omit the core and gui modules`
如果要不使用gui模块构建工程，可以使用“-=”排除gui模块。默认情况下，QT包含core和gui两个模块，所以下列代码会构建一个最小化工程。
`QT -= gui # Only the core module is used.`
下列选项可以用于QT变量：
Core：QtCore模块，默认包含
Gui：QtGui模块，默认包含
Network：QtNetwork模块
Opengl：QtOpenGL模块
Sql：QtSql模块
Svg：QtSvg模块
Xml：QtXml模块
Xmlpatterns：QtXmlPatterns
qt3support：Qt3Support模块
注意，增加opengl选项到QT变量会自动促使相应选项到增加到CONFIG变量。因此，对于Qt应用程序，增加opengl选项到QT和CONFIG变量不是必须的。

### 5、配置特性

qmake可以使用特性文件.prf文件设置额外的配置特性。这些额外特性常常提供了对构建过程中自定义工具的支持。为了增加特性到构建过程，可以增加特性名称到CONFIG变量。
例如，qmake可以利用pkg-config支持的外部库对构建过程进行配置，例如D-Bus或ogg外部库，代码如下：

```
CONFIG += link_pkgconfig
PKGCONFIG += ogg dbus-1
```

### 6、声明第三方库

如果在工程中使用除Qt支持的库以外的第三方库，需要在工程文件中指定。
qmake搜索库的路径和要链接的特定库要加入到LIBS变量的列表值中。给出库本身的路径，或是指定库的类unix风格标记和路径可以优先使用。
例如，下列代码展示如何指定库：
`LIBS += -L/usr/local/lib -lmath`
包含头文件的路径可以使用INCLUDEPATH变量指定。

## 三、QMake命令行使用

当qmake有多个选项在命令行运行，qmake的行为可以被自定义。qmake选项可以微调构建过程，提供有用的诊断信息，并指定工程的目标平台。

### 1、语法

qmake的使用采用下列简单形式：
`qmake [mode] [options] files`
Qmake支持两种不同的操作模式：默认模式下，qmake会使用工程文件的信息生成MakeFile文件，但qmake也可以生成工程文件。如果要显示设置模式，必须在其它所有选项前指定模式。模式有下列两个选项值：
-makefile：qmake生成MakeFile
-project：qmake生成工程文件，生成的过程文件可能需要编辑。

### 2、通用选项参数

为了自定义构建过程和覆写平台的默认设置，qmake可以在命令行指定一系列参数选项。下列基本选项提供有用的信息，指定qmake输出的文件的位置，控制输出到控制台调试信息的水平。
-help：qmake会回顾特性，给出有用帮助信息
-o file：qmake的输出会被重定向到file 文件。如果本选项不指定，qmake会根据运行的模式为输出选择一个合适的文件名。如果指定了“-”，输出定向到stdout。
-d：qmake会输出调试信息
对于每个目标平台都需要不同构建的有多个子目录的工程，qmake可以使用下列选项在每个工程文件中设置相应特定平台的变量。
-unix：qmake运行在unix模式，会使用unix的文件和路径命名规范，增加对unix的测试会成功，是所有的类unix平台的默认模式。
-macx：qmake运行在Mac OS X模式，会使用unix的文件和路径命名规范，增加对macx的测试会成功，是Mac OS X平台的默认模式。
-win32：qmake运行在win32模式，会使用Windows的文件和路径命名规范，增加对win32的测试会成功，是Windows平台的默认模式。
工程使用的模板通常在工程文件中使用TEMPLATE变量设置，可以使用下列选项覆写或修改：
-t tmpl：qamke会使用tmpl设置TEMPLATE变量，但仅在.pro文件被处理后。
-t prefix：增加前缀prefix到TEMPLATE变量
调整警告信息的水平可以帮助找到工程文件中的问题。
-Wall：qmake会报告已知的所有警告信息
-Wnone：不生成任何警告信息
-Wparser：qmake只会生成解析警告信息，解析警告信息会在解析工程文件过程中提醒开发者常见的陷阱和潜在问题。
-Wlogic：qmake会警告工程文件中的常见陷阱和潜在问题。例如，如果一个文件是否被多次放到文件列表中，或是如果文件没有找到，qmake会警告。

### 3、MakeFile模式选项

`qmake -makefile [options] files`
在makefile模式，qmake会生成用于构建工程的makefile文件。此外，下列选项可以被用于makefile模式中：
-after：qmake会在指定文件后的命令行上处理给定赋值
-nocache：qmake会忽略.qmake.cache文件
-nodepend：qmake不会生成任何依赖信息
-cache file：qmake会使用file作为缓存文件，其它的.qmake.cache文件会被忽略。
-spec spec：qmake会使用spec作为平台和编译器信息的路径，QMAKESPEC变量的值会被忽略。
可以在命令行上进行qmake赋值，赋值会在指定的所有文件处理。例如：
`qmake -makefile -unix -o Makefile "CONFIG+=test" test.pro`
上述代码会从使用unix路径名的test.pro文件生成一个Makefile。但指定选项的很多是默认的，不是必须的。因此，在Unix平台，上述代码可以简化如下：
`qmake "CONFIG+=test" test.pro`
如果确定变量在指定文件后被处理，可以使用-after选项。当-after选项指定，在-after后的所有命令行的赋值会被延迟到指定文件被解析后进行。

### 4、工程模式选项

`qmake -project [options] files`
在project模式下，qmake会生成一个工程文件。可以在project模式下使用下列选项：
-r：qmake会递归处理给定的目录
-nopwd：qmake不会查找当前源码的工作路径，只使用指定文件。
在project模式下，files参数是文件或目录列表。如果指定一个目录，会被包含到DEPENDPATH变量，相关代码会包含到生成的工程文件中；如果给定一个文件，会被追加到依赖于扩展的合适变量。例如，UI会被增加到FORMS变量，C++文件会被增加到SOURCES变量。

## 四、QMake平台相关事项

很多跨平台工程使用qmake的基本配置和特性进行处理。在一些平台上，利用平台相关特性有时是有用的，甚至是必须的。qmake直到很多特性，这些特性只能通过特定变量访问，特定变量只在独立平台上有效。

### 1、Mac OS X平台

本平台特有的特性包括支持创建通用二进制文件、框架和捆绑包。
A、源包和二进制包
源包中提供的qmake版本与二进制包中提供的配置略有不同，因为它使用了不同的特性规范。源包通常使用macx-g++规范，二进制包通常被配置为使用macx-xcode代码规范。
每个包的用户需要使用-spec参数选项调用qmake覆写配置。例如，在一个工程目录使用下列命令可以从一个二进制包生成Makefile文件：
`qmake -spec macx-g++`
B、框架使用
qmake会自动生成链接框架的构建规则，这些框架的标准框架路径在Mac OS X平台下是/Library/Frameworks/。
除了标准框架目录之外，需要向构建系统指定目录，通过增加链接器选项到QMAKE_LFLAGS变量可以实现。
`QMAKE_LFLAGS += -F/path/to/framework/directory/`
框架本身会通过附加-framework选项和框架的名称被链接到LIBS变量。
`LIBS += -framework TheFramework`
C、创建框架
任何给定的库项目都可以被配置，以便生成的库文件放置在准备部署的框架中。通过设置工程使用lib模板，并增加lib_bundle选项到CONFIG变量可以实现。

```
TEMPLATE = lib
CONFIG += lib_bundle
```

与库关联的数据使用QMAKE_BUNDLE_DATA变量指定。这将保存将使用库捆绑包进行安装的项，并且通常用于指定头文件集合。例如：

```
FRAMEWORK_HEADERS.version = Versions
FRAMEWORK_HEADERS.files = path/to/header_one.h path/to/header_two.h
FRAMEWORK_HEADERS.path = Headers
QMAKE_BUNDLE_DATA += FRAMEWORK_HEADERS
```

FRAMEWORK_HEADERS是用户定义的变量，用于定义使用特殊框架所需的头文件。追加FRAMEWORK_HEADERS到QMAKE_BUNDLE_DATA变量，确保头文件信息被增加到所安装的库捆绑包的资源集合中。框架的名称和版本由变量QMAKE_FRAMEWORK_BUNDLE_NAME和QMAKE_FRAMEWORK_VERSION指定，默认情况下，使用TARGET和VERSION变量的值。
D、创建通用二进制包
为了创建应用程序的通用二进制包，需要使用已经配置了-universal选项的Qt版本。
在二进制包中，支持的架构通常在CONFIG变量指定。例如，下列代码会使qmake生成同时支持PowerPC 和X86架构的通用二进制包的构建规则。
`CONFIG += x86 ppc`
此外，开发者使用PowerPC平台需要设置QMAKE_MAC_SDK变量。
E、创建和移动XCode项目
MAC OS X平台的开发者可以利用qmake对XCode工程文件的支持，通过运行qmake从已有的qmake工程文件生成一个XCode工程。
`qmake -spec macx-xcode project.pro`
注意：如果工程在磁盘上进行了移动，需要再次运行qmake处理工程文件生成一个XCode工程。
F、同时支持两种构建目标
要实现同时支持两个构建目标目前并不可行，因为在概念上，主动构建配置的XCode概念不同于qmake构建目标的概念。
XCode主动构建配置用于修改xcode配置、编译器选项以及类似的构建选项。不像Visual Studio，XCode不允许基于构建配置是否选择debug或release来选择特定的库文件。Qmake的debug和release设置会控制链接到执行文件的库文件。
目前不可能在qamke生成的XCode工程文件中设置XCode设置中的文件。
此外，所选的主动构建配置存储在.pbxuser文件中，.pbxuser文件是由XCode在第一次加载中生成的，而不是qamke创建的。

### 2、Windows平台

Windows平台特有的特性包括在部署Visual Studio 2005开发的Qt应用程序时支持创建Visual Studio工程文件和处理清单文件。
A、创建Visual Studio工程文件
使用Visual Studio编写Qt应用程序的开发人员可以使用Qt商业版提供的Visual Studio集成工具，而不必担心如何管理项目依赖关系。
但是，某些开发者可能需要导入已经存在的qmake工程到Visual Studio。qmake能够利用工程文件创建一个包含开发环境所需必须信息的Visual Studio工程。通过设置qmake工程模板为vcapp或vclib可以实现，可以使用命令行进行：
`qmake -tp vc`
在子目录递归生成.vcproj文件和在主目录生成文件如下：
`qmake -tp vc -r`
每次更新工程文件时，需要运行qmake生成一个更新的Visual Studio工程。
注意：如果使用Visual Studio Add-in，可以通过Qt->Import from .pro file菜单项导入.pro文件。
B、Visual Studio 2005 Manifest文件
当部署使用Visual Studio 2005构建的Qt应用程序时，确保应用程序链接时创建的Manifest文件被正确处理是必须的。对于生成DLL的工程来说是自动处理的。
移除嵌入在应用程序可执行文件的manifest文件可以使用下列赋值给CONFIG变量完成：
`CONFIG -= embed_manifest_exe`
移除嵌入在应用程序DLL文件的manifest文件可以使用下列赋值给CONFIG变量完成：
`CONFIG -= embed_manifest_dll`

### 3、Symbian平台

Symbian平台特有的特性包括处理静态数据，兼容性，栈和堆大小，编译器特定选项，应用程序或库的唯一标识符。
A、处理静态数据
如果应用程序使用了任何静态数据，构建系统需要了解这些静态数据。这是因为Symbian系统会试图在没有使用静态数据的情况下节省内存。
若要指定静态数据支持，将其添加到项目文件中：
`TARGET.EPOCALLOWDLLDATA = 1`
默认值为0
B、栈和堆大小
Symbian平台使用预定义大小的堆栈和堆。如果应用程序超过任一限制，则可能崩溃或无法完成其任务。毫无理由的崩溃常常可以追溯到堆栈和堆大小不足。
堆栈大小具有最大值，而堆大小具有最小值和最大值，均以字节指定。如果内存不可用，则最小值阻止应用程序启动。最小值和最大值由一个空间分隔。例如：

```
TARGET.EPOCHEAPSIZE = 10000 10000000
TARGET.EPOCSTACKSIZE = 0x8000
```

默认值取决于所使用的Symbian SDK的版本，但是，Qt工具链将此设置为最大可能值，并且不应该更改此值。
C、编译器特定选项
通用编译器选项通常使用QMAKE_CFLAGS和QMAKE_CXXFLAGS变量进行设置。为了设置特定的编译器选项，可以使用`QMAKE_CFLAGS.<compiler>`和`QMAKE_CXXFLAGS.<compiler>`。`<compiler>`可以是WINSCW架构（仿真器）的CW，或是ARMV5架构（硬件）的ARMCC，或是ARMV5架构（硬件）的GCCE。例如：

```
QMAKE_CXXFLAGS.CW += -O2
QMAKE_CXXFLAGS.ARMCC += -O0
```

D、唯一标识符
Symbian应用程序可能有附加的唯一标识符。下面是如何在工程文件中定义唯一标识符。
支持IDS的可用类型有四种：UID2、UID3、SID和VID。它们可以如下指定的：

```
TARGET.UID2 = 0x00000001
TARGET.UID3 = 0x00000002
TARGET.SID = 0x00000003
TARGET.VID = 0x00000004
```

如果未指定SID，则默认与UID3值相同。如果未指定UID3，qmake将自动生成适合开发和调试的UID3。应该为要释放的应用程序手动指定UID3值。
这儿也有一个UID1，但不会被任何应用所涉及。
UID2对于不同类型的文件具有特定的值；例如app/exes总是0x10039 CE。工具链将为最常见的文件类型（如EXE/APP和共享库DLL）设置值。
E、Capability
Capability为应用程序定义额外的特权，例如列出文件系统上的所有文件的能力。Capability在项目文件中定义如下：
`TARGET.CAPABILITY += AllFiles`
可以通过首先指定所有的能力，然后在它们前面减去不必要的能力来指定哪些能力不具备，例如：
`TARGET.CAPABILITY = ALL -TCB -DRM -AllFiles`

## 五、QMake高级功能

### 1、qmake高级功能简介

许多qamke工程文件使用varname=values和varname+=values定义的列表来简单描述工程使用的源文件和头文件。qamke还提供用于处理变量声明中提供的信息的其它运算符、函数和作用域。这些高级特性允许从单个工程文件生成多个平台的MakeFile文件。

### 2、操作符

在许多工程文件中，赋值操作符“=”和追加操作符“+=”可以用于包含有关工程的所有信息。典型的使用模式是将值列表赋值给变量，并根据各种测试的结果追加更多的值。由于qmake使用默认值定义了某些变量，因此有时需要使用移除操作符“-=”过滤出不需要的值。下面的运算符可以用来操作变量的内容。
赋值操作符“=”用于将一个值赋值给一个变量。
`TARGET = myapp`
上述代码会设置TARGET变量的值为myapp，会使用myapp覆写TARGET变量以前设置的任何值。
追加操作符“+=”用于追加一个新的值到变量的值列表中。
`DEFINES += QT_DLL`
上述代码会追加QT_DLL到预处理列表的定义中，以将其放入生成的Makefile文件中。
移除操作符“-=”用于从一个变量的值列表中移除一个值。
`DEFINES -= QT_DLL`
上述代码会将QT_DLL从预处理列表的定义中移除，以将其结果放入生成的Makefile文件中。
增加操作符“*=”会增加一个值到变量的值列表中，但仅限这个值不存在的情况。“*=”操作符胡阻止一个值被多次包含到变量中。
`DEFINES *= QT_DLL`
上述代码只有在预处理列表的定义不存在QT_DLL情况下，才会将QT*DLL加入，以将其结果放入生成的Makefile文件中。
注意：unique函数也可以确保变量中每个值只包含一个实例。
“~=”操作符可以代替指定的正则表达式匹配的任何值。
`DEFINES ~= s/QT*[DT].+/QT`
上述代码，值列表中的以QT_D或QT_T开头放入任何值使用QT替换。
“$$”操作符用于提取变量的内容，用于在变量中传递值或是提供给函数使用。

```
EVERYTHING = $$SOURCES $$HEADERS
message("The project contains the following files:")
message($$EVERYTHING)
```

### 3、作用域

作用域与过程化编程语言的IF语句比较类似。如果条件为true，作用域内的声明会被处理。
A、语法
作用域由一个条件和同一行跟随的一个左括号，一系列命令和定义，新一行的右括号组成。

```
<condition> {
        <command or definition>
        ...
}
```

左括号必须与条件在同一行。作用域可能会被连接多个条件。
B、作用域和条件
条件后面的作用域是一对括号中包含的一系列声明。例如：

```
win32 {
        SOURCES += paintwidget_win.cpp}
```

如果qmake运行在Windows平台，上述代码会增加paintwidget_win.cpp源文件到生成的Makefile的源文件列表中。如果qmake运行在其它平台，定义会被忽略。
在给定作用域使用的条件也可以取反，用于提供一组可替代的声明，仅在原始条件为false时才被处理。例如，假设想要在除了Windows平台上的所有平台上处理某些事务，代码如下：

```
!win32 {
        SOURCES -= paintwidget_win.cpp}
```

作用域可以将嵌套，以组合多个条件。例如，如果想要在某个平台包含某个特定文件，仅且在调试开启时处理。代码如下：

```
macx {
        debug {
            HEADERS += debugging.h
        }}
```

为了省去写很多作用域，可以通过使用“：”嵌套作用域。上述嵌套作用域可以重写如下：

```
macx:debug {
        HEADERS += debugging.h}
```

也可以使用“：”操作符执行单行条件赋值。
`win32:DEFINES += QT_DLL`
上述代码只有在Windows平台才会增加QT_DLL到DEFINES变量。
通常，“：”操作符更像一个逻辑与操作符，用于连接多个条件，并且必须所有条件为true。
“|”操作符的行为像一个逻辑或操作符（OR），连接多个条件，只要求其中一个条件为true。

```
win32|macx {
        HEADERS += debugging.h}
```

可以通过使用else作用域来向作用域内的内容提供替代声明。如果前一个作用域的条件为false，对else作用域进行处理。例如：

```
win32:xml {
        message(Building for Windows)
     SOURCES += xmlhandler_win.cpp} else:xml {
         SOURCES += xmlhandler.cpp} else {
        message("Unknown configuration")}
```

C、配置和作用域
存储在CONFIG变量的值会被qmake特殊处理。每个可能的值都可以作为作用域的条件。例如，CONFIG的值列表可以使用opengl值扩展。
`CONFIG += opengl`
上述代码的结果是测试opengl的任何作用域都会被处理，可以利用这个特性给最终的可执行文件一个合适的名称。

```
opengl {
        TARGET = application-gl} else {
        TARGET = application}
```

这个特性使得在不必丢失需要特定配置的所有自定义设置的情况下，就可以很容易地更改工程的配置。上述代码中，第一个作用域的声明被处理时，最终的可执行文件是application-gl。但是，如果opengl没有被指定，第二个作用域的声明会被处理，最终的可执行文件是application。
由于可以在CONFIG上设置自己的值，这提供了一种便捷的方法去自定义工程文件并微调生成的MakeFile文件。
D、平台的作用域值
除了在许多作用域条件中使用的win32、macx和unix值之外，还可以使用多种其它内置平台和编译器特定值对作用域进行测试。这些都是基于Qt的mkspecs目录中提供的平台规范。例如，工程文件中的下列代码会显示在用的当前规范和测试linux-g++规范。

```
message($$QMAKESPEC)
linux-g++ {
        message(Linux)}
```

只要在mkspecs目录中存在一个规范，就可以测试任何其他平台编译器组合。
在Symbian平台上，unix作用域为true。

### 4、变量

在工程文件中使用的很多变量是qmake在生成MakeFile文件时使用的特殊变量，例如，DEFINES,、SOURCES和HEADERS。用户可以创建自定义变量，当遇到对一个名称赋值时，qmake会使用给定的名称创建一个新的变量。例如：
`MY_VARIABLE = value`
对于自定义的变量，没有任何使用限制，因为qmake将忽略它们，除非在处理作用域时需要对它们进行评估。
通过变量名使用“$$”前缀可以将一个变量的值赋值给另一个变量。例如：
`MY_DEFINES = $$DEFINES`
现在MY_DEFINES变量包含工程文件中DEFINES变量在此处中的内容。等效于下列代码：
`MY_DEFINES = $${DEFINES}`
第二种写法允许将变量的内容追加到另一个值，而不必用空格分隔这两个值。例如，下列代码会确保最终的可执行文件有一个包含所使用模板的名称。
`TARGET = myproject_$${TEMPLATE}`
变量可以用于存储环境变量的内容。
为了获取qamke运行时的环境的值，可以使用$$(...)操作符。

```
DESTDIR = $$(PWD)
message(The project will be installed in $$DESTDIR)
```

在上述赋值后，当工程文件被处理时，PWD环境变量的值会被读取。
为了在生成Mafkefile文件时获取环境变量值的内容，可以使用$(...)操作符。

```
DESTDIR = $$(PWD)
message(The project will be installed in $$DESTDIR)

DESTDIR = $(PWD)
message(The project will be installed in the value of PWD)
message(when the Makefile is processed.)
```

在上述代码中，当工程文件被处理时，PWD的值会被立即读取，但$(PWD)会在生成的MakeFile文件中被赋值给DESTDIR变量。这使得构建过程更加灵活，只要在处理MakeFile文件时环境变量被正确设置。
特殊的$$[...]操作符被用于访问Qt构建时的多个配置选项。

```
message(Qt version: $$[QT_VERSION])
message(Qt is installed in $$[QT_INSTALL_PREFIX])
message(Qt resources can be found in the following locations:)
message(Documentation: $$[QT_INSTALL_DOCS])
message(Header files: $$[QT_INSTALL_HEADERS])
message(Libraries: $$[QT_INSTALL_LIBS])
message(Binary files (executables): $$[QT_INSTALL_BINS])
message(Plugins: $$[QT_INSTALL_PLUGINS])
message(Data files: $$[QT_INSTALL_DATA])
message(Translation files: $$[QT_INSTALL_TRANSLATIONS])
message(Settings: $$[QT_INSTALL_SETTINGS])
message(Examples: $$[QT_INSTALL_EXAMPLES])
message(Demonstrations: $$[QT_INSTALL_DEMOS])
```

使用这个操作符访问的变量通常用于使第三方插件与组件集成。例如，如果工程文件中有下列声明，Qt Designer插件可以与Qt Designer内置插件一起安装。

```
target.path = $$[QT_INSTALL_PLUGINS]/designer
INSTALLS += target
```

### 5、变量处理函数

qmake提供了一个内置函数的选择，以允许变量的内容被处理。内置函数处理被提供的参数，将值或值列表作为结果返回。为了将内置函数结果赋值给变量，必须对内置函数使用$$操作符，就像将一个变量的内置赋值给另一个变量一样。

```
HEADERS = model.h
HEADERS += $$OTHER_HEADERS
HEADERS = $$unique(HEADERS)
```

内置函数应该用于操作符的右侧。
可以自定义一个函数处理变量内容。自定义函数按如下定义：

```
defineReplace(functionName){
        #function code}
```

下列函数使用一个变量作为唯一参数，使用eval内置函数从变量中提取出了一个值列表，并且编辑了值列表。

```
defineReplace(headersAndSources) {
    variable = $$1
    names = $$eval($$variable)
    headers =
    sources =

    for(name, names) {
        header = $${name}.h
        exists($$header) {
            headers += $$header
        }
        source = $${name}.cpp
        exists($$source) {
            sources += $$source
        }
    }
    return($$headers $$sources)}
```

### 6、条件判断函数

qmake提供了用于编写作用域时作为条件的内置函数。这些内置函数不会返回一个值，而是指明成功或失败。

```
count(options, 2) {
        message(Both release and debug specified.)}
```

这些内置函数只能用于条件表达式。
可以自定义函数提供作用域的条件。下列代码用于测试一个列表中的每个文件是否存在，如果所有的文件都存在，返回true；否则返回false。

```
defineTest(allFiles) {
        files = $$ARGS

        for(file, files) {
            !exists($$file) {
                return(false)
            }
        }
        return(true)}
```

### 7、增加新的配置特性

Qmake允许用户创建自己的特性，增加到工程文件中，通过增加名称到CONFIG变量的值列表中。

## 六、QMake预编译头文件

### 1、预编译头文件简介

预编译头文件是一些编译器支持的一种性能特性，用于编译稳定的代码体，并将代码的编译状态存储在二进制文件中。在后续编译过程中，编译器将加载存储状态，并继续编译指定的文件。每个后续编译速度更快，因为不需要重新编译稳定的代码。qmake支持在某些平台上使用预编译头文件（PCH）和构建环境。
Windows平台：

```
nmake
Dsp projects (VC 6.0)
Vcproj projects (VC 7.0 & 7.1)
```

Mac OS X平台：

```
Makefile
Xcode
```

Unix平台：
GCC 3.4及以上版本

### 2、增加预编译头文件到工程

A、预编译头文件的注释
预编译头必须包含在整个工程中稳定和静态的代码。典型的PCH如下：

```
// Add C includes here

#if defined __cplusplus
// Add C++ includes here
#include <stdlib>
#include <iostream>
#include <vector>
#include <QApplication> // Qt includes
#include <QPushButton>
#include <QLabel>
#include "thirdparty/include/libmain.h"
#include "my_stable_class.h"
...
#endif
```

注意：预编译头文件需要从C++包含中分离出C包含，因为C文件的预编译头文件可能不包含C++代码。
B、工程选项
要在工程中使用预编译头文件，只需要在工程文件中定义PRECOMPILED_HEADER变量即可。
`PRECOMPILED_HEADER = stable.h`
qmake会处理其余事情，确保创建和使用预编译头文件。开发者不需要在HEADERS中包含预编译头文件，因为如果配置支持PCH，qmake会这样做。
默认情况下，Windows（以及Windows CE）为目标的MSVC和G++规范会通过precompile_header开启预编译。
使用precompile_header选项，可以在工程文件中触发条件代码块，以便在使用预编译头时添加设置。

```
precompile_header:!isEmpty(PRECOMPILED_HEADER) {
DEFINES += USING_PCH}
```

### 3、注意事项

在某些平台上，预编译头文件的文件名后缀与其他对象文件的文件名后缀相同。例如，下面的声明可能会导致两个不同的对象文件生成相同的名称：

```
PRECOMPILED_HEADER = window.h
SOURCES            = window.cpp
```

为了避免像这样的潜在冲突，确保将预编译的头文件赋予不同的名称是一种很好的工程实践。

### 4、工程实例

下列代码可以在Qt发布版的examples/qmake/precompile目录下可以找到。
mydialog.ui文件：

```
<ui version="4.0" >
 <author></author>
 <comment></comment>
 <exportmacro></exportmacro>
 <class>MyDialog</class>
 <widget class="QDialog" name="MyDialog" >
  <property name="geometry" >
   <rect>
    <x>0</x>
    <y>0</y>
    <width>401</width>
    <height>70</height>
   </rect>
  </property>
  <property name="windowTitle" >
   <string>Mach 2!</string>
  </property>
  <layout class="QVBoxLayout" >
   <property name="margin" >
    <number>9</number>
   </property>
   <property name="spacing" >
    <number>6</number>
   </property>
   <item>
    <widget class="QLabel" name="aLabel" >
     <property name="text" >
      <string>Join the life in the fastlane; - PCH enable your project today! -</string>
     </property>
    </widget>
   </item>
   <item>
    <widget class="QPushButton" name="aButton" >
     <property name="text" >
      <string>&Quit</string>
     </property>
     <property name="shortcut" >
      <string>Alt+Q</string>
     </property>
    </widget>
   </item>
  </layout>
 </widget>
 <pixmapfunction>qPixmapFromMimeSource</pixmapfunction>
 <resources/>
 <connections/>
</ui>
```

stable.h文件：

```
/* Add C includes here */

#if defined __cplusplus
/* Add C++ includes here */

# include <iostream>
# include <QApplication>
# include <QPushButton>
# include <QLabel>
#endif
```

myobject.h文件：

```
#include <QObject>

class MyObject : public QObject
{
public:
    MyObject();
    ~MyObject();
};
```

myobject.cpp文件：

```
#include <iostream>
#include <QDebug>
#include <QObject>
#include "myobject.h"

MyObject::MyObject()
    : QObject()
{
    std::cout << "MyObject::MyObject()\n";
}
```

util.cpp文件：

```
void util_function_does_nothing()
{
    // Nothing here...
    int x = 0;
    ++x;
}
```

main.cpp文件：

```
#include <QApplication>
#include <QPushButton>
#include <QLabel>
#include "myobject.h"
#include "mydialog.h"

int main(int argc, char **argv)
{
    QApplication app(argc, argv);

    MyObject obj;
    MyDialog dialog;

    dialog.connect(dialog.aButton, SIGNAL(clicked()), SLOT(close()));
    dialog.show();

    return app.exec();
}
```

precompile.pro文件：

```
TEMPLATE  = app
LANGUAGE  = C++
CONFIG   += console precompile_header

# Use Precompiled headers (PCH)
PRECOMPILED_HEADER  = stable.h

HEADERS   = stable.h \
            mydialog.h \
            myobject.h
SOURCES   = main.cpp \
            mydialog.cpp \
            myobject.cpp \
            util.cpp
FORMS     = mydialog.ui
```

## 七、QMake变量

### 1、QMake变量简介

QMake的基本行为受定义在工程构建过程中声明的变量的影响。某些变量用于声明资源，如每个平台中通用的头文件、源文件，其它变量用于定义指定平台中的编译器和链接器中的行为。
平台特定变量遵循变量扩展或修改的命名模式，但在其名称中包含相关平台的名称。例如，QMAKE_LIBS用于指定工程需要链接的库的列表，QMAKE_LIBS_X11用于扩展或覆写这个列表。

### 2、常用QMake变量

CONFIG
CONFIG变量用于指定工程配置和编译器选项。CONFIG变量的值会被qmake内部识别并有特殊的意义。
下列CONFIG值用于控制编译选项：
release：工程会以release模式构建，如果指定了debug，会被忽略。
debug：工程会被debug模式构建
debug_and_release：工程会以debug和release两种模式构建，会有一些意想不到的副作用。
build_all：如果指定了debug_and_release，工程默认会以debug和release两种模式构建
ordered：当使用subdirs模板时，本选项指定列出的子目录会以给出的顺序被处理
precompile_header：在工程中支持预编译头文件的使用
warn_on：编译器应该输出尽可能多的警告信息，如果指定warn_off，本选项会会忽略。
warn_off：编译器应该输出尽可能少的警告信息
由于 CONDIG变量中定义debug和release两个选项时，debug选项会覆盖release选项，如果想要使用debug和release两种模式构建工程，使用debug_and_release选项。此时，qmake会生成包含构建两种版本的规则的MakeFiles，使用make all可以调用。
当链接库时，qmake依赖于底层平台来了解库中链接的其它库。但是，如果是静态链接，除非使用下列的CONFIG选项，否则qmake不会得到这些信息。
create_prl：本选项使qmake能够追踪这些依赖关系。当本选项开启，qmake会创建一个以.prl结尾的文件，用于保存有关库的元信息。
link_prl：当本选项开启时，qmake会处理所有链接到应用程序的库，并找出他们的元信息。
注意：构建一个静态库时，需要使用create_prl；使用一个静态库时，需要使用link_prl。

DEFINES
qmake会将DEFINES变量的值作为C编译器预处理宏（-D）添加。
例如：DEFINES += USE_MY_STUFF QT_DLL

DEPENDPATH
此变量包含要查找依赖关系的所有目录的列表，会在查找包含文件时候使用。 
DESTDIR
指定输出目标文件的目录

DESTDIR_TARGET
本变量是由qmake内部设置的，基本是DESTDIR变量加上TARGET变量作为结尾。本变量的值通常由qmake或qmake.conf处理，并且很少需要修改。

DLLDESTDIR
指定dll目标文件拷贝到的地方

FORMS
本变量指定在编译前，uic要处理的UI文件。为了构建这些UI文件自动增加到工程，需要所有的依赖、头文件、源文件。

HEADERS
定义工程的头文件。qmake会为指定头文件生成依赖信息。如果头文件中需要moc，qmake也会自动检测，为了生成和链接moc文件，会增加相应的依赖和文件到工程。

```
HEADERS = myclass.h \
          login.h \
          mainwindow.h
```

INCLUDEPATH
本变量指定编译时需要查找搜索的inlucde路径。
为了指定一个包含空格的路径，将路径使用引号括起来。

```
win32:INCLUDEPATH += "C:/mylibs/extra headers"
unix:INCLUDEPATH += "/home/user/extra headers"
```

INSTALLS
本变量包含当make install或是类似的安装过程被执行时，要被安装的资源列表。INSTALLS值列表中的每个项会通常会使用属性定义，属性提供安装在哪儿的相关信息。
例如，下列代码target.path定义描述了构建目标被安装的路径，增加构建目标到INSTALLS会将构建目标加入要安装的资源列表中。

```
target.path += $$[QT_INSTALL_PLUGINS]/imageformats
INSTALLS += target
```

注意：qmake会忽略可执行文件，如果需要安装可执行文件，可以取消文件的可执行属性标识。

LIBS
本变量包含链接到工程的库列表。可以使用Unix平台-l(library)和-L(library path)的标识，qmake会正确处理Windows和Symbian平台上的这些库。例如：

```
unix:LIBS += -L/usr/local/lib -lmath
win32:LIBS += c:/mylibs/math.lib
```

注意：在Windows平台，使用-l选项指定库会使用最高版本的库。例如，math2.lib可能会潜在使用，替换math.lib。为了便面这种模糊性，推荐显示的指定库，通过使用包含库文件后缀.lib的文件名。
为了指定包含空格的路径，将路径使用引号括起来。

```
win32:LIBS += "C:/mylibs/extra libs/extra.lib"
unix:LIBS += "-L/home/user/extra libs" -lextra
```

默认情况下，使用库前，存储在LIBS变量中的库列表会被简化为唯一名称的列表。为了改变这种行为，可以使用在CONFIG变量使用no_lflags_merge选项。

MOC_DIR
本变量指定临时moc文件的存放路径。例如，

```
unix:MOC_DIR = ../myproject/tmp
win32:MOC_DIR = c:/myproject/tmp
```

PRECOMPILED_HEADER
为了加快工程的编译速度，本变量会为创建一个预编译头文件指明一个头文件。预编译头文件目前只支持某些平台（Windows所有MSVC工程类型, Mac OS X - Xcode, Makefile, Unix - gcc 3.3+版本）。

PWD
本变量指定指向当前文件被解析的目录的全路径。为了支持影子构建，编写工程文件时在源码树引用文件时会有用。

OUT_PWD
本变量包含指向生成MakeFile文件的目录的全路径

QMAKE
本变量包含qmake程序自己的名字，会放在生成的MakeFile文件中。

QMAKESPEC
当生成MakeFile时，本变量包含qmake配置要使用的名称。
使用QMAKESPEC环境变量会覆盖qmake配置。注意，由于qmake读取工程文件的方式，在工程文件内设置QMAKESPEC变量会没有效果。

QT
QT变量中存储的值用于控制工程中使用的Qt模块。
core：默认包含，QtCore模块
gui：默认包含，QtGui模块
network：QtNetwork模块
opengl：QtOpenGl模块
phonon：Phonon多媒体框架
sql：QtSql模块
svg：QtSvg模块
xml：QtXml模块
webkit：QtWebkit模块
默认，QT包含core和gui模块，在没有进一步配置的情况下确保构建一个GUI应用程序。
如果想要构建一个没有QtGui模块的工程，需要使用“-=”将gui排除。如：
`QT -= gui # Only the core module is used`
注意：增加opengl选项到QT变量会自动将相应的选项增加到CONFIG变量。因此，对于应用程序来说，不必增加opengl选项到QT和CONFIG两个变量。

QTPLUGIN
本变量包含静态插件的名字列表

QT_VERSION
本变量包含当前Qt的版本

QT_MAJOR_VERSION
本变量包含当前Qt版本的主版本号

QT_MINOR_VERSION
本变量包含当前Qt版本的次版本号

RC_FILE
本变量包含应用程序的资源文件的名称

RESOURCES
本变量包含资源集合文件的名称（qrc）

SOURCES
本变量包含工程中所有源文件的名称，如：

```
SOURCES = myclass.cpp \
        login.cpp \
        mainwindow.cpp
```

SUBDIRS
此变量与subdirs模板一起使用时，指定包含需要构建的工程部分的所有子目录或工程文件的名称。使用此变量指定的每个子目录必须包含其自己的工程文件。
建议每个子目录中的工程文件与子目录本身具有相同的基名，因为这样可以省略文件名。例如，如果子目录是myapp，目录中的工程文件应用命名为myapp.pro。
或者，可以在任何目录中指定.pro文件的相对路径。强烈建议只在当前工程的父目录或其子目录中指定路径。例如：

```
SUBDIRS = kernel \
          tools \
          myapp
```

如果需要确保子目录按指定的顺序构建，需要在CONFIG 变量增加ordered选项。
`CONFIG += ordered`
通过修改附加的属性SUBDIRS的默认行为，支持的附加调节属性如下：
.subdir：使用指定的子目录取代SUBDIRS的值
.file：显示指定子工程的pro文件，不能与修饰符.subdir结合使用
.condition：指定bld.inf定义，如果子工程被构建，必须为true。
.depends：子工程依赖于指定的子工程，只对生成MakeFile的平台可用。
.makefile：子工程的MakeFile，只对生成MakeFile的平台可用。
.target：子工程相关的MakeFile目标的基字符串
例如，定义两个子目录，它们的值不同于SUBDIRS的值。

```
SUBDIRS += my_executable my_library
my_executable.subdir = app
my_executable.depends = my_library
my_library.subdir = lib
```

Visual Studio不支持ordered选项。

TARGET
本变量指定目标文件名称
TEMPLATE = app
TARGET = myapp
SOURCES = main.cpp
上述代码会在创建一个可执行文件myapp（Unix）和myapp.exe（Windows）。

TEMPLATE
本变量指定目标文件的名称。
app ：建立一个应用程序的Makefile，是默认值。
lib：建立一个库的Makefile。
vcapp：建立一个应用程序的Visual Studio项目文件。
vclib：建立一个库的Visual Studio项目文件。
subdirs：特殊的模板，
TRANSLATIONS
本变量包含翻译文件（.ts）列表，

VERSION
本变量用于包含应用程序或库的版本号。

## 八、QMake函数

### 1、QMake函数简介

QMake提供内置函数用于处理变量的内容以及在配置过程中进行测试。处理变量内容的函数通常会返回可赋值给其它变量的值，可以使用$$FuncionName获取函数的返回值；进行测试的函数通常作为作用域的条件部分使用。

### 2、替换函数

qmake提供了在配置过程中处理变量内容的函数。这些函数称为替换函数。通常，替换函数返回可以赋值给其它变量的值。可以通过在函数名称前使用$$操作符来获取这些值。

basename(variablename)
返回指定文件的基本文件名

```
FILE = /etc/passwd
FILENAME = $$basename(FILE) #passwd
```

dirname(file)
返回指定文件file中的目录部分

```
FILE = /etc/X11R6/XF86Config
DIRNAME = $$dirname(FILE) #/etc/X11R6
```

find(variablename, substr)
在variablename变量的所有值中查找匹配substr字符串的值，substr可能是正则表达式。

join(variablename, glue, before, after)
使用glue连接variablename变量中的值。如果变量的值非空，在值前面加一个前缀before，在值的后面加一个后缀after。Variablename是必须参数，其它参数默认是空字符串。如果需要在glue、before、after中对空格进行编码，必须对它们使用引号。

member(variablename, position)
返回variablename变量的值列表中position位置的值。如果在指定位置不能找到值项，返回一个空字符串。Variablename是必须参数，如果不指定position参数，position默认为0，返回variablename变量的值列表中的第一个值。

prompt(question)
显示指定的question，返回一个从stdin读取的值。

quote(string)
将整个string转换为单个实体，返回结果。这只是一种把字符串括上双引号的花样方法。

replace(string, old_string, new_string)
使用new_string替换在变量string中出现的old_string。如：

```
MESSAGE = This is a tent.
message($$replace(MESSAGE, tent, test))
sprintf(string, arguments...)
```

使用逗号分隔的函数参数arguments替换1%——9%，返回处理后的字符串。

unique(variablename)
返回变量中值的链表，如果有重复的删除。

```
ARGS = 1 2 3 2 5 1
ARGS = $$unique(ARGS) #1 2 3 5
```

### 3、测试函数

CONFIG(config)
本函数用来测试放置在CONFIG变量中的变量。这与常规旧式（tmake）作用域相同，但具有附加的优点，可以将第二个参数传递给活动配置进行测试。由于CONFIG变量中值的顺序是重要的，CONFIG的第二个参数用于指定要考虑的值的集合。例如：

```
CONFIG = debug
CONFIG += release
CONFIG(release, debug|release):message(Release build!) #will print
CONFIG(debug, debug|release):message(Debug build!) #no print
```

由于release作为活跃设置， CONFIG用于生成构建文件。在一般情况下，不需要第二个参数，但对于特定的互斥测试，这是非常宝贵的。

contains(variablename, value)
如果variablename变量包含value值，成功；否则，失败。可以使用作用域检查此函数的返回值。

```
contains( drivers, network ) {
        # drivers contains 'network'
        message( "Configuring for network build..." )
        HEADERS += network.h
        SOURCES += network.cpp}
```

上述代码只有在drivers变量包含network值的条件下，作用域才会被处理。

count(variablename, number)
如果variablename变量包含指定数量number的值列表，成功；否则，失败。
本函数用于确保作用域内的声明仅在变量包含正确数值的情况下才被处理。

```
options = $$find(CONFIG, "debug") $$find(CONFIG, "release")
count(options, 2) {
        message(Both release and debug specified.)}
```

error(string)
函数无返回值，用于显示给定的字符串string给用户，并退出。只用于不可恢复的错误。
`error(An error has occurred in the configuration process.)`

eval(string)
评估使用qamke语法规则的string字符串的内容，返回true。在string字符串中可以使用定义和赋值来修改现有变量的值或创建新的定义。

```
eval(TARGET = myapp) {
        message($$TARGET)}
```

注意：引号可以用来分隔字符串，如果不需要返回值，则可以放弃。

exists(filename)
测试给定文件名的文件是否存在。如果文件存在，函数成功；否则，失败。如果文件名是一个正则表达式，如果有任何文件匹配成功，则函数执行成功。

```
exists( $(QTDIR)/lib/libqt-mt* ) 
{
      message( "Configuring for multi-threaded Qt..." )
      CONFIG += thread
}
```

for(iterate, list)
这个特殊的测试函数将开启循环，遍历列表中的所有值，依次对每个值设置迭代。为方便起见，如果列表为1…10，则迭代将遍历值1到10。
在for循环的条件行后使用else作用域是不允许的。

```
LIST = 1 2 3
for(a, LIST):exists(file.$${a}):message(I see a file.$${a}!)
```

message(string)
此函数简单地将消息写入控制台。不像error()函数，本函数允许继续处理。
`message( "This is a message" )`
上述代码会将"This is a message"消息写入控制台。引号的使用是可选的。
注意：默认，对于给定项目，qmake生成的每个MakeFile文件都会写入消息。如果要确保每个项目只显示一次消息，在构建期间，可以测试build_pass变量，并在相邻build_pass变量的作用域中过滤出消息。
`!build_pass:message( "This is a message" )`

include(filename)
将filename指定的文件的内容包含在当前工程所在的点。如果文件已经被包含，函数成功；否则，失败。被包含的文件要被立即处理。
通过使用此函数作为作用域的条件，可以检查文件是否被包含。

```
include( shared.pri )
OPTIONS = standard custom!include( options.pri ) {
        message( "No custom build options specified" )
OPTIONS -= custom}
```

infile(filename, var, val)
当文件被qmake解析时，如果filename文件包含有val值的var变量，成功；否则，失败。如果不指定第三个参数val，函数只会测试文件中是否包含var变量。
`isEmpty(variablename)`
如果variablename变量为空，成功；否则，失败。等价于count(variablename, 0)。

```
isEmpty(CONFIG) {
CONFIG += qt warn_on debug}
```

system(command)
在shell中执行给定的命令command，如果command返回一个0的退出状态，成功；否则，失败。
可以使用system函数从command命令获取stdout和stderr，赋值给变量。如：

```
UNAME = $$system(uname -s)
contains( UNAME, [lL]inux ):message( This looks like Linux ($$UNAME) to me )
```

warning(string)
显示给定的字符串string，总会成功。与message()相同。

packagesExist(packages)
使用PKGCONFIG机制决定在工程解析时是否存在给定的packages。通常用于打开、关闭特性。如:

```
packagesExist(sqlite3 QtNetwork QtDeclarative) 
{
DEFINES += USE_FANCY_UI
}
```

## 九、配置QMake环境

### 1、属性

qmake拥有一个持久信息系统，允许在qmake中一次设置变量，以后每次调用qmake时，可以查询该值。
在qmake中按如下设置变量：
`qmake -set VARIABLE VALUE`
使用适当的变量和值应该代替VARIABLE和VALUE。
为了从qmake中取出信息，如下：

```
qmake -query VARIABLE
qmake -query #queries all current VARIABLE/VALUE pairs..
```

注意：qmake -query只会列出先前使用qmake -set VARIABLE VALUE设置的变量。
属性信息会被保存到QSetting对象中对象中（意味着它将存储在不同平台的不同位置）。由于VARIABLE也可以被版本化，可以在较旧版本的qamke中设置一个值，而较新版本将检索此值。但是，如果在较新版本的qmake设置VARIABLE，将不能再旧版本使用这个值。通过前缀化qmake的版本到VARIABLE，可以查询特定版本的变量，代码如下：
`qmake -query "1.06a/VARIABLE"`
qmake也有内置属性的概念，例如可以使用QT_INSTALL_PREFIX属性查询这个qmake版本的Qt安装。
`qmake -query "QT_INSTALL_PREFIX"`
由于没有被版本化，内置属性不能有前缀版本，并且qmake的每个版本都有自己的内置属性值集合。

```
QT_INSTALL_PREFIX：Where the version of Qt this qmake is built for resides
QT_INSTALL_DATA - Where data for this version of Qt resides
```

QMAKE_VERSION：当前qmake的版本
最终，这些值可以在一个工程文件中查询，使用如下语法：
`QMAKE_VERS = $$[QMAKE_VERSION]`

### 2、QMAKESPEC

qmake需要一个平台和编译器的描述文件，文件包含很多用于生成MakeFile的默认值。标准的Qt版本带有很多这类文件，位于Qt安装目录的 mkspecs子目录下。
QMAKESPEC环境变量包含下列的任何值：
指向包含qmake.conf文件的目录的完整路径。qmake会打开目录中的qmake.conf文件。如果文件不存在，qmake会以错误退出。
平台-编译器组合的名称。qmake会搜索，当Qt编译时
QMAKESPEC路径会自动增加到INCLUDEPATH系统变量。

### 3、INSTALLS

在Unix上，使用构建工具安装应用程序和库是相同的。例如，通过调用make install。qmake有安装集的概念，。
例如，documentation文件集合使用如下方式描述：

```
documentation.path = /usr/local/program/doc
documentation.files = docs/*
```

path成员告诉qmake，文件应该安装在/usr/local/program/doc路径，files成员指定要拷贝到安装目录下的文件。本例中，docs目录下的所有文件将被拷贝到/usr/local/program/doc目录。
一旦安装集已被完全描述，可以像如下代码将其添加到安装列表中：
`INSTALLS += documentation`
qmake会确保指定的文件被拷贝到安装目录。如果需要对安装过程进行更大的控制，还可以为对象的额外成员提供定义。例如，下列代码告诉qmake为安装集执行一系列的命令：
`unix:documentation.extra = create_docs; mv master.doc toc.doc`
unix作用域确保这些特殊的命令只会在unix平台下执行。其它平台适合的命令可以使用其它作用域规则定义。
在执行对象的其他成员中的指令前执行extra成员中指定的命令。
如果追加内置的安装集到INSTALLS变量，并且不指定files和extra成员，qmake会决定拷贝哪些内容。目前，只支持内置安装集的是target：

```
target.path = /usr/local/myprogram
INSTALLS += target
```

上诉代码中，qmake知道拷贝哪些内容，自动处理安装过程。

### 4、缓存文件

缓存文件是qmake读取的特殊文件，用于查找不在qmake.conf文件、工程文件或是命令行指定的设置。如果qmake运行时没有指定-nocache选项，qmake会试图在当前目录的上层目录下查找名称为.qmake.cache的文件。如果没有找到，qmake会忽略这个处理步骤。 如果qmake找到一个.qmake.cache文件，qmake会在处理工程文件前首先处理这个文件。

### 5、库依赖

经常在链接到一个库时，qmake依赖于底层平台来了解库中链接的其他库，并让平台将它们拉入。然而，在很多情况下，这是不够的。例如，当静态链接一个库时，没有链接到其他库，因此不会创建与这些库的依赖关系。但是，后续链接到该库的应用程序需要知道在哪里可以找到静态库所需的符号。为了帮助解决这种情况，qmake尝试在适当的情况下遵循库的依赖关系，但是必须通过以下两个步骤明确地启用该行为。
A、开启库自身的依赖追踪。要做到这点，必须告诉qmake保存库的有关信息。
`CONFIG += create_prl`
这只和lib模板有关，其它模板会被忽略。当启用此选项时，qmake会创建一个在.prl结尾的文件，该文件将保存库相关的一些元信息。这个元文件就像一个普通的工程文件，但只包含内部变量声明。可以自由查看该文件，如果删除该文件，则qmake会知道在需要时重新创建它，即在后续读取工程文件时，或者如果依赖库（以下描述）已经发生变化时。在安装此库时，通过将其指定为INSTALLS声明中的目标，qmake将自动将.prl文件拷贝到安装路径。
B、在使用静态库的应用程序中读取该元信息。
`CONFIG += link_prl`
当该选项开启，qmake会处理由应用程序链接的所有库，并找到它们的元信息。qmake会使用它来确定相关链接信息，特别是向应用程序工程文件的DEFINES以及LIBS添加值。一旦qmake处理了该文件，它将查看LIBS变量中新引入的库，并找到它们的依赖.prl文件，直到所有库都被解析。此时，MakeFile文件按常规创建，并且库与应用程序显式链接。
prl文件的内部结构是关闭的，因此后续可以很容易地进行更改。prl文件并不是用来被手工改变的，只能由{qmake Manual#qmake}{qmake}创建，并且不应该在操作系统之间传输，由于它们可能包含依赖于平台的信息。

### 6、文件扩展

在正常情况下，qmake会尝试为平台使用适当的文件扩展名。但是，有时需要重写每个平台的默认选项，并显式定义用于qmake的文件扩展名。这是通过重新定义某些内置变量来实现的；
例如，用于moc文件的扩展可以用工程文件中的以下赋值来重新定义。
`QMAKE_EXT_MOC = .mymoc`
下列变量可用于重新定义qmake所识别的公共文件扩展名。
QMAKE_EXT_MOC：修改包含的moc文件的扩展
QMAKE_EXT_UI：修改designer UI文件的扩展
QMAKE_EXT_PRL：修改库依赖文件的扩展
QMAKE_EXT_LEX：修改文件后缀（LEXSOURCES）
QMAKE_EXT_YACC：修改文件后缀（YACCSOURCES）
QMAKE_EXT_OBJ：修改生成的对象文件的后缀
上述所有变量都只接受第一个值，所以必须给它分配一个值，会在整个工程文件中使用。有两个变量可以接受一个值列表：
QMAKE_EXT_CPP：qmake会将这些后缀的文件解释为C++源文件 QMAKE_EXT_H：qmake会将这些后缀的文件解释为C和C++头文件

### 7、自定义MakeFile文件输出

qmake试图实现跨平台构建工具所期望的一切。当真的需要运行特定的平台相关命令时，常常是不太理想的。这可以通过对不同qmake后端的特定指令来实现。
对MakeFile文件输出的定制是通过对象风格的API实现的，就像在qmake中其它地方发现的那样。对象是通过指定成员来自动定义的，例如：

```
mytarget.target = .buildfile
mytarget.commands = touch $$mytarget.target
mytarget.depends = mytarget2
mytarget2.commands = @echo Building $$mytarget.target
```

上述代码定义了一个名为mytarget的qmake目标，mytarget目标包含一个名为.buildfile的MakeFile目标，.buildfile使用touch命令依次生成。最终，.depends成员指定mytarget目标依赖于mytarget2。mytarget2是一个伪目标，只定义了一些显示到控制台的文本。
最后一步是指示qmake，这个对象是要建立的目标。
QMAKE_EXTRA_TARGETS += mytarget mytarget2
这就是实际构建自定义目标所需做的一切。当然，可能希望将其中一个目标绑定到qmake构建目标。要做到这一点，只需要将MakeFile目标包含到PRE_TARGETDEPS列表中。
下表是QMAKE_EXTRA_TARGETS变量的可用选项的概述。
commands：生成自定义构建目标的命令
CONFIG：自定义构建目标的特定配置选项
depends：自定义目标锁依赖的现有构建目标
recurse：为了调用子目标的MakeFile文件，当创建MakeFile文件时，指定使用哪些子目标。当CONFIG变量设置了recursive才能使用。
recurse_target：通过MakeFile文件中的子目标MakeFile文件，指定要构建的目标。
target：自定义构建目标创建的文件
CONFIG变量：
recursive：指明MakeFile中要创建的规则，因而会在子目标的MakeFile文件中调用相关目标。默认会为每个子目标创建一个实体。
为了方便起见，还有一种新的编译器或预处理器的工程定制方法。

```
new_moc.output  = moc_${QMAKE_FILE_BASE}.cpp
new_moc.commands = moc ${QMAKE_FILE_NAME} -o ${QMAKE_FILE_OUT}
new_moc.depend_command = g++ -E -M ${QMAKE_FILE_NAME} | sed "s,^.*: ,,"
new_moc.input = NEW_HEADERS
QMAKE_EXTRA_COMPILERS += new_moc
```

通过上面的定义，如果有可用的moc，可以使用moc随时替换。
在给定的NEW_HEADERS变量的所有参数上执行命令。结果写到output成员指定文件。这个文件会被增加到工程中的其它源文件。此外，为了生成依赖信息，qmake会执行depend_command命令，也将这些信息放到工程中。
这些命令可以很容易地放入缓存文件中，从而允许后续工程文件向NEW_HEADERS添加参数。
下表概述了QMAKE_EXTRA_COMPILERS变量的可用选项。
commands：用于从输入产生输出的命令。
CONFIG：为自定义编译器指定配置选项
depend_command：指定用于生成输出依赖项列表的命令。
dependency_type：指定输出的文件类型，如果它是已知类型（TYPE_C, TYPE_UI, TYPE_QRC），则使用其中的一种类型处理它。
depends：指定输出文件的依赖
input：包含使用自定义编译器处理的文件的变量
name：对自定义编译器所做事情的描述。只用于某些后端
output：自定义编译器创建的文件名
output_function：指定用于创建文件名的qmake自定义函数
variable_out：应该将从输出创建的文件添加到变量。
指定到CONFIG选项的成员：
commands：用于从输入产生输出的命令。
CONFIG：为自定义编译器指定配置选项
depend_command：指定用于生成输出依赖项列表的命令。
dependency_type：指定输出的文件类型，如果它是已知类型（TYPE_C, TYPE_UI, TYPE_QRC），则使用其中的一种类型处理它。
depends：指定输出文件的依赖
input：包含使用自定义编译器处理的文件的变量
name：对自定义编译器所做事情的描述。只用于某些后端
output：自定义编译器创建的文件名
output_function：指定用于创建文件名的qmake自定义函数
variable_out：应该将从输出创建的文件添加到变量

# qmake

qmake是一个工具，可帮助**简化跨不同平台的开发项目的构建过程**。 qmake可以**自动生成Makefile**，因此只需几行信息即可创建每个Makefile。 qmake**可以用于任何软件项目**，无论它是否用Qt编写。

qmake根据项目文件中的信息生成一个Makefile。 项目文件由开发人员创建，通常很简单，但是可以为复杂项目创建更复杂的项目文件。 qmake包含其他功能来支持Qt开发，并自动包括moc和uic的构建规则。 qmake还可以为Microsoft Visual Studio生成项目，而无需开发人员更改项目文件。

## 1.qmake Tutorial

Let's assume that you have just finished a basic implementation of your application, and you have created the following files:

- hello.cpp
- hello.h
- main.cpp

您可以在Qt发行版的examples / qmake / tutorial目录中找到这些文件。 您对应用程序设置唯一了解的其他事情是它是用Qt编写的。 首先，使用您喜欢的纯文本编辑器，在examples / qmake / tutorial中创建一个名为hello.pro的文件。 您需要做的第一件事是添加一些行，这些行告诉qmake有关开发项目的源文件和头文件。

### 1.1.添加源文件

我们将首先将源文件添加到项目文件中。 为此，您需要使用SOURCES变量。 只需使用SOURCES + =开始新行，然后将hello.cpp放在其后即可。 您应该具有以下内容：

```c++
SOURCES += hello.cpp
```

我们对项目中的每个源文件重复此操作，直到得到以下结果：

```c++
 SOURCES += hello.cpp
 SOURCES += main.cpp
```

如果您喜欢使用类似Make的语法，将所有文件一目了然，则可以使用换行符转义，如下所示：

```c++
 SOURCES = hello.cpp \
           main.cpp
```

### 1.2.添加头文件

现在源文件已列在项目文件中，现在必须添加头文件。 这些文件的添加方式与源文件完全相同，只是我们使用的变量名是HEADERS。

完成此操作后，您的项目文件应如下所示：

```c++
 HEADERS += hello.h
 SOURCES = hello.cpp \
 		  main.cpp
```

### 1.3.设置目标

**目标名称是自动设置的； 它与项目文件相同，但后缀适合平台**。 例如，如果项目文件名为hello.pro，则目标将是Windows上的hello.exe和Unix上的hello。 如果要使用其他名称，可以在项目文件中进行设置：

```c++
TARGET = helloworld
```

最后一步是设置CONFIG变量。 由于这是Qt应用程序，因此我们需要将qt放在CONFIG行上，以便qmake将添加要链接的相关库，并确保生成的Makefile中包含moc和uic的构建行。

完成的项目文件应如下所示：

```c++
CONFIG += qt
HEADERS += hello.h
SOURCES = hello.cpp \
 		 main.cpp
```

现在，您可以使用qmake为您的应用程序生成Makefile。 在命令行的项目目录中，键入以下内容：

```c++
qmake -o Makefile hello.pro
```

然后根据您使用的编译器键入make或nmake。

对于Visual Studio用户，qmake也可以生成.dsp或.vcproj文件，例如：

```c++
 qmake -tp vc hello.pro
```

### Making an Application Debuggable